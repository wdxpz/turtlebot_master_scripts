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





# Build startall.launch file to support multiple type of robots

## current supported robots

* waffle_pi
* waffle
* burge
* rosbot2
* rosbot2_pro

## Build startall.launch

1. read `xml_data` content from startall.launch

2. for first `include` node, set attribute 'map_file' value as the map file path

   ```
   <include file="$(find multirobot_nv)/launch/start_map.launch">
     <arg name="map_file" value="$(env HOME)/map/map.yaml" />
   </include>
   ```

3. if the robot is turtlebot, read 1st 'include' node from: `template_start_turtlebot_namespace.launch`, setting corresponding value for each attributes, append to `xml_data`

   ```
     <include file="$(find multirobot_nv)/launch/start_turtlebot.launch">
     <arg name="robot_namespace" value="tb3_0" />
     <arg name="tb3_0_init_x" value="0.0" />
     <arg name="tb3_0_init_y" value="0.0" />
     <arg name="tb3_0_init_a" value="0.0" />
     <arg name="bot_model" value="waffle_pi" />
     </include>
   ```

4. if the robot is rosbot, read 1st 'include' node from: `template_start_rosbot_namespace.launch`, setting corresponding value for each attributes, append to `xml_data`

   ```
     <include file="$(find multirobot_nv)/launch/start_turtlebot.launch">
     <arg name="robot_namespace" value="rb2_0" />
     <arg name="rb2_0_init_x" value="0.0" />
     <arg name="rb2_0_init_y" value="0.0" />
     <arg name="rb2_0_init_a" value="0.0" />
     <arg name="bot_model" value="rosbot2_pro" />
     </include>
   ```

## Rosbot Resources

### Rosbot Official Docs

1. [rosbot turtorial](https://husarion.com/tutorials/)



### Required packages for navigation

```
mkdir ~/ros_workspace
mkdir ~/ros_workspace/src
cd ~/ros_workspace/src
catkin_init_workspace
sudo apt update

git clone https://github.com/husarion/rosbot_description.git
git clone https://github.com/husarion/rosbot_ekf.git


#Install dependencies
cd ~/ros_workspace
rosdep install --from-paths src --ignore-src -r -y
sudo apt-get install ros-kinetic-robot-localization

#compile
cd ~/ros_workspace
catkin_make

#install enviroment
nano ~/.bashrc
# add: export ~/ros_workspace/devel/setup.sh
source ~/.bashrc

#copy rosbot config yamls to multirobot_nv package
cd ~/catkin_ws/src/multirobot_nv/param
git clone https://github.com/husarion/tutorial_pkg.git
cd turorial_pkg
mv config/ ../rosbot_param
cd ..
rm -rf turorial_pkg
```

### Implementation Reference sor Rosbot launch

1. [map navigation](https://husarion.com/tutorials/ros-tutorials/9-map-navigation/)
2. [config files for movebase](https://github.com/husarion/tutorial_pkg/tree/master/config)

