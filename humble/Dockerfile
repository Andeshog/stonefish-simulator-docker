FROM ros:humble

RUN apt-get update && apt-get upgrade -y

RUN apt-get install -y git

RUN git clone https://github.com/patrykcieslak/stonefish

RUN apt-get install -y \
    libsdl2-dev \
    libglm-dev \
    libfreetype6-dev \
    ros-humble-pcl-conversions \
    ros-humble-image-transport 

RUN cd stonefish && \
    mkdir -p build && \
    cd build && cmake .. && \
    make -j4 && make install

RUN mkdir -p stonefish_ws/src && \
    cd stonefish_ws/src && git clone https://github.com/patrykcieslak/stonefish_ros2.git

RUN /bin/bash -c "source /opt/ros/humble/setup.bash && \
    cd /stonefish_ws && \
    export MAKEFLAGS='-j1 -l1' && colcon build"

ENV LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH

COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
CMD ["bash"]
