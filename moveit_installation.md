# MoveIt Installation ROS Noetic



Reference: https://ros-planning.github.io/moveit_tutorials/doc/getting_started/getting_started.html



## Prep Work



```bash
$ sudo apt-get install python3-rosdep
$ sudo rosdep init
$ rosdep update
$ sudo apt update
$ sudo apt dist-upgrade
$ sudo apt install ros-noetic-catkin python3-catkin-tools python3-osrf-pycommon
$ sudo apt install python3-wstool
```



## MoveIt Workspace 

```bash
$ mkdir -p ~/ws_moveit/src
$ cd ~/ws_moveit/src

$ wstool init .
$ wstool merge -t . https://raw.githubusercontent.com/ros-planning/moveit/master/moveit.rosinstall
$ wstool remove  moveit_tutorials  # this is cloned in the next section
$ wstool update -t .
```



## First Example

```bash
$ cd ~/ws_moveit/src
$ git clone https://github.com/ros-planning/moveit_tutorials.git -b master
# git clone https://github.com/ros-planning/panda_moveit_config.git -b melodic-devel

$ cd ~/ws_moveit/src
$ rosdep install -y --from-paths . --ignore-src --rosdistro noetic
```



## Catkin Build and Source

```bash
#For WSL only..
# sudo strip --remove-section=.note.ABI-tag /usr/lib/x86_64-linux-gnu/libQt5Core.so.5

$ cd ~/ws_moveit
$ catkin config --extend /opt/ros/${ROS_DISTRO} --cmake-args -DCMAKE_BUILD_TYPE=Release
$ catkin build
$ source ~/ws_moveit/devel/setup.bash
$ echo 'source ~/ws_moveit/devel/setup.bash' >> ~/.bashrc
```



## Testing

```bash
$ cd
$ roslaunch panda_moveit_config demo.launch rviz_tutorial:=true
```



If you are doing this for the first time, you should see an empty world in RViz and will have to add the Motion Planning Plugin:

- You should see an empty world in RViz:

[![A](https://ros-planning.github.io/moveit_tutorials/_images/rviz_empty.png)](https://ros-planning.github.io/moveit_tutorials/_images/rviz_empty.png)

- In the RViz Displays Tab, press *Add*:

[![B](https://ros-planning.github.io/moveit_tutorials/_images/rviz_click_add.png)](https://ros-planning.github.io/moveit_tutorials/_images/rviz_click_add.png)

- From the moveit_ros_visualization folder, choose “MotionPlanning” as the DisplayType. Press “Ok”.

[![C](https://ros-planning.github.io/moveit_tutorials/_images/rviz_plugin_motion_planning_add.png)](https://ros-planning.github.io/moveit_tutorials/_images/rviz_plugin_motion_planning_add.png)

- You should now see the Panda robot in RViz:

[![D](https://ros-planning.github.io/moveit_tutorials/_images/rviz_start.png)](https://ros-planning.github.io/moveit_tutorials/_images/rviz_start.png)

