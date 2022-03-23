# ROS Navigation Tutorials

Reference: http://wiki.ros.org/navigation/Tutorials/RobotSetup/TF

```bash
$ mkdir -p nav_ws/src
$ cd nav_ws/src

$ catkin_create_pkg robot_setup_tf roscpp tf geometry_msgs
$ cd robot_setup_tf/src
$ gedit
```



Save the following code as: `tf_broadcaster.cpp`

```cpp
#include <ros/ros.h>
#include <tf/transform_broadcaster.h>

int main(int argc, char** argv){
  ros::init(argc, argv, "robot_tf_publisher");
  ros::NodeHandle n;

  ros::Rate r(100);

  tf::TransformBroadcaster broadcaster;

  while(n.ok()){
    broadcaster.sendTransform(
      tf::StampedTransform(
        tf::Transform(tf::Quaternion(0, 0, 0, 1), tf::Vector3(0.1, 0.0, 0.2)),
        ros::Time::now(),"base_link", "base_laser"));
    r.sleep();
  }
}
```



Save and close file

```bash
$ gedit
```

Save the following code as: `tf_listener.cpp`



```cpp
#include <ros/ros.h>
#include <geometry_msgs/PointStamped.h>
#include <tf/transform_listener.h>

void transformPoint(const tf::TransformListener& listener){
  //we'll create a point in the base_laser frame that we'd like to transform to the base_link frame
  geometry_msgs::PointStamped laser_point;
  laser_point.header.frame_id = "base_laser";

  //we'll just use the most recent transform available for our simple example
  laser_point.header.stamp = ros::Time();

  //just an arbitrary point in space
  laser_point.point.x = 1.0;
  laser_point.point.y = 0.2;
  laser_point.point.z = 0.0;

  try{
    geometry_msgs::PointStamped base_point;
    listener.transformPoint("base_link", laser_point, base_point);

    ROS_INFO("base_laser: (%.2f, %.2f. %.2f) -----> base_link: (%.2f, %.2f, %.2f) at time %.2f",
        laser_point.point.x, laser_point.point.y, laser_point.point.z,
        base_point.point.x, base_point.point.y, base_point.point.z, base_point.header.stamp.toSec());
  }
  catch(tf::TransformException& ex){
    ROS_ERROR("Received an exception trying to transform a point from \"base_laser\" to \"base_link\": %s", ex.what());
  }
}

int main(int argc, char** argv){
  ros::init(argc, argv, "robot_tf_listener");
  ros::NodeHandle n;

  tf::TransformListener listener(ros::Duration(10));

  //we'll transform a point once every second
  ros::Timer timer = n.createTimer(ros::Duration(1.0), boost::bind(&transformPoint, boost::ref(listener)));

  ros::spin();

}
```



```bash
$ cd ..
$ gedit CMakeLists.txt
```



Add the following code at the end of `CMakeLists.txt`

```bash
add_executable(tf_broadcaster src/tf_broadcaster.cpp)
add_executable(tf_listener src/tf_listener.cpp)
target_link_libraries(tf_broadcaster ${catkin_LIBRARIES})
target_link_libraries(tf_listener ${catkin_LIBRARIES})
```

```bash
$ cd
$ cs nav_ws
$ catkin_make
$ echo 'source ~/nav_ws/devel/setup.bash' >> ~/.bashrc
$ source ~/.bashrc
$ rospack list

```



T1

```bash
$ roscore
```

T2

```bash
$ rosrun robot_setup_tf tf_broadcaster
```

T3

```bash
$ rosrun robot_setup_tf tf_listener
```



If all goes well, you should see the following output showing a point being transformed from the "base_laser" frame to the "base_link" frame once a second.

```
[ INFO] 1248138528.200823000: base_laser: (1.00, 0.20. 0.00) -----> base_link: (1.10, 0.20, 0.20) at time 1248138528.19
[ INFO] 1248138529.200820000: base_laser: (1.00, 0.20. 0.00) -----> base_link: (1.10, 0.20, 0.20) at time 1248138529.19
[ INFO] 1248138530.200821000: base_laser: (1.00, 0.20. 0.00) -----> base_link: (1.10, 0.20, 0.20) at time 1248138530.19
[ INFO] 1248138531.200835000: base_laser: (1.00, 0.20. 0.00) -----> base_link: (1.10, 0.20, 0.20) at time 1248138531.19
[ INFO] 1248138532.200849000: base_laser: (1.00, 0.20. 0.00) -----> base_link: (1.10, 0.20, 0.20) at time 1248138532.19
```
