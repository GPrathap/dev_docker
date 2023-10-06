FROM osrf/ros:humble-desktop-full-jammy

ARG ROS_DISTRO=humble
ARG user_id=1000
ARG ros_ws=/home/developer/dev_ws
ARG DOGTOOTH_REPO=/home/developer/dogtooth_ws/src/Dogtooth

ENV DEBIAN_FRONTEND=noninteractive

# Install packages.
RUN apt-get update && apt-get install -y \
    ros-${ROS_DISTRO}-gazebo-* \
    python-is-python3 \
    nano tmux \
    less python3-pip net-tools \
    xterm \
    ros-${ROS_DISTRO}-navigation2 ros-${ROS_DISTRO}-nav2-* ros-${ROS_DISTRO}-gazebo-ros-pkgs \ 
    ros-${ROS_DISTRO}-turtlebot3-gazebo ros-${ROS_DISTRO}-nav2-costmap-2d ros-${ROS_DISTRO}-nav2-* \
    ros-${ROS_DISTRO}-robot-localization ros-${ROS_DISTRO}-octomap* ros-${ROS_DISTRO}-tf2-tools locate ros-${ROS_DISTRO}-nav2_*
#    && rm -rf /var/lib/apt/lists/*

RUN pip install tmule==1.5.9
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

# Add `colcon_cd` to your shell startup script
# https://docs.ros.org/en/galactic/Tutorials/Configuring-ROS2-Environment.html#add-colcon-cd-to-your-shell-startup-script
RUN echo "source /usr/share/colcon_cd/function/colcon_cd.sh" >> ~/.bashrc \
    && echo "export _colcon_cd_root=${ros_ws}" >> ~/.bashrc

COPY ./config/.dogtoothrc /home/developer/

RUN echo "source /home/developer/dogtooth_ws/install/setup.bash" >> ~/.bashrc
RUN echo "source /home/developer/.dogtoothrc" >> ~/.bashrc
RUN echo "source /home/developer/dogtooth_ws/src/Dogtooth/dogtooth_bringup/tmule/tmule_config/init_cmd_setup.sh" >> ~/.bashrc 
RUN echo "source /home/developer/dogtooth_ws/src/Dogtooth/.runcom" >> ~/.bashrc
RUN echo "alias dogtooth_tmule_cd='cd /home/developer/dogtooth_ws/src/Dogtooth/dogtooth_bringup/tmule/'" >> ~/.bashrc
RUN echo "alias dogtooth_tmule_exec='tmule -c dogtooth-robot.yaml launch'"  >> ~/.bashrc

# RUN  echo "export USER=$USER" >> ~/.bashrc
# This entrypoint is from base image.
# See https://github.com/osrf/docker_images/blob/master/ros/galactic/ubuntu/focal/ros-core/ros_entrypoint.sh
ENTRYPOINT ["/ros_entrypoint.sh"]

CMD ["sleep", "infinity"]
