---
title: "Cleaning up"
teaching: 10
exercises: 0
questions:
- "How do I delete containers and associated data from my Azure VM?"

objectives:
- "Delete containers created created on Azure"
- "Perform a validation test to ensure that the installation of CMSSW, ROOT, and Python containers is successful."

## Deleting Docker Containers

To delete the Docker containers and associated data, you can use the following commands:

##### CMSSW
```
sudo docker rm my_od
sudo rm -rf cms_open_data_work
```
##### ROOT
```
sudo docker rm my_root
sudo rm -rf cms_open_data_root
```
##### PYTHON
```
sudo docker rm my_python
sudo rm -rf cms_open_data_python
```

Running these commands will remove the respective docker containers from your system. Additionally, it will delete the corresponding directories (cms_open_data_work, cms_open_data_root, cms_open_data_python) containing the data associated with each container.

Please note that deleting the containers will permanently remove the data stored inside them. Make sure to back up any important data before executing these commands.

 
