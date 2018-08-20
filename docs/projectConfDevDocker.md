---
id: projectConfDevDocker
title: Set Environment Variables in Collaboration System
sidebar_label: Configurations
---

## Event logs       
### Generate Token
```shell
cd        
sudo docker-compose up        
sudo docker exec -i collaboration-system_web_1 python3 manage.py generateToken --n
```
### Edit .env.docker file for variables and token
- Copy the generated token and place in EVENT_API_TOKEN variable. It should look something like given below.
```shell
EVENTAPI_TOKEN_USERNAME=eventloguser
EVENTAPI_TOKEN_PASSWORD=eventlogpass
EVENT_API_TOKEN=268929a10c2c73e06ebd496c224156f4b191614b
ELASTICSEARCH_ADDRESS=elasticsearch
```

## H5P       
- Edit .env.docker file. COLLAB_ROOT should have the IP address of Collaboration system and port number 7000. H5P_ROOT should have the IP address of H5P server and port 8000. It should look something like given below.
```shell
COLLAB_ROOT=http://<IP-Address>:7000/
H5P_ROOT=http://<IP-Address>:8000/
```

## Etherpad
### Get API Key for Etherpad
- Execute the following command to get the API key for Etherpad. We will need this while setting environment variables in Collaboration system.
```shell
sudo docker exec -i collaboration-system_node_1 cat APIKEY.txt
```

### Edit .env.docker file
- APIKEY is nothing but what was generated above. NODESERVERURL should have the IP address of Etherpad (node). NODESERVERPORT should have port 9001.
```shell
APIKEY=558ae5e3155785040488b6f3e27281a6db0e7d4a411ac49bae84....
NODESERVERURL=http://<IP-Address>
NODESERVERPORT=9001
```

## Recommendation
- Edit .env.docker file. RecommendationIP should have the IP address of Recommendation system and RecommendationPort should have port 3445. It should look something like given below.
```shell
RecommendationIP=<IP-Address>
RecommendationPort=3445
```
