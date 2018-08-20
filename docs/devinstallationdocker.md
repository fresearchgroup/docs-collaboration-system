---
id: devinstallationdocker
title: Developer Installation Using Docker
sidebar_label: Initial Setup
---

The steps given below cater to installation and configuration of the following:
- Collaboration System
- Event logs: Logging of all events
- Etherpad: A real time editing tool
- H5P: HTML5 tool for creating interactive contents
- Recommendation System

## Install Prerequisites
- Docker - https://docs.docker.com/install/linux/docker-ce/ubuntu/#set-up-the-repository
- Docker Compose -- https://docs.docker.com/compose/install/
- Git -- sudo apt-get install git
- Update the system
- Make sure it is connected to the internet

## Clone the following Repositories
```shell
git clone https://github.com/fresearchgroup/Collaboration-System.git        
git clone https://github.com/fresearchgroup/Collaboration-System-Event-Logs.git        
git clone https://github.com/fresearchgroup/Community-Content-Tools.git        
git clone https://github.com/fresearchgroup/Community-Recommendation.git        
```

## Start the DB of Collaboration System
```shell
cd Collaboration-System        
git checkout develop        
sudo docker-compose build        
sudo docker-compose up db        
```