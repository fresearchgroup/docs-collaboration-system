---
id: h5pDevDocker
title: H5P (Interactive Content)
sidebar_label: H5P
---

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
