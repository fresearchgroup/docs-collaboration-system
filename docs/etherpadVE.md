---
id: etherpadVE
title: Etherpad, Real-time collaborative editing
sidebar_label: Etherpad
---

Etherpad is a real-time collaboarative editor which is used in Collaboration system. Follow the steps given below to set it up.

## Clone the repository
```shell
git clone https://github.com/fresearchgroup/Community-Content-Tools.git        
```
## Download Etherpad and copy the required files
```shell
cd        
wget https://github.com/ether/etherpad-lite/archive/1.7.0.tar.gz
tar -xvf 1.7.0.tar.gz
mv etherpad-lite-1.7.0/ etherpad-lite/
cd etherpad-lite/
sudo cp -r * ../Community-Content-Tools/etherpad-lite/
```

## Install Node JS 8
Download and install Node JS 8 from https://nodejs.org/

## Run
```shell
cd
cd Community-Content-Tools/etherpad-lite
./bin/run.sh
```

## API Key
Note the API Key. It is needed while configuring Collaboration System.
```shell
cd
cd Community-Content-Tools/etherpad-lite
cat APIKEY.txt
```
