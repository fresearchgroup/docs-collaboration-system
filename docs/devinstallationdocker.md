---
id: devinstallationdocker
title: Developer Installation Using Docker
sidebar_label: Using Docker
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

## Load DB with H5P updates
```shell
sudo docker exec -i collaboration-system_db_1 mysql -uroot -proot django < collab-updated.sql
```

## Build H5P (Dependency)
```shell
sudo docker-compose up db                
cd ../Community-Content-Tools/H5P
```
- Edit the .env.docker file and change the IP address of COLLAB_ROOT and H5P_ROOT
```shell
COLLAB_ROOT=http://<IP-Address>:7000
H5P_ROOT=http://<IP-Address>:8000
```
- Build H5P image
```shell
sudo docker build -t h5p_image .        
```

## Build Etherpad (Dependency)
```shell
cd        
git clone https://github.com/ether/etherpad-lite        
cd etherpad-lite/
sudo cp -r * ../Community-Content-Tools/etherpad-lite/        
cd         
cd Community-Content-Tools/etherpad-lite/        
sudo docker build -t etherpadlite .        
sudo docker run -p 9001:9001 etherpadlite   
```

## Build ELK (Dependency)
```shell
cd        
cd Collaboration-System-Event-Logs/evelog-Docker
sudo docker-compose build        
sudo docker-compose up
```

## Build Recommendation (Dependency)
```shell
cd
cd Community-Recommendation/        
sudo docker-compose build        
sudo nano Dockerfile         
sudo docker-compose build        
sudo docker-compose up        
```

## Set Environment Variables in Collaboration System for Event logs       
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

## Set Environment Variables in Collaboration System for H5P       
- Edit .env.docker file. COLLAB_ROOT should have the IP address of Collaboration system and port number 7000. H5P_ROOT should have the IP address of H5P server and port 8000. It should look something like given below.
```shell
COLLAB_ROOT=http://<IP-Address>:7000/
H5P_ROOT=http://<IP-Address>:8000/
```

## Set Environment Variables in Collaboration System for Etherpad
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

## Set Environment Variables in Collaboration System for Recommendation
- Edit .env.docker file. RecommendationIP should have the IP address of Recommendation system and RecommendationPort should have port 3445. It should look something like given below.
```shell
RecommendationIP=<IP-Address>
RecommendationPort=3445
```

## Migrate and Start Collaboration System
```shell
cd        
cd Collaboration-System               
sudo docker exec -i collaboration-system_web_1 python3 manage.py migrate        
sudo docker-compose build        
sudo docker-compose up        
```

## Checking the Systems

### H5P
- Browse http://<IP-Address>:8000/h5p/. It should display H5P Django REST API.

### Load H5P Libraries
- Go to https://h5p.org/sites/default/files/official-h5p-release-20170301.h5p and download the official h5p libraries.
- Browse http://<IP-Address>:8000/h5p/libraries/ and upload the downloaded libraries and select proceed.

### Etherpad
- Browse http://<IP-Address>:9001/. It should display ‘New Pad’.

### ELK
- Browse http://<IP-Address>:5000/. It should display ‘ok’ message.
- Browse http://<IP-Address>:9200/. It should display some json file.
- Browse http://<IP-Address>:5601/. It should display kibana dashboard.
- Navigate to ‘Management’, ‘Index Pattern’, and in ‘Step 1 of 2: Define index pattern’, type ‘logs’ in the textbox. Proceed to Step 2. In Step 2 select ‘timestamp’ and click ‘Create index pattern’. You will now be able to get logs of every event that occurs on Collaboration system.

### Collaboration System
- Browse http://<IP-Address>:7000/. It should display the home page of Collaboration system. You are now ready to go ahead.

## Testing the System
```shell
cd        
cd Collaboration-System
python3 manage.py test
```
