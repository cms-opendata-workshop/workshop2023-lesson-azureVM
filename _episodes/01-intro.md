---
title: "Introduction"
teaching: 10
exercises: 5
questions:
- "How to create a VM over Microsoft Azure?"
- "How to install docker with the CMS open data software in a single virtual machine?"
objectives:
- "Create a single virtual machine on Microsoft Azure using the Ubuntu Server operating system."
- "Learn the process of installing Docker on the Ubuntu virtual machine."
- "Install the CMSSW, ROOT, and Python Docker images on the Ubuntu virtual machine."
- "Verify the successful installation of CMSSW, ROOT, and Python Docker images on the virtual machine."
keypoints:
- "Azure"
---

## Overview
In this hands-on exercise, you will learn how to use Microsoft Azure's cloud platform to create a virtual machine (VM) and harness the capabilities of containerization. 

You will install three essential container images on the VM:

1. **CMS software (CMSSW)**
2. **ROOT**
3. **Python tools**

The VM environment offers the added convenience of a graphical user interface accessible through Virtual Network Computing (VNC). With VNC, you can seamlessly access the graphical interface of the containerized applications directly in a browser window, making it effortless to interact with and visualize your data.

By the end of this exercise, you will have a fully functioning virtual machine on Microsoft Azure, equipped with the CMSSW, ROOT, and Python container images, all accessible through an intuitive browser-based graphical interface.

Let's dive in and explore the process of creating the VM, installing the container images, and utilizing the VNC interface to empower your data analysis and exploration.

## Creating a VM on Microsoft Azure

To begin, let's take advantage of Microsoft Azure's Azure for Students offering, which provides free access to the cloud. You can access the Azure for Students page by visiting [Azure Portal](https://azure.microsoft.com/en-us/free/students/) and signing in with your `academic account email`.

Upon accessing the link, click on the `Start Free` button. If this is your first time accessing Azure, you may be required to provide some personal information, but rest assured that credit card details should not be requested. Upon successful registration, you will be granted **100 USD credit** to get started.

> If you wish to use Azure with a non-academic account, you will receive a 200 USD credit to use within the first 30 days after signing up. However, it is important to note that you may be required to provide credit card details during the sign-up process. For more detailed information, you can access the documentation or resources available from [Azure free account FAQ ](https://azure.microsoft.com/en-us/free/free-account-faq/#F1)

Now, let's proceed with creating your VM. 
1. Click on `Deploy a virtual machine` and follow `Create a Linux virtual machine`.
2. Locate the **Ubuntu Server 20.04 LTS** image from the Azure Marketplace service. Select the `Create` option to proceed.
3. In the **Basic Data** tab, fill in the following mandatory details:
  - **Subscription:** Depends on your account `Azure for Students` or `Azure subscription`
  - **Resource group:** `(New) Resource Group`
  - **Virtual machine name:** `Choose any name you prefer`
  - **Region:** `Choose your preferred location`
  - **Image:** `Ubuntu Server 20.04 LTS - x64 Gen2`
  - **Size:** `Standard_B2ms - 2 vCPUs, 8 GiB memory`
  - **Type of authentication:** `Public key SSH`
  - **Username:** `azureuser`
  - **Key pairs name:** `Ubuntu_key`
  - **Public inbound ports:** `Allow selected ports`
  - **Select inbound ports:** `SSH (22)`
  
  `You can leave the remaining fields with their default values, as well as the other tabs.`

4. Once all the necessary information is provided, click on `Review + create` at the bottom of the page. You will be redirected to a summary of the selected options and the associated price (which should be within your student credits, approximately 0.0832 USD/hr).
5. After reviewing the details, click on `Create` to initiate the deployment process.
6. A pop-up message will appear, prompting you to generate a new key pair. Select the `Download private key and create resource` option. This action will initiate the download of a file named `<VMName>_key.pem`.
  > Please note that the deployment process may take some time.
7. Once the deployment is complete, Click on `Go to resource`. You will find information about your VM, including the public IP address. Make sure that your VM is in the **Running** status, and the `Start` icon (triangle) at the top left side of the page should be disabled.

##### Congratulations! You have successfully created your VM.
