---
title: "Accessing the VM with SSH"
teaching: 10
exercises: 0
questions:
- "How do I connect to my Azure VM?"

objectives:
- "Establish an SSH connection to the Azure VM using PuTTY."
- "Configure PuTTY to establish tunnels for VNC, and Jupyter connections"

keypoints:
- "Once connected, you will have command-line access to the VM, allowing you to execute commands and perform administrative tasks remotely."
---

## Accessing the VM with SSH

You can use any SSH client to connect to your VM. Here, we provide the steps using PuTTY for Windows and Linux operating systems.

### For Linux
1. Open a terminal on your Linux machine and navigate to the path of the .pem file you downloaded from Azure before.
2. Set the correct permissions for the pem file by running the following command:

```
chmod 600 ubuntu_key.pem
````

3. Execute the following command:

```
ssh -i ubuntu_key.pem -L 5901:localhost:5901 -L 6080:localhost:6080 -L 8888:localhost:8888 azureuser@<AZURE_VM_IP>
```

### For Windows

#### Installation of PuTTY

1. Download the latest version of PuTTY from the official website: [PuTTY](https://www.putty.org/)

2. Open `PuTTYgen` and select the `Conversions` option. 
3. Then, choose `Import key` to locate and select the `.pem` file you downloaded previously from Azure. 

> Note: Do not select `Generate`.
{: .testimonial}

4. Go to the `File` menu, select `Save private key`, and confirm by clicking `Yes` in the pop-up window.

5. Save the new file as `Any_name_you_want.ppk` to your computer.

6. Close the PuTTYgen window.

#### Configuration of PuTTY

1. Open PuTTY and navigate to the left part of the PuTTY window. Select **Category > Session** and fill in the following values:

    - **Host Name (or IP address):** `Azure_VM_IP`
    - **Port:** `22`

2. In the left part of the PuTTY window, select **Category > Connection > SSH > Auth**. Under `Private key file for authentication`, click on `Browse` and load the `.ppk` file created earlier.

3. For VNC connections, navigate to **Category > Connection > SSH > Tunnel**.

    - To add the VNC tunnel, set **Source Port** to `5901`, **Destination** to `localhost:5901`, and click the **Add** button.
    - To add the WebVNC tunnel, set **Source Port** to `6080`, **Destination** to `localhost:6080`, and click the **Add** button.
    - To add the Jupyter tunnel, set **Source Port** to `8888`, **Destination** to `localhost:8888`, and click the **Add** button.


> Note: Tunnels will be required later. They will allow you to easily connect to VNC or Jupyter when the corresponding container is launched.
{: .testimonial}

4. After defining the above tunnels, save the SSH connection settings and establish the connection by clicking the `Open` button. In the pop-up window, select `Accept` and enter the VM credentials (by default, `azureuser`).

Congratulations! You now have remote access to your VM created in Azure.

{% include links.md %}
