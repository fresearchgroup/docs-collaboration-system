---
id: checkDevDocker
title: Check and Test the system
sidebar_label: Check and Test
---

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
