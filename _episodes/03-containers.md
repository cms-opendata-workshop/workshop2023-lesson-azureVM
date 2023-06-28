---
title: "Containers"
teaching: 10
exercises: 10
questions:
- "What is the purpose of installing Docker in the Azure VM?"
- "How can you access the graphical user interface of the CMSSW container?"
- "What is the recommended method for validating the successful installation of CMSSW, ROOT, and Python containers?"

objectives:
- "Installation process of Docker on your Ubuntu VM created on Azure"
- "Perform a validation test to ensure that the installation of CMSSW, ROOT, and Python containers is successful."

keypoints:
- "Installing Docker and the necessary containers (CMSSW, ROOT, Python) enables you to easily set up and utilize a containerized environment for efficient data analysis and exploration in the Azure VM."
---

## Installation of Containers
In this section, we will guide you through the installation process for Docker and the CMSSW, ROOT, and Python containers.

> Docker is a container platform that enables packaging applications with their dependencies to facilitate quick and consistent deployment and execution across different environments.

### Docker Installation

To install Docker on your Ubuntu system, you can follow the steps outlined below. You can also refer to the [Official Docker Documentation](https://docs.docker.com/engine/install/ubuntu/#set-up-the-repository) for a detailed guide.

1. Update the apt package index and install packages to allow apt to use a repository over HTTPS:

    ```
    sudo apt-get update
    sudo apt-get install ca-certificates curl gnupg -y
    ```

2. Add Docker’s official GPG key:

    ```bash
    sudo install -m 0755 -d /etc/apt/keyrings
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    sudo chmod a+r /etc/apt/keyrings/docker.gpg
    ```

3. Use the following command to set up the repository:

    ```bash
    echo "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] \
    https://download.docker.com/linux/ubuntu "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
    sudo tee /etc/apt/sources.list.d/docker.list
    ```

4. Update the apt package index:

    ```bash
    sudo apt-get update
    ```

5. Install Docker Engine, containerd, and Docker Compose. To install the latest version, run:

    ```bash
    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
    ```
6. Execute the next commands for adding the user to the "docker" group and starting a new shell session with the "docker" group as the primary group, the user will gain the necessary permissions to interact with Docker without requiring root privileges. 

    ```bash
    sudo groupadd docker
    sudo usermod -aG docker $USER
    newgrp docker
    ```

6. Verify that the Docker Engine installation is successful by running the hello-world image:

    ```bash
    docker run hello-world
    ```

    >  You should be able to view these lines:
    
    >  Hello from Docker!
    
    > This message shows that your installation appears to be working correctly.
    
### Start Containers from CMS Open Data Container Images

To get access to CMS software (CMSSW) and ROOT Python tools for open data analysis, you can follow the steps outlined below. 

### CMSSW

> For detailed information about CMSSW, you can refer to the documentation [CMS Open Data Guide](https://cms-opendata-guide.web.cern.ch/cmssw/cmsswanalyzers/).

1. Download the docker image for CMS open data and start a container:

    ```bash
    cd
    mkdir cms_open_data_work
    docker run -it --name my_od -P -p 5901:5901 -p 6080:6080 -v \
    ${HOME}/cms_open_data_work:/code cmsopendata/cmssw_7_6_7-slc6_amd64_gcc493 \
    /bin/bash
    ```
    
2. Once you are inside the container, you can start the VNC service to access the graphical user interface. Run the following command to start VNC:

    ```bash
    start_vnc
    ```

    > After starting VNC, you can access the VNC service in two ways:
    > 1. VNC Client: Use a VNC client and connect to localhost:1 to access the graphical interface.
    > 2. Web Browser: Access the VNC service in your web browser by navigating to http://localhost:6080/vnc.html. `Password:` **cms.cern**

3. To stop the VNC service and exit the container, run :

    ```
    stop_vnc
    exit
    ```

With the CMSSW container running, you can now proceed with analyzing the open data from CMS using the CMSSW software.

### ROOT 

To start a container with ROOT installed, you can follow the steps outlined below.

1. Download the docker images for ROOT and start the container:

    ```bash
    cd
    mkdir cms_open_data_root
    docker run -it --name my_root --net=host --env="DISPLAY" \
    -v $HOME/.Xauthority:/home/cmsusr/.Xauthority:rw \
    -v ${HOME}/cms_open_data_root:/code \
    gitlab-registry.cern.ch/cms-cloud/root-vnc:latest
    ```

2. To start VNC inside the container:

    ```bash
    start_vnc
    ```
    
    > After starting VNC, you can access the VNC service in two ways:
    > 1. VNC Client: Use a VNC client and connect to localhost:1 to access the graphical interface.
    > 2. Web Browser: Access the VNC service in your web browser by navigating to http://localhost:6080/vnc.html. `Password:` **cms.cern**

3. To stop VNC and exit:

    ```bash
    stop_vnc
    exit
    ```

### Python Tools 

To start a container with Python tools installed, you can follow the steps outlined below.

1. Download and install Python tools container:
    ```bash 
    cd
    mkdir cms_open_data_python
    docker run -it --name my_python -P -p 8888:8888 --net=host \
    --env="DISPLAY" -v $HOME/.Xauthority:/home/cmsusr/.Xauthority:rw \
    -v ${HOME}/cms_open_data_python:/code \
    gitlab-registry.cern.ch/cms-cloud/python-vnc:latest
    ```

    This will download and install the necessary container for Python tools.

2. To start Jupyter (notebook server) inside the container, run the following command:

    ```bash
    jupyter-lab --ip=0.0.0.0 --no-browser
    ```

    > When you start a notebook server with token authentication enabled (default), a token is generated for authentication. 
    > The token information is logged to the terminal, allowing you to copy and paste the URL into your web browser. 
    > Here is an example of the logged token:
    > "The Jupyter Notebook is running at: http://localhost:8888/?token=c8de56fa4deed24899803e93c227592aef6538f93025fe01"
    > Jupyter can be accessed in your web browser by navigating to that link.

3. To stop the Jupyter server, since it takes over the shell, press `CTRL + C` and type **y** when prompted with the message **Shutdown this Jupyter server (y/[n])?**.
4. To exit the container, run the following command:

    ```bash
    exit
    ```
> Please note that the commands provided for CMSSW, ROOT, and Python Tools containers are a summary of the process. For more detailed instructions and additional configurations, refer to the [Docker pre-exercise](https://cms-opendata-workshop.github.io/workshop2023-lesson-docker/03-docker-for-cms-opendata/index.html).

## Returning to the Same Container

If you need to return to a previously used container, you can do so using the docker start command:

```bash
docker start -i my_od
docker start -i my_root
docker start -i my_python
```

By running these commands, you can resume your work in the desired container. The -i flag ensures that you can interact with the container's terminal. Remember to use the appropriate container name (my_od, my_root, or my_python) based on the container you want to start. With these commands, you can easily return to the same container and continue your work without any loss of progress or data.

> Note: Make sure that the containers are not already running before using the docker start command.
{: .testimonial}
  

{% include links.md %}
