# Use the official Isaac Sim base image
FROM nvcr.io/nvidia/isaac-sim:4.2.0
# Set DEBIAN_FRONTEND to noninteractive to avoid prompts during package installation
ENV DEBIAN_FRONTEND=noninteractive
# Install ROS 2 Humble
RUN apt-get update && \
    apt-get install -y software-properties-common && \
    add-apt-repository universe && \
    apt-get update && \
    apt-get install -y curl gnupg2 lsb-release && \
    curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | apt-key add - && \
    sh -c 'echo "deb http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" > /etc/apt/sources.list.d/ros2-latest.list' && \
    apt-get update && \
    apt-get install -y ros-humble-desktop && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Source ROS 2 setup script
RUN echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc

# Set environment variables
ENV ROS_DISTRO humble
ENV ROS_VERSION 2

# Install additional ROS 2 dependencies if needed
RUN apt-get update && \
    apt-get install -y python3-rosdep python3-colcon-common-extensions && \
    rosdep init && \
    rosdep update && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install other necessary software pkgs
RUN apt-get update && \
    apt-get install -y python3-pip nano curl wget htop net-tools git  build-essential  gcc && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Set OMNI_KIT_ALLOW_ROOT to 1 to allow running the Omniverse Kit as root
ENV OMNI_KIT_ALLOW_ROOT=1

# Set ALSA_CARD to 0 to avoid audio issues
ENV ALSA_CARD=0

# Set the entrypoint
ENTRYPOINT ["/bin/bash"]