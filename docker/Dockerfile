FROM osrf/ros:humble-desktop-full

LABEL maintainer="Salvatore Del Peschio <salvatoredelpeschio@gmail.com>"

ENV DEBIAN_FRONTEND=noninteractive
ENV ROS_DISTRO=humble
ENV LANG=en_US.UTF-8
ENV LC_ALL=en_US.UTF-8

RUN apt-get update && apt-get install -y \
    build-essential cmake git wget curl \
    python3-pip python3-colcon-common-extensions python3-rosdep python3-vcstool \
    vim nano htop tree locales \
    && locale-gen en_US.UTF-8 \
    && rm -rf /var/lib/apt/lists/*

RUN wget https://packages.osrfoundation.org/gazebo.gpg -O /usr/share/keyrings/pkgs-osrf-archive-keyring.gpg \
    && echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/pkgs-osrf-archive-keyring.gpg] http://packages.osrfoundation.org/gazebo/ubuntu-stable $(lsb_release -cs) main" | tee /etc/apt/sources.list.d/gazebo-stable.list > /dev/null

RUN apt-get update && apt-get install -y gz-harmonic && rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install -y \
    ros-${ROS_DISTRO}-ros-gz \
    ros-${ROS_DISTRO}-ros-gz-bridge \
    ros-${ROS_DISTRO}-ros-gz-sim \
    ros-${ROS_DISTRO}-ros-gz-image \
    && rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install -y \
    ros-${ROS_DISTRO}-xacro \
    ros-${ROS_DISTRO}-robot-state-publisher \
    ros-${ROS_DISTRO}-joint-state-publisher \
    ros-${ROS_DISTRO}-joint-state-publisher-gui \
    ros-${ROS_DISTRO}-rviz2 \
    ros-${ROS_DISTRO}-ros2-control \
    ros-${ROS_DISTRO}-ros2-controllers \
    ros-${ROS_DISTRO}-gz-ros2-control \
    ros-${ROS_DISTRO}-tf2-tools \
    ros-${ROS_DISTRO}-tf-transformations \
    && rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install -y \
    ros-${ROS_DISTRO}-ur \
    ros-${ROS_DISTRO}-ur-description \
    ros-${ROS_DISTRO}-ur-moveit-config \
    && rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install -y \
    ros-${ROS_DISTRO}-moveit \
    ros-${ROS_DISTRO}-moveit-setup-assistant \
    && rm -rf /var/lib/apt/lists/*

RUN pip3 install --no-cache-dir \
    black \
    flake8 \
    mypy \
    pytest \
    pytest-cov \
    numpy \
    scipy \
    matplotlib \
    transforms3d

WORKDIR /ros2_ws

RUN echo "source /opt/ros/${ROS_DISTRO}/setup.bash" >> ~/.bashrc && \
    echo "source /ros2_ws/install/setup.bash 2>/dev/null || true" >> ~/.bashrc && \
    echo "alias cb='colcon build --symlink-install'" >> ~/.bashrc && \
    echo "alias ct='colcon test'" >> ~/.bashrc && \
    echo "alias gs='gz sim'" >> ~/.bashrc

CMD ["bash"]