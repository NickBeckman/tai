
[Edit on GitHub](https://github.com/ROBOTIS-GIT/emanual/blob/master/docs/en/platform/turtlebot3/simulation/standalone_gazebo_simulation.md "https://github.com/ROBOTIS-GIT/emanual/blob/master/docs/en/platform/turtlebot3/simulation/standalone_gazebo_simulation.md") 

Kinetic 
Melodic
Noetic
Dashing
Foxy
Humble
Windows

## [Standalone Gazebo Simulation](#standalone-gazebo-simulation "#standalone-gazebo-simulation")

**NOTE**: This tutorial is developed only for user who want to simulate TurtleBot3 without ROS. However, we highly recommend to run simulation on ROS.

1. Install Library for Gazebo7

```
$ sudo apt-get install libgazebo7-dev

```
2. Download Source Code from Github

```
$ git clone https://github.com/ROBOTIS-GIT/turtlebot3_gazebo_plugin

```
3. Add Gazebo Plugin Path in `.bashrc` File

```
$ nano ~/.bashrc

```

**NOTE**: turtlebot3\_gazebo\_plugin path = ~/turtlebot3\_gazebo\_plugin

```
 export GAZEBO\_PLUGIN\_PATH=$GAZEBO\_PLUGIN\_PATH:${turtlebot3\_gazebo\_plugin path}/build
 export GAZEBO\_MODEL\_PATH=$GAZEBO\_MODEL\_PATH:${turtlebot3\_gazebo\_plugin path}/models

```
4. Make and Build

```
$ cd ${turtlebot3\_gazebo\_plugin path}
$ mkdir build
$ cd build
$ cmake ..
$ make

```
5. Execute Gazebo Plugin.  

 Replace the **${TB3\_MODEL}** with the TurtleBot3 model you want to use: `burger`, `waffle`, `waffle_pi`.

```
$ cd ${turtlebot3\_gazebo\_plugin}
$ gazebo worlds/turtlebot3_${TB3\_MODEL}.world

```

![](/assets/images/platform/turtlebot3/simulation/gazebo_waffle_pi.png)  

![](/assets/images/platform/turtlebot3/simulation/gazebo_burger.png)
6. Teleoperation with Keyboard

```
w - set linear velocity up
x - set linear velocity down
d - set angular velocity up
a - set angular velocity down
s - set all velocity to zero

```
7. Topic Subscribe Command
	* Show all topic

```
	$ gz topic -l

```
	* Subscribe scan data

```
	$ gz topic -e /gazebo/default/user/turtlebot3_${TB3\_MODEL}/lidar/hls_lfcd_lds/scan

```
	* Subscribe image data
		+ For Waffle

```
		 $ gz topic -e /gazebo/default/user/turtlebot3_waffle/image/intel_realsense_r200/image

```
		+ For Waffle Pi

```
		 $ gz topic -e /gazebo/default/user/turtlebot3_waffle_pi/image/raspberry_pi_cam/image

```
8. Execute listener

```
$ cd ${turtlebot3\_gazebo\_plugin}/build
$ ./lidar_listener ${TB3\_MODEL}

```
9. Open a new terminal window and enter below command.

```
$ cd ${turtlebot3\_gazebo\_plugin}/build
$ ./image_listener ${TB3\_MODEL}

```

**NOTE**: This feature is available for Kinetic only.

**NOTE**: This feature is available for Kinetic only.

**NOTE**: This feature is available for Kinetic only.

**NOTE**: This feature is available for Kinetic only.

**NOTE**: This feature is available for Kinetic only.

**NOTE**: This feature is available for Kinetic only.

**NOTE**: This feature is available for Kinetic only.

 Previous Page
Next Page 