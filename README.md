# AR.Drone basic control
This repository contains 4 ROS packages. 

Three have been downloaded - ardrone_autonomy, tum_ardrone and tum_simulator. 

One was created by me - ardrone_test.

## Description of contents of 4 packages
### 1. ardrone_autonomy (downloaded)

this package connects the entire AR Drone system to the ROS environment giving you the control of the motion of the drone (by sunscribing to topics like /ardrone/takeoff, /ardrone/land, /cmd_vel to which you can publish takeoff, land and control commands resp.)

It also publishes the IMU, magnetometer and navigation (attitudes, velocities, processed accelerations, altitude, battery percent, etc.) data (through the /imu, /mag, /navdata and /navdata_gps topics) and camera images (through the /front/image_raw and /bottom/image_raw topics), etc. (http://ardrone-autonomy.readthedocs.io/en/latest/)

### 2. ardrone_test (created by me)

This package cpntains node (ardrone_test_node - with code in waypoint_nav.cpp file) that contains subscribers that subscribe to all the above topics published by the ardrone_autonomy node. This data (accelerometer, magnetometer, gyroscope, camera, gps, etc) can then be processed in this node. 

This node also contains publishers that publish takeoff, land and drone control commands to /ardrone/takeoff, /ardrone/land and /cmd_vel topics. These publishers can be utilised through takeoff(), land() and move(lx,ly,lz,rx,ry,rz) fucntions. For simplicity and ease of use, running this node will open up a menu allowing you to press keyboard buttons to takeoff, land and perform basic movements (left, right, up, down, yaw). 

![Alt text](https://raw.github.com/kaustubhsridhar/AR.Drone-basic-control/master/basic_menu.png "menu shown on running ardrone_test_node node")

##### All further code (to manipulate drone some way by sending control commands) shall be written here in ardrone_test_node (i.e. inside waypoint_nav.cpp file)

### 4. tum_simulator (downloaded)

This package contains the implementation of a gazebo simulator for the Ardrone 2.0 . (http://wiki.ros.org/tum_simulator)


## Downloading/Installing the code
Run the following code lines in a terminal
```
mkdir catkin_ws/
```
```
cd catkin_ws/
```
```
git clone https://github.com/kaustubhsridhar/AR.Drone-nonlinear-control-Gazebo-Simulation.git
```
(note that the src folder should be directly in the catkin_ws folder. delete any unnecessary folder created by git cloning)
```
catkin_make --pkg ardrone_autonomy
```
```
catkin_make --pkg ardrone_test
```
```
catkin_make --pkg tum_ardrone
```

## Builidng the code 
Run the following code lines in a terminal
```
cd catkin_ws/
```
```
catkin_make
```
## Running the code on the actual AR.Drone 2.0
Run the following code lines in different terminals

```
roscore
```
```
rosrun ardrone_autonomy ardrone_driver _navdata_demo:=0
```
```
rosrun ardrone_test ardrone_test_node
```
## Running a simulation of AR.Drone 2.0 on Gazebo
Run the following code lines in different terminals

```
roscore
```
```
roslaunch cvg_sim_gazebo ardrone_testworld.launch
```
```
rosrun ardrone_test ardrone_test_node
```
