---
id: configuration
title: Project Configuration
sidebar_label: Project Configuration
---

## Collaboration System initial configuration

Copy the patch file from 'temp' folder of the project to virtualenv Django -reversion compare module which has been installed in the virtual environment (collab) through requirements.txt.

```shell
$ sudo cp CollaborationSystem/temp/patch_for_reversion_compare.py collab/lib/python3.5/site-packages/reversion_compare/views.py

```


## Optional(if the database is empty or using a new database):

Run the following command inside CollaborationSystem project

```shell
$ python3 manage.py migrate
$ python3 manage.py loaddata workflow
$ python3 manage.py loaddata roles
$ python3 manage.py loaddata faq

```

After migrations are done and all the tables are created, changes the body column in Articles tables to make it multilingual , will take symbols, unicode character etc.
do --

```shell
mysql -u root -p #and select the database that was created and run the following sql query
ALTER TABLE BasicArticle_articles MODIFY COLUMN body text CHARACTER SET utf8 COLLATE utf8_general_ci NULL;

```

Create an initial forum and set the permissions, also set the site ids
Create a admin user --

```shell
$ python3 manage.py createsuperuser

```

Goto - http://ipaddress/admin/ and use your admin user and password.

Find - MACHINA: FORUM and select Forums.

- Create a Forum (Add Forum) --

- Forum type = Default Forum

- Name = Collaboration System

- Description = “The forum for ‘Collaborative Communities’ will allow individual users to discuss on  communities, topics related to communities, and thus, enhance its value for the society in terms of education.”

And save the forum.

Cick on GLOBAL FORUM PERMISSIONS

- Under Edit group permissions
- Click on the search button and select author
- And click on Select button
- Set GRANTED permission on following options
    - Can read forum
    - Can see forum
    - Can delete own posts
    - Can edit own posts
    - Can post announcements
    - Can post stickies
    - Can post without approval
    - Can reply to topics
    - Can start new topics
- Save the permissions

Add Sites--

	Goto - http://ipaddress/admin/

Find - SITES and select Sites

Add all ip addresses and domain names (one at a time).
Keep the Domain name  and Display name same.
