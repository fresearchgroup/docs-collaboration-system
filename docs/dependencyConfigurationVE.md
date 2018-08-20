---
id: dependencyConfigurationVE
title: Set Environment Variables in Collaboration System
sidebar_label: Dependency Configurations
---

In these steps, the .env file will be edited for configuring the dependencies, installed earlier. If any dependency is not installed then comment the appropriate lines in the .env file.s

## H5P       
- Edit .env file. COLLAB_ROOT should have the IP address of Collaboration system and port number 7000. H5P_ROOT should have the IP address of H5P server and port 8000. It should look something like given below.
```shell
COLLAB_ROOT=http://<IP-Address>:7000/
H5P_ROOT=http://<IP-Address>:8000/
```

## Etherpad
- Edit .env file. APIKEY is the key noted while installing and running 'Etherpad'. NODESERVERURL should have the IP address of Etherpad (node). NODESERVERPORT should have port 9001.
```shell
APIKEY=558ae5e3155785040488b6f3e27281a6db0e7d4a411ac49bae84....
NODESERVERURL=http://<IP-Address>
NODESERVERPORT=9001
```

## Event logs       

### Generate Token
```shell
cd CollaborationSystem 
python3 manage.py generateToken --n
```

### Edit .env file for variables and token
- Copy the generated token and place in EVENT_API_TOKEN variable. It should look something like given below.
```shell
EVENTAPI_TOKEN_USERNAME=eventloguser
EVENTAPI_TOKEN_PASSWORD=eventlogpass
EVENT_API_TOKEN=268929a10c2c73e06ebd496c224156f4b191614b
ELASTICSEARCH_ADDRESS=elasticsearch
```
