# Isaac Sim Devcontainer

This repository contains the development container configuration for Isaac Sim.

## Features

- Pre-configured environment for Isaac Sim development.
- Includes all necessary dependencies and tools.
- Easy to set up and use.


## Getting Started

To get started with the development container, follow these steps:

1. Make sure you have installed NVIDIA Driver running `nvidia-smi`. If not Install it;
    ```bash
    sudo apt-get update
    sudo apt install build-essential -y
    wget https://us.download.nvidia.com/XFree86/Linux-x86_64/535.129.03/NVIDIA-Linux-x86_64-535.129.03.run
    chmod +x NVIDIA-Linux-x86_64-535.129.03.run
    sudo ./NVIDIA-Linux-x86_64-535.129.03.run
    ```

2. **Install Docker**: Ensure you have Docker installed on your machine. You can install as following:
    ```bash
    # Docker installation using the convenience script
    curl -fsSL https://get.docker.com -o get-docker.sh
    sudo sh get-docker.sh

    # Post-install steps for Docker
    sudo groupadd docker
    sudo usermod -aG docker $USER
    newgrp docker

    # Verify Docker
    docker run hello-world
    ```

3. Install NVIDIA Docker Toolkit:
    ```bash
    # Configure the repository
    curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg \
    && curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list | \
        sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
        sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list \
    && \
        sudo apt-get update

    # Install the NVIDIA Container Toolkit packages
    sudo apt-get install -y nvidia-container-toolkit
    sudo systemctl restart docker

    # Configure the container runtime
    sudo nvidia-ctk runtime configure --runtime=docker
    sudo systemctl restart docker

    # Verify NVIDIA Container Toolkit
    docker run --rm --runtime=nvidia --gpus all ubuntu nvidia-smi
    ```

3. **Pull the Isaac Sim Docker Image**:

    To pull the Isaac Sim Docker image, you need to authenticate with the NVIDIA container registry. Follow these steps:

    To authenticate with the NVIDIA container registry (nvcr.io) and obtain the necessary credentials, follow these steps:

    - **Sign into NGC**:
        - Go to the [NGC Sign In page](https://ngc.nvidia.com/signin).
        - Enter your NVIDIA account credentials to sign in. If you don't have an account, you will need to create one.

    - **Generate an API Key**:
        - Once signed in, navigate to the **Setup** page by clicking on your profile icon in the top right corner and selecting **API Key**.
        - Click on **Generate API Key**. This key will be used as your password for Docker login.

    - **Use the API Key for Docker Login**:
        - Open your terminal and run the following command:
            ```sh
            docker login nvcr.io
            ```
        - When prompted for a username, use your NGC email address.
        - When prompted for a password, use the API key you generated.

    - **pull the Isaac Sim Docker image**: After successfully logging in, you can pull the Isaac Sim Docker image as described in the README:
        ```sh
        docker pull nvcr.io/nvidia/isaac-sim:4.2.0
        ```

4. **Clone the Repository**:
    ```sh
    git clone https://github.com/NDHANA94/isaac_sim_devcontainer.git
    cd isaac_sim_devcontainer/
    ```
5. **Open in VS Code**: 

    - Open Visual Studio Code. 
    - Install the **Remote - Containers** extension from the Extensions view (if not already installed).
    - Open the cloned repository folder in VS Code.
    - You should see a prompt to reopen the folder in a container. Click on "Reopen in Container".
    - If you don't see the prompt, you can manually open the folder in a container by following these steps:
        - Press `F1` to open the Command Palette.
        - Type `Remote-Containers: Reopen in Container` and select it.
        - VS Code will then reopen the folder inside the development container.

6. **Build the Container**: The container will start building automatically. This might take a few minutes.








