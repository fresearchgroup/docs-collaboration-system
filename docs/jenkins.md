---
id: jenkins
title: Jenkins Set Up
sidebar_label: Jenkins Set Up
---

Jenkins is a powerful application that allows continuous integration and continuous delivery of projects, regardless of the platform you are working on.

## Continuous Integration

Continuous Integration is a development practice that requires developers to integrate
code into a shared repository at regular intervals. This concept was meant to remove the
problem of finding later occurrence of issues in the build lifecycle. Continuous integration requires the developers to have frequent builds. The common practice is that whenever a code commit occurs, a build should be triggered.

##  UsingJjenkins for Continuous Integration

<img src="/collaboration-system/img/jenkins.jpg">

Note : Wherever deploy is written in the figure Ansible scripts are needed.

1. Jenkins will trigger ansible scripts to deploy the project before performing Selenium tests.

2. After running selenium tests Jenkins will trigger ansible to deploy the project to production env. )


## Steps to be followed for creating a jenkins project

1. Install Jenkins and configure it.

2. Click on new item on jenkins , enter the name of the project , select freestyle project and click ok.

3. Go to Manage Jenkins and then Manage Plugins. Then click on Available and in the search tab search for the following plugins to be installed.
    - Git plugin
    - Continuous Integration game
    - Build Pipeline Plugin
    - Ansible plugin
    - Selenium plugin
    - SSH plugin

Install them.

4. In the new project created select configure.

5.  In the general tab give the project name.

6.  In source code management select git. In git give repository URL credentials,branches to build etc.

7.  In build triggers , select build periodically and give the interval to build the file.

      eg : H/15 * * * * (build every 15 minutes)

8. In build triggers, select Poll SCM and give the interval when to poll the changes in the SCM.

9.  In build select execute shell and execute the script to be run.

Example--
```
#!/bin/bash
export WORKSPACE=`pwd`
mkvirtualenv --python=/usr/bin/python3 testing
workon testing
pip3 install -r requirements.txt
python3 manage.py migrate
python3 manage.py test BasicArticle
```

10. Save the project.

11. Give the post build action if any has to be given.

    Eg.  build another project, script to be executed

12. Build the project using build now.

13. To see the output select the console output  of the project


## Creating a pipeline

We can create a pipeline using any number of freestyle projects. In the post build action of the project we can specify which project has to be executed next. We can select the option that run only if the build is successful.


Steps to be followed for creating a build pipeline view

 - Click on the + sign on the jenkins dashboard.

 - Give the view name and select Build Pipeline View.

 - Give the details of the pipeline like which project to be executed first.

 - Save these details a pipeline view will be created


## Creating a Jenkins agent for remote deployment

- Click on “Manage Jenkins” in the dashboard sidebar.
- Click on “Manage Nodes”.
- Click on “New Node” in the sidebar.
- Enter the name of the node in the Node name section.
- Select “permanent agent” option -> Click OK.
- Optional: Give the description of the node.
- Enter the “Remote Root Directory”.
- In “Launch Method” select: Launch slave agents via SSH.
- In host: specify the IP address of the host on which you want to deploy the agent.


## Creating Allure report in Jenkins

It is a test report tool that is designed to create test execution reports that are clear to everyone.

## Installing allure plugin

Go to ‘Manage jenkins’ -> ‘Manage plugins’ - > ‘Available’ tab
Search ‘Allure jenkins plugin’ and install it without restart.  

## Generate allure report for Collaboration System

 1.  Create  a free style project on Jenkins
 2. In the post build action add Allure report.
 3. Create a directory in the workspace ie allurerequire and paste  the following in requirements.txt of creating allure report.

              arrow==0.8.0
              colorama==0.3.7
              enum34==1.1.6
              lxml==3.6.0
              moment==0.5.1
              namedlist==1.7
              py==1.4.31
              pytest==2.7.3
              pytest-allure-adaptor==1.7.7
              pytest-gitignore==1.3
              python-dateutil==2.5.3
              pytz==2016.4
              selenium==2.53.5
              six==1.10.0
              times==0.7


3. In the execute shell of build action add these lines

           sudo apt-get -y install libxml2-dev libxslt-dev
           pip install -r allurerequire/requirements.txt
           mkdir -p ./allure-results
           export DJANGO_SETTINGS_MODULE=CollaborationSystem.settings
           python3 -m pip install pytest pytest-allure-adaptor
           python3 -m pytest --alluredir=./allure-results Group/tests.py Community/tests.py   BasicArticle/tests.py

4.  Save and Build the project.

5.   Click on the Allure report  to see the reports created.
