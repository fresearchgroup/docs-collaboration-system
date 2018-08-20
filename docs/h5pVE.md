---
id: h5pVE
title: H5P (Interactive Content)
sidebar_label: H5P
---

H5P is a HTML5 tool for creating interactive contents which is integrated with Collaborative Communities. Follow the steps given below to set it up.


## Clone repository
```shell
git clone https://github.com/Content-Tools-Team/H5P.git
```

## Setup virtual environment
Create and activate virtual environment, with python 2.7 , django 1.8
```shell
virtualenv venv --python=python2.7 
source venv/bin/activate
```

## Install requirements and H5P Plugin
```shell
pip install -r requirements.txt
pip install H5PP-0.1.9.tar.gz
```

## Install mysql and configure the database
```shell
pip install mysql
sudo apt-get install mysql-server
sudo apt-get install libmysqlclient-dev
python sql_reset.py
```

## Create a superuser
```shell
python manage.py createsuperuser
```

## Run the server
```shell
python manage.py runserver  <IP_Address>:8000
```

## Install libraries
- Go to https://h5p.org/sites/default/files/official-h5p-release-20170301.h5p and download the official h5p libraries.
- Go to http://localhost:8000/h5p/home and upload the libraries.