# Isaac Sim Devcontainer

This repository contains the development container configuration for Isaac Sim.

## Features

- Pre-configured environment for Isaac Sim development.
- Includes all necessary dependencies and tools including ROS2-Humble.
- Volume mounted `/workspace` directory for your local development files.
- Easy to set up and use.


## Getting Started

To get started with the development container, follow these steps:

1. **Install NVIDIA Driver:** Make sure you have installed NVIDIA Driver running `nvidia-smi`. If not Install it;
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

3. **Install NVIDIA Docker Toolkit:**
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

4. **Pull the Isaac Sim Docker Image**:

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

5. **Clone the Repository**:
    ```sh
    git clone https://github.com/NDHANA94/isaac_sim_devcontainer.git
    cd isaac_sim_devcontainer/
    ```

6. **Setup `as.desktop` to grant access to local Docker container for GUI aaplications:**
    You can simply run `xhost +local:docker` or setup the desktop icon provided to grant access to container to use host display for GUI as following.
    - Copy and past `dsa.desktop` desktop icon to your Desktop.
    - Right click on it and then click on `Allow Launching`.
    - Now double clicking on this icon you can grant access to local container to run GUI applications on host display.
7. **Open in VS Code**: 

    - Open Visual Studio Code. 
    - Install the **Remote - Containers** extension from the Extensions view (if not already installed).
    - Open the cloned repository folder in VS Code.
    - You should see a prompt to reopen the folder in a container. Click on "Reopen in Container".
    - If you don't see the prompt, you can manually open the folder in a container by following these steps:
        - Press `F1` to open the Command Palette.
        - Type `Remote-Containers: Reopen in Container` and select it.
        - VS Code will then reopen the folder inside the development container.

8. **Build the Container**: The container will start building automatically. This might take a few minutes.


</br></br>


## Executable Files in the `/isaac_sim` Directory:

The `/isaac_sim` directory in the Docker container contains several executable scripts that help you manage, configure, and run Isaac Sim in various modes. Here is a brief overview of these scripts and how to use them:

### Overview of Executable Scripts

- **`clear_caches.sh`**: Clears caches used by Isaac Sim to free up space and ensure fresh data.
  

- **`isaac-sim.docker.gui.sh`**: Runs Isaac Sim with a graphical user interface (GUI) in a Docker container.
  

- **`isaac-sim.docker.sh`**: Runs Isaac Sim in a Docker container without a GUI.


- **`isaac-sim.fabric.sh`**: Related to Isaac Sim fabric, which may involve fabric simulation or configuration.


- **`isaac-sim.headless.native.sh`**: Runs Isaac Sim in headless mode natively on the host machine without a GUI.


- **`isaac-sim.headless.webrtc.sh`**: Runs Isaac Sim in headless mode with WebRTC support for remote visualization.


- **`isaac-sim.selector.sh`**: Selects and runs different configurations of Isaac Sim.
 

- **`isaac-sim.sh`**: Main script to run Isaac Sim. This is typically the entry point for starting the simulation.


- **`jupyter_notebook.sh`**: Starts a Jupyter Notebook server, useful for running Python notebooks with Isaac Sim.


- **`omni.isaac.sim.post.install.run.sh`**: Runs post-installation tasks for Isaac Sim, ensuring everything is set up correctly.


- **`omni.isaac.sim.post.install.sh`**: Post-installation script for Isaac Sim, typically run once after installation.


- **`omni.isaac.sim.warmup.sh`**: Warms up Isaac Sim, possibly by preloading assets or initializing systems.


- **`privacy.sh`**: Related to privacy settings, possibly for configuring data collection preferences.


- **`pull_kit_sdk.sh`**: Pulls the Kit SDK, which may be required for certain development tasks.


- **`python.sh`**: Runs Python with the Isaac Sim environment, ensuring all necessary dependencies are loaded.


- **`run_all_benchmarks.sh`**: Runs all benchmarks for Isaac Sim, useful for performance testing.


- **`run_all_tests.sh`**: Runs all tests for Isaac Sim, ensuring the system is functioning correctly.


- **`runapp.sh`**: Runs an Isaac Sim application, possibly a specific simulation or demo.


- **`runheadless.native.sh`**: Runs Isaac Sim in headless mode natively on the host machine without a GUI.


- **`runheadless.webrtc.sh`**: Runs Isaac Sim in headless mode with WebRTC support for remote visualization.


- **`setup_conda_env.sh`**: Sets up a Conda environment for Isaac Sim, useful for managing dependencies.


- **`setup_python_env.sh`**: Sets up the Python environment for Isaac Sim, ensuring all necessary packages are installed.

</br>

### How to Use These Scripts

1. **Access the Container**:
   - Open the Docker container in VS Code or through the terminal.

2. **Navigate to the `/isaac_sim` Directory**:
   ```sh
   cd /isaac_sim
   ```

3. **Run the Desired Script**:
   - Make sure the script has execute permissions:
     ```sh
     chmod +x <script_name>.sh
     ```
   - Execute the script:
     ```sh
     ./<script_name>.sh
     ```

</br></br>


## `/workspace` Directory with Volume mounted:
`/workspace` directory is used as a volume mount point for your local development files. This allows you to work on your projects locally and have the changes reflected inside the container. Here’s how you can use it:









