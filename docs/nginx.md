---
id: nginx
title: Nginx Configuration
sidebar_label: Nginx Configuration
---

## Web Server with Nginx and Gunicorn

Install the needed Packages

```shell
$ sudo apt-get install nginx python3-dev libmysqlclient-dev
$ sudo apt-get install python3-dev libmysqlclient-dev
$ sudo apt-get -y install supervisor
$ sudo systemctl enable supervisor
$ sudo systemctl start supervisor
$ sudo  apt-get install python3-pip
$ sudo pip3 install virtualenv
$ git clone https://github.com/fresearchgroup/Collaboration-System.git
$ sudo mv Collaboration-System CollaborationSystem
$ virtualenv collab -p python3
$ source collab/bin/activate
$ pip3 install -r CollaborationSystem/requirements.txt
$ django-admin --version      ( Check django version --  1.11.7)
$ pip3 install gunicorn
$ pip3 install psycopg2


```

Define Static URL in project.
Add the following line after STATIC_URL  (can be added anywhere in settings file)-

```shell
$ sudo nano CollaborationSystem/CollaborationSystem/settings.py
STATIC_ROOT = "/home/edx/static"

cd CollaborationSystem
$ python manage.py collectstatic
cd


```

## Configure Gunicorn -
Create a new file named gunicorn_start.bash inside /home/edx -

```shell
$ sudo nano gunicorn_start.bash
```
And add the following to that file

```
#!/bin/bash

NAME="CollaborationSystem"           # Name of the application
DJANGODIR=/home/edx/CollaborationSystem # Django project directory
SOCKFILE=/home/edx/run/gunicorn.sock     # we will communicte using this unix socket
USER=edx                                # the user to run as
GROUP=edx                               # the group to run as
NUM_WORKERS=3       # how many worker processes should Gunicorn spawn
DJANGO_SETTINGS_MODULE=CollaborationSystem.settings # which settings file should Django use
DJANGO_WSGI_MODULE=CollaborationSystem.wsgi  # WSGI module name
echo "Starting $NAME as `whoami`"

# Activate the virtual environment

cd $DJANGODIR
source /home/edx/collab/bin/activate
export DJANGO_SETTINGS_MODULE=$DJANGO_SETTINGS_MODULE
export PYTHONPATH=$DJANGODIR:$PYTHONPATH

# Create the run directory if it doesn't exist

RUNDIR=$(dirname $SOCKFILE)
test -d $RUNDIR || mkdir -p $RUNDIR

# Start your Django Unicorn
# Programs meant to be run under supervisor should not daemonize themselves (do not use --daemon)

exec gunicorn ${DJANGO_WSGI_MODULE}:application \
  --name $NAME \
  --workers $NUM_WORKERS \
  --user=$USER --group=$GROUP \
  --bind=unix:$SOCKFILE \
  --log-level=debug \
  --log-file=-

```

Start Gunicorn and execute

```shell
$ chmod u+x gunicorn_start.bash
$ mkdir run logs
$ touch logs/gunicorn.log
$ sudo nano /etc/supervisor/conf.d/edx.conf

```

Add the following to edx.conf -

```
[program:edx]
command = /home/edx/gunicorn_start.bash
user=root
autostart=true
autorestart=true
redirect_stderr=true
stdout_logfile=/home/edx/logs/gunicorn.log
environment=LANG=en_US.UTF-8,LC_ALL=en_US.UTF-8

```

Restart Services -

```shell
$ sudo systemctl restart supervisor
$ sudo systemctl enable supervisor
$ sudo supervisorctl status edx

```

Open the file gunicorn.service  -


```shell
$ sudo nano /etc/systemd/system/gunicorn.service

```
Add the folllowing -

```
[Unit]
Description=gunicorn daemon
After=network.target

[Service]
User=edx
Group=www-data
WorkingDirectory=/home/edx/CollaborationSystem
ExecStart=/home/edx/collab/bin/gunicorn --access-logfile - --workers 3 --bind unix:/home/edx/run/gunicorn.sock CollaborationSystem.wsgi:application

[Install]
WantedBy=multi-user.target

```

Start Gunicorn -

```shell
$ sudo systemctl start gunicorn
$ sudo systemctl enable gunicorn
$ sudo systemctl status gunicorn

```

Add the following to edx.conf file and change the server_name ip address

```shell
$ sudo nano /etc/nginx/sites-available/edx.conf

```
```
server {
    listen 80;
    server_name 10.129.26.188;  # here can also be the IP address of the server

    keepalive_timeout 5;
    proxy_connect_timeout 300s;
    proxy_read_timeout 300s;

    access_log /home/edx/logs/nginx-access.log;
    error_log /home/edx/logs/nginx-error.log;

    location /static/ {
       root /home/edx;
    }
   location /media/ {
       root /home/edx/CollaborationSystem;
    }
    location / {
        include proxy_params;
        proxy_pass http://unix:/home/edx/run/gunicorn.sock;
    }
}

```

Create symbolic link and restart-

```shell
$ sudo ln -s /etc/nginx/sites-available/edx.conf /etc/nginx/sites-enabled/edx.conf
$ sudo nginx -t
$ sudo systemctl restart nginx
$ sudo ufw allow 'Nginx Full'
$ sudo systemctl restart nginx
$ sudo supervisorctl restart edx
$ sudo service gunicorn restart
$ sudo service supervisor restart

```
Create a .env inside CollaborationSystem and paste the following -
```shell
$ sudo nano CollaborationSystem/.env
```
```
SECRET_KEY=myf0)*es+lr_3l0i5$4^)^fb&4rcf(m28zven+oxkd6!(6gr*6
DEBUG=True
DB_NAME=django
DB_USER=root
DB_PASSWORD=root
DB_HOST=localhost
DB_PORT=3306
ALLOWED_HOSTS= localhost, 10.129.132.103
GOOGLE_RECAPTCHA_SECRET_KEY=6Lfsk0MUAAAAAFdhF-dAY-iTEpWaaCFWAc1tkqjK
EMAIL_HOST=localhost
EMAIL_HOST_USER=
EMAIL_HOST_PASSWORD=
EMAIL_PORT=25
EMAIL_USE_TLS=False
DEFAULT_FROM_EMAIL=collaboratingcommunity@cse.iitb.ac.in
SOCIAL_AUTH_GOOGLE_OAUTH2_KEY=735919351499-ajre9us5dccvms36ilhrqb88ajv4ahl0.apps.googleusercontent.com
SOCIAL_AUTH_GOOGLE_OAUTH2_SECRET=I1v-sHbsogVc0jAw9M9Xy1eM
```
Note:Add all the ip addresses including the ip address of haproxy to ALLOWED_HOSTS in .env file and change the variables as per your needs.
