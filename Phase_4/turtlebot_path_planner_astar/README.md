# Astar_Search_Algorithm_ENPM661-Project-3 Phase4

## By Varun Asthana
### University of Maryland

## Overview

Project 3 phase 4 has 2 python scripts. One script is similar to script from phase3 that generates a 2D map with obstacles and finds a path to travel from a user-defined start and end point. The other script is used to initialize ros node and publish over the required ROS tpics for the simulation of the TurtleBot in Gazevo.

### Dependencies
* ROS Kinetic
* Gazebo7
* python2.7
* numpy
* math
* matplotlib.pyplot
* cv2 (version 3.3)
* time
* heapq
* argparse


### Assumptions
To run the package-
1) Above mentioned dependancies are available and running in the user's system.
2) catkin_ws workspace is properly setup.
(If your workspace is named something else or is at other path, use that name and/or path in the below commands)
3) turtlebot package is installed. If not, then run the below command to install it.
```
$ sudo apt-get install ros-kinetic-turtlebot-gazebo ros-kinetic-turtlebot-apps ros-kinetic-turtlebot-rviz-launchers
```
### How to build and run the program
Copy the folder inside the Phase4 folder to the catkin_ws/src directory
```
$ cd catkin_ws
$ catkin_make
$ source devel/setup.bash
$ roslaunch turtlebot_path_planner_astar planner.launch c:=0.2 x:=-4.5 y:=3 t:=120
```

In the last command above, parameter c is for robot clearance, (x,y,t) are for initial pose as coordinates and theta with origin at the center of the map and theta is measured anti-clockwise from positive x-axis. All parameters are to be in METERS except for 't' to be in degrees.

### User Inputs after launching of ros nodes
All inputs are to be given in METERS
* Left and right wheel RPM (eg: 90,90)
* Goal position in x,y (eg: 0,-3)

RPM is converted to the unit of "rad/sec" by multiplying the user input with 2pi/60.

Least count of 1cm is considered for the complete system with a threshold of 0.5cm in x and y coordinates and 30 degrees in rotation for node generation
Eg 1.014 m will be treated as 1.010 m or 101.0 cm
Eg 1.015 m will be treated as 1.015 m or 101.0 cm
Eg 1.015 m will be treated as 1.016 m or 102.0 cm

Also, ceil value of radius + clearance will be considered. Threshold for reaching the goal is set at 0.1m (or 10cm). 

### Path Generation
The run speed from top left to bottom right of the map (withut plotting of explored nodes) is around 5 mins.

After the goal point is reached, a path will be traced back from the start to goal point. On the map, this path will be drawn in RED. In the file location, an image "back_tracking.png" is saved. Once the path is displayed, the user can type any number and press enter to start the simulation in Gazebo.

### Vidoe Outputs
* demo1.mp4 and demo2.mp4 shows the simulation of TurtleBot in Gazebo for 2 different cases.