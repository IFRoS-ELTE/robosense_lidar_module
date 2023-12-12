# Use the ROS Noetic base image on Ubuntu Focal
FROM ros:noetic-ros-base-focal

# Set the ROS distribution environment variable
ENV ROS_DISTRO=noetic

# Set the ROS root directory
ENV ROS_ROOT=/opt/ros/${ROS_DISTRO}

# Install essential tools, libraries, and ROS dependencies
RUN apt-get update && apt-get install --no-install-recommends -y \
        build-essential \
        git \
        python3-catkin-tools \
        python3-pip \
        nano \
        curl \
        wget \
        libgl1-mesa-dev \
        libglu1-mesa-dev \
        x11-apps \
        ros-noetic-rviz \
        ros-noetic-rqt \
        ros-noetic-rqt-common-plugins \
        libyaml-cpp-dev \
        libpcap-dev \
    && apt-get clean \ 
    && rm -rf /var/lib/apt/lists/*

# Add the source setup.bash command to the user's bashrc
RUN echo "source /opt/ros/noetic/setup.bash" >> /root/.bashrc

# Uncomment and run rosdep update and rosdep install if needed
# RUN rosdep update && \
#     rosdep install

# Copy the ros_entrypoint.sh script from ros:ros-base
COPY ros_entrypoint.sh /
RUN chmod +x /ros_entrypoint.sh

# Set the ros_entrypoint.sh script as the entry point for the container
ENTRYPOINT ["/ros_entrypoint.sh"]

# Create a new workspace folder for ROS
RUN mkdir -p /root/ros_ws/src

# Set the new workspace folder as the working directory
WORKDIR /root/ros_ws
