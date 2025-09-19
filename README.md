
# Notes. 

- For the ROS1_Bridge to work, I have created this new repo for both ros1 and ros2 zed interfaces following the practises of https://github.com/TommyChangUMD/ros-humble-ros1-bridge-builder.

- However, package name conflicts with ros1_bridge
- ros1 packages should end with _msg and ros2 can be end with `_interfaces` or `_msgs`. Our ros1 package is zed_interfaces. so, to not to disturb visionAI flow or ros1 flow, forked and updated ros1_bridge to accept both _interfaces and _msgs. 
- Then, the new ros2 interfaces commit has changed a  lot especially with that skeleton 3d and not matching with ros1 skeleton3d/2d. So, I have gone to very first commit of ros2 to match ros1 msgs. 

```
zed ros2 commit(Old to match with ROS1 VisionAI) : https://github.com/stereolabs/zed-ros2-interfaces/commit/f766201a15968c8efa234ddad4ddd84f4273e5c3
```

```
source /zed_msgs/zed_msgs_ros2/install/setup.bash
source /ros-humble-ros1-bridge/install/local_setup.bash
ros2 run ros1_bridge dynamic_bridge --print-pairs | grep -i zed
  - 'zed_interfaces/msg/BoundingBox2Df' (ROS 2) <=> 'zed_interfaces/BoundingBox2Df' (ROS 1)
  - 'zed_interfaces/msg/BoundingBox2Di' (ROS 2) <=> 'zed_interfaces/BoundingBox2Di' (ROS 1)
  - 'zed_interfaces/msg/BoundingBox3D' (ROS 2) <=> 'zed_interfaces/BoundingBox3D' (ROS 1)
  - 'zed_interfaces/msg/Keypoint2Df' (ROS 2) <=> 'zed_interfaces/Keypoint2Df' (ROS 1)
  - 'zed_interfaces/msg/Keypoint2Di' (ROS 2) <=> 'zed_interfaces/Keypoint2Di' (ROS 1)
  - 'zed_interfaces/msg/Keypoint3D' (ROS 2) <=> 'zed_interfaces/Keypoint3D' (ROS 1)
  - 'zed_interfaces/msg/Object' (ROS 2) <=> 'zed_interfaces/Object' (ROS 1)
  - 'zed_interfaces/msg/ObjectsStamped' (ROS 2) <=> 'zed_interfaces/ObjectsStamped' (ROS 1)
  - 'zed_interfaces/msg/Skeleton2D' (ROS 2) <=> 'zed_interfaces/Skeleton2D' (ROS 1)
  - 'zed_interfaces/msg/Skeleton3D' (ROS 2) <=> 'zed_interfaces/Skeleton3D' (ROS 1)


  ros2 run ros1_bridge dynamic_bridge --bridge-all-topics
```