# Usage
## implementation
1. create or copy ros project multirobot_nv under ~/catkin_ws/src/
```
$ catkin_create_pkg launch_robot
$ cd launch_robot
$ cp all dirs and files in this repo 
```
## configuration
1. add new node for each robot in startall.launch, by giving the robot namesapce and intial (x,y,a) 

```
  <include file="$(find multirobot_nv)/launch/start_namespace.launch">
  <arg name="robot_namespace" value="tb3_0" />
  <arg name="tb3_0_init_x" value="0.0" />
  <arg name="tb3_0_init_y" value="0.0" />
  <arg name="tb3_0_init_a" value="0.0" />
  </include>

  <include file="$(find multirobot_nv)/launch/start_namespace.launch">
  <arg name="robot_namespace" value="tb3_1" />
  <arg name="tb3_1_init_x" value="10.0" />
  <arg name="tb3_1_init_y" value="10.0" />
  <arg name="tb3_1_init_a" value="0.0" />
  </include>

  ...
```

## launch

```
roslaunch multirobot_nv startall.launch
```
