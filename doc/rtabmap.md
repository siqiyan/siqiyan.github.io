# RTAB-Map

I created this documentation for my own reference so that in the future I don't
need to start from the beginning and figure out everything again. It might not
work in general since I only tested on my own machine.

## System Requirement

* Ubuntu 16.04
* ROS Kinetic

## Hardware Requirement

* Astra Camera

## Install Dependencies

I am putting every dependencies as well as RTAB-Map itself in a folder called
`rtabmap_modules` for convenience.

```Bash
mkdir ~/rtabmap_modules
```

Then install required dependencies through apt:

```Bash
sudo apt update
sudo apt install libsqlite3-dev libpcl-dev libopencv-dev git cmake libproj-dev libqt5svg5-dev
```

Install Astra camera driver:
```Bash
sudo apt install ros-kinetic-astra-*
```

### OpenCV

I am using this commit: 834c99255320fb565259d3e9177edcb590d4a6be, also we need
[opencv\_contrib](https://github.com/opencv/opencv_contrib), which used this
commit: fd004893cbc8c5c3f7dd45a17f0e34673027320c.

```Bash
cd ~/rtabmap_modules
git clone https://github.com/opencv/opencv.git
git clone https://github.com/opencv/opencv_contrib.git
cd opencv
mkdir build
cd build
cmake cmake -DOPENCV_EXTRA_MODULES_PATH=../../opencv_contrib/modules ..
make -j
sudo make install
```

### Other dependencies

g2o:

```Bash
cd ~/rtabmap_modules
git clone https://github.com/RainerKuemmerle/g2o.git 
cd g2o
mkdir build
cd build
cmake -DBUILD_WITH_MARCH_NATIVE=OFF -DG2O_BUILD_APPS=OFF -DG2O_BUILD_EXAMPLES=OFF -DG2O_USE_OPENGL=OFF ..
make -j4
sudo make install
```

GTSAM:

```Bash
git clone --branch 4.0.0-alpha2 https://github.com/borglab/gtsam.git gtsam-4.0.0-alpha2
cd gtsam-4.0.0-alpha2
mkdir build
cd build
cmake -DGTSAM_USE_SYSTEM_EIGEN=ON -DGTSAM_BUILD_EXAMPLES_ALWAYS=OFF -DGTSAM_BUILD_TESTS=OFF -DGTSAM_BUILD_UNSTABLE=OFF ..
make -j4
sudo make install
```

## Install RTAB-Map

I am using RTAB-Map 0.19.3 for compatibility with rtabmap\_ros, and I couldn't
get other version working for now.

```Bash
cd ~/rtabmap_modules
wget https://github.com/introlab/rtabmap/archive/0.19.3-kinetic.tar.gz
tar xvf 0.19.3-kinetic.tar.gz
trash 0.19.3-kinetic.tar.gz
cd rtabmap-0.19.3
mkdir build
cd build
cmake ..
make -j
sudo make install
```

Now we can build the ROS interface for rtabmap:
```Bash
cd ~/rtabmap_modules
mkdir -p catkin_ws/src
cd catkin_ws/src
wget https://github.com/introlab/rtabmap_ros/archive/0.19.3-kinetic.tar.gz
tar xvf 0.19.3-kinetic.tar.gz
trash 0.19.3-kinetic.tar.gz
cd ..
catkin_make
```

## Usage

Launch Astra camera:

```Bash
roslaunch astra_launch astra.launch
```

In another terminal launch rtabmap:
```Bash
. ~/rtabmap_modules/catkin_ws/devel/setup.bash
roslaunch rtabmap_ros rtabmap.launch
```

## References

[RTAB-Map](http://introlab.github.io/rtabmap/)

[https://scott-yantek.squarespace.com/research/2018/1/16/rtab-map-setup-with-orbbec-astra-in-ros](https://scott-yantek.squarespace.com/research/2018/1/16/rtab-map-setup-with-orbbec-astra-in-ros)
