---
title: "Cleaning up"
teaching: 5
exercises: 5
questions:
- "How do I delete containers and associated data from my Azure VM?"

objectives:
- "Delete containers created created on Azure"
- "Perform a validation test to ensure that the installation of CMSSW, ROOT, and Python containers is successful."

keypoints:
- "Containers will permanently remove the data stored inside them. Therefore, it is recommended to back up any important data before executing these commands."
---
## Deleting Docker Containers

To delete the Docker containers and associated data, you can use the following commands:

### CMSSW
```
sudo docker rm my_od
sudo rm -rf cms_open_data_work
```
### ROOT
```
sudo docker rm my_root
sudo rm -rf cms_open_data_root
```
### PYTHON
```
sudo docker rm my_python
sudo rm -rf cms_open_data_python
```

Running these commands will remove the respective docker containers from your system. Additionally, it will delete the corresponding directories (cms_open_data_work, cms_open_data_root, cms_open_data_python) containing the data associated with each container.

> Please note that deleting the containers will permanently remove the data stored inside them. Make sure to back up any important data before executing these commands.

## Validation Test
To validate the installation and ensure that everything is working fine, you can perform a validation test. Follow the steps of this [test page](https://cms-opendata-workshop.github.io/workshop2022-lesson-docker/04-validation/index.html).

  > Note: This page provides instructions on how to test the functionality of CMSSW, ROOT, and Python within the docker containers.

   
## Stoping a Virtual Machine on Microsoft Azure
If you intend to reuse the created VM in the future, it is recommended to stop the VM. Stopping a VM in Azure may be advisable to prevent the consumption of your free credit or to avoid incurring additional costs.

To stop a virtual machine on Microsoft Azure, follow these steps:

1. Shut down the VM from the Ubuntu shell.
2. Go to the `Home` page in the Azure portal.
3. Click on the `Virtual machines` icon.
4. The list of created VMs will be displayed.
5. Select the VM you wish to stop and choose the `Stop` option at the top.
6. A confirmation message will appear: "Do you want to stop all the selected virtual machines?" Select the `Yes` option.
7. The stopping process may take a few seconds.
9. Once completed, you will find a notification at the top indicating: **"Executed stop command on 1 selected items. Succeeded: 1, Failed: 0, Canceled: 0."**

## Deleting a Virtual Machine on Microsoft Azure

If you do not intend to reuse the created VM in the future, it is recommended to delete the VM. Deleting a VM in Azure may be advisable to prevent the consumption of your free credit or to avoid incurring additional costs.

To delete a virtual machine and its associated resources on Microsoft Azure, follow these steps:

1. Go to the `Home` page in the Azure portal.
2. Click on the `Virtual machines` icon.
3. The list of created VMs will be displayed.
4. Check the VM you want to delete and select the `Delete` option at the top.
5. You will receive a confirmation message: "Do you want to delete all the selected virtual machines?" Type "`yes`" in the `Confirm delete` box.
6. The deletion process may take a few seconds.
8. Once completed, the VM should no longer be visible in the `virtual machines` list.
