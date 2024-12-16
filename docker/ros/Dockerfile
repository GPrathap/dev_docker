FROM osrf/ros:melodic-desktop-full

ARG ROS_DISTRO=melodic
ARG user_id=1000
ARG ros_ws=/home/developer/dev_ws

ENV DEBIAN_FRONTEND=noninteractive
ENV NVIDIA_VISIBLE_DEVICES \
    ${NVIDIA_VISIBLE_DEVICES:-all}
ENV NVIDIA_DRIVER_CAPABILITIES \
    ${NVIDIA_DRIVER_CAPABILITIES:-all}

# Install packages.
RUN apt-get update && apt-get install -y \
    ros-${ROS_DISTRO}-gazebo-* \
    nano tmux \
    less python3-pip net-tools \
    xterm locate
    # ros-${ROS_DISTRO}-navigation2 ros-${ROS_DISTRO}-nav2-* ros-${ROS_DISTRO}-gazebo-ros-pkgs \ 
    # ros-${ROS_DISTRO}-turtlebot3-gazebo ros-${ROS_DISTRO}-nav2-costmap-2d ros-${ROS_DISTRO}-nav2-* \
    # ros-${ROS_DISTRO}-robot-localization ros-${ROS_DISTRO}-octomap* ros-${ROS_DISTRO}-tf2-tools locate ros-${ROS_DISTRO}-nav2_*
#    && rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install -y --no-install-recommends \
      libglvnd0 \
      libgl1 \
      libglx0 \
      libegl1 \
      libgles2 && \
    rm -rf /var/lib/apt/lists/*

RUN apt-get update -y && apt install python-rosdep python-rosinstall python-rosinstall-generator python-wstool build-essential python-catkin-tools -y 


# RUN apt-get install -y ros-${ROS_DISTRO}-interactive* ros-${ROS_DISTRO}-twist*
# Add a user with the same user_id as the user on the host
ENV USER=developer
RUN useradd -ms /bin/bash $USER \
 && echo "$USER:$USER" | chpasswd \
 && adduser $USER sudo \
 && echo "$USER ALL=NOPASSWD: ALL" >> /etc/sudoers.d/$USER

RUN mkdir -p ${ros_ws}/src/
# Commands below run as the developer user
USER $USER


# Working directory
WORKDIR /home/developer

# ENVs
ENV HOME=/home/developer
ENV PATH="/home/developer/.local/bin:${PATH}"

# Force Python stdout and stderr streams to be unbuffered.
ENV PYTHONUNBUFFERED 1

# Add sourcing to your shell startup script
# https://docs.ros.org/en/galactic/Tutorials/Configuring-ROS2-Environment.html#add-sourcing-to-your-shell-startup-script
RUN echo "source /opt/ros/${ROS_DISTRO}/setup.bash" >> ~/.bashrc
RUN echo "source ${ros_ws}/devel/setup.bash" >> ~/.bashrc

# RUN  echo "export USER=$USER" >> ~/.bashrc
# This entrypoint is from base image.
# See https://github.com/osrf/docker_images/blob/master/ros/galactic/ubuntu/focal/ros-core/ros_entrypoint.sh
ENTRYPOINT ["/ros_entrypoint.sh"]

CMD ["sleep", "infinity"]
