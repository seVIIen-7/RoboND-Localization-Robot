# Localization Robot
In this project, the [ROS AMCL package](http://wiki.ros.org/amcl) is utilized to accurately localize a mobile robot inside a map in the Gazebo simulation environments. There are nodes.
1. [Map Server Node](http://wiki.ros.org/map_server)
2. AMCL Node
3. Move Base Node
4. [Teleop Node](https://github.com/ros-teleop/teleop_twist_keyboard)
## Project Environment
To run this package, some of the following package might need to be installed. You could install them as shown below:
```
$ sudo apt-get install ros-kinetic-navigation
$ sudo apt-get install ros-kinetic-map-server
$ sudo apt-get install ros-kinetic-move-base
$ sudo apt-get install ros-kinetic-amcl
```
## Test
First, launch the simulation:
```
$ cd /home/workspace/catkin_ws/
$ roslaunch <YOUR PACKAGE NAME> <YOUR WORLD>.launch
```
In a new terminal, launch the amcl launch file:
```
$ roslaunch <YOUR PACKAGE NAME> amcl.launch
```
RViz Configuration:
- Select `odom` for fixed frame
- Click the "Add" button and
  - add `RobotModel`: thiss would add the robot itself to RViz
  - add `Map` and select first `topic/map`: the second and third topics in the list will show the global costmap, and the local costmap. Both can be helpful to tune your parameters
  - add `PoseArray` and select `topic/particlecloud`: this will display a set of arrows around the robot

Each arrow is essentially a particle defining the pose of the robot that this localization package created.

Tune the parameter and use the following 2 methods:
### Option 1: Send `2D Navigation Goal`
Click the 2D Nav Goal button in the toolbar, then click and drag on the map to send the goal to the robot. It will start moving and localize itself in the process. If you would like to give amcl node a nudge, you could give the robot an initial position estimate on the map using 2D Pose Estimate.
### Option 2: Use `teleop` Node
Open another terminal and launch the `teleop` script:
```
rosrun teleop_twist_keyboard teleop_twist_keyboard.py
```
