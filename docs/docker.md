---
id: docker
title: Docker
sidebar_label: Docker installation
---

## Install the system by creating Docker containers

Install Docker --

```
Docker - https://docs.docker.com/install/linux/docker-ce/ubuntu/#set-up-the-repository

Docker Compose -- https://docs.docker.com/compose/install/

```

## Steps for Docker --

1. Clone the repository --

      ```
      git clone https://github.com/fresearchgroup/Collaboration-System.git

      ```

2. The run the following commands inside the repository --

      Build the image --

      ```
       docker-compose build

      ```
      Run the database image --

      ```
       docker-compose up db

      ```

      To check the name of the database container image name type --

      ```
      docker-compose ps

      ```
      Upload the database dump to database container image created in the previous step.

      ```
       docker exec -i <container-image-name> mysql -u<username> -p<password> django < collab.sql

      ```

      Migrate the models to the database conatiner ---

      ```
      docker-compose run web python manage.py migrate

      ```

      Create a superuser(administrator) using --

      ```
      docker-compose run web python manage.py createsuperuser

      ```

      [optional if database dump is uploaed]

      Will load the initial data from json files --

      ```
      docker-compose run web python manage.py loaddata workflow roles faq

      ```

      Run the image--

      ```
      docker-compose up

      ```
