# AR.Drone_basic_control
This repository contains 4 ROS packages. 
Three have been downloaded - ardrone_autonomy(http://ardrone-autonomy.readthedocs.io/en/latest/), tum_ardrone(http://wiki.ros.org/tum_ardrone) and tum_simulator(http://wiki.ros.org/tum_simulator). 
One was created by me - ardrone_test.

## Description of contents of 4 packages
* ardrone_autonomy

this package connects the entire AR Drone system to the ROS environment giving you the control of the motion of the drone and publishes the IMU, magnetometer and navigation (attitudes, velocities, processed accelerations, altitude, battery percent, etc.) data (through the /imu, /mag, /navdata and /navdata_gps topics) and camera images (through the /front/image_raw and /bottom/image_raw topics), etc. 

* ardrone_test (created by me)

This package cpntains node (ardrone_test_node - with code in waypoint_nav.cpp file) that contains subscribers that subscribe to all the above topics published by the ardrone_autonomy node. This data (accelerometer, magnetometer, gyroscope, camera, gps, etc) can then be processed in this node. 

This node also contains publishers that publish takeoff, land and drone control commands to /ardrone/takeoff, /ardrone/land and /cmd_vel topics. These publishers can be utilised through takeoff(), land() and move(lx,ly,lz,rx,ry,rz) fucntions. For simplicity and ease of use, running this node will open up a menu allowing you to press keyboard buttons to takeoff, land and perform basic movements (left, right, up, down, yaw). (https://drive.google.com/open?id=0B3_gyQ1dIf-QTmE5Z200Y3JmVGc)

All further code (to manipulate drone some way by sending control commands) shall be written here in waypoint_nav.cpp

* tum_ardrone [used only drone_gui node]

Running this node will open a simple GUI for controlling the drone (i.e. move up, down, left, right, takeoff and land). This GUI is an alternate option to perform basic movements and to land in case of emergencies. (http://wiki.ros.org/tum_ardrone/drone_gui)

* tum_simulator

This package contains the implementation of a gazebo simulator for the Ardrone 2.0 .

## Builidng the code (after downloading into catkin_ws folder)

```
cd catkin_ws/
```
```
catkin_make
```
## Running the code on the actual AR.Drone 2.0

```
roscore
```
```
rosrun ardrone_autonomy ardrone_driver _navdata_demo:=0
```
```
rosrun ardrone_test ardrone_test_node
```
```
rosrun tum_ardrone drone_gui
```
## Running a simulation of AR.Drone 2.0 on Gazebo

```
roscore
```
```
roslaunch cvg_sim_gazebo ardrone_testworld.launch
```
```
rosrun ardrone_test ardrone_test_node
```
```
rosrun tum_ardrone drone_gui
```