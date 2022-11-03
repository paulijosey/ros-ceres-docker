ARG ros_version='noetic'
FROM ros:${ros_version}-perception-focal
ARG ceres_version='1.14.0'

ENV CATKIN_WS=/root/catkin_ws
ENV DATA_DIR=/root/data

      # set up thread number for building
RUN   apt-get update && apt-get upgrade -y && apt-get install -y \
      cmake \
      git \
      bc \
      i2c-tools \
      libatlas-base-dev \
      libgflags-dev \
      libeigen3-dev \
      libgoogle-glog-dev \
      libsuitesparse-dev && \
      rm -rf /var/lib/apt/lists/*

      # Build and install Ceres
RUN   if [ "x$(nproc)" = "x1" ] ; then export USE_PROC=1 ; \
      else export USE_PROC=$(($(nproc)/2)) ; fi && \
      git clone https://ceres-solver.googlesource.com/ceres-solver && \
      cd ceres-solver && \
      git checkout tags/$ceres_version && \
      mkdir build && cd build && \
      cmake .. && \
      make install -j$(USE_PROC) && \
      rm -rf ../../ceres-solver && \
      rm -rf /var/lib/apt/lists/*
