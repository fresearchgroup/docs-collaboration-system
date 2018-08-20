---
id: etherpadDevDocker
title: Etherpad, Real-time collaborative editing
sidebar_label: Etherpad
---

## Download Etherpad
```shell
cd        
wget https://github.com/ether/etherpad-lite/archive/1.7.0.tar.gz
tar -xvf 1.7.0.tar.gz
mv etherpad-lite-1.7.0/ etherpad-lite/
```

## Copy Required files of Etherpad to the repository
```shell
cd etherpad-lite/
sudo cp -r * ../Community-Content-Tools/etherpad-lite/
```

## Build and Run
```shell
cd         
cd Community-Content-Tools/etherpad-lite/        
sudo docker build -t etherpadlite .        
sudo docker run -p 9001:9001 etherpadlite   
```
