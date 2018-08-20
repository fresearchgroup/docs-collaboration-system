---
id: startcollabDevDocker
title: Start Collaboration System
sidebar_label: Run Collaboration System
---

## Migrate and Start Collaboration System
```shell
cd        
cd Collaboration-System               
sudo docker exec -i collaboration-system_web_1 python3 manage.py migrate        
sudo docker-compose build        
sudo docker-compose up        
```