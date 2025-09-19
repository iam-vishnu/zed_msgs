# Notes

* To make **ROS1\_Bridge** work, I created a new repository for both **ROS1** and **ROS2** ZED interfaces, following the practices from [ros-humble-ros1-bridge-builder](https://github.com/TommyChangUMD/ros-humble-ros1-bridge-builder).

* Faced a **package name conflict** with `ros1_bridge`.

  * Convention: ROS1 packages should end with `_msg`, while ROS2 packages can end with `_interfaces` or `_msgs`.
  * Our ROS1 package is named `zed_interfaces`. To avoid disturbing the VisionAI or ROS1 flow, I forked and updated `ros1_bridge` to accept both `_interfaces` and `_msgs`.

* The newer **ROS2 interfaces commit** introduced significant changes (e.g., Skeleton3D), which no longer matched the ROS1 `skeleton3d/2d` messages.

  * To maintain compatibility, I reverted to the earliest ROS2 commit that aligns with the ROS1 messages:

    ```
    https://github.com/stereolabs/zed-ros2-interfaces/commit/f766201a15968c8efa234ddad4ddd84f4273e5c3
    ```

* **Repositories created**:

  * [zed\_msgs](https://github.com/iam-vishnu/zed_msgs) → for both ROS1 and ROS2 ZED messages (based on the commit above).

* **ROS1 bridge update**: Added support for `_interfaces` and `_msgs` in ROS1 as well.
  * [ros1\_bridge](https://github.com/iam-vishnu/ros1_bridge)

  * Ref: [Robotics StackExchange Answer](https://robotics.stackexchange.com/a/88029)

---

### Usage

- Refer : https://github.com/bosonrobotics/autopilot_v2/tree/265-perception-image_segmentation-for-ros2/jetson/visionai/ros1-bridge-docker

```bash
source /zed_msgs/zed_msgs_ros2/install/setup.bash
source /ros-humble-ros1-bridge/install/local_setup.bash

# Check available ZED message pairs
ros2 run ros1_bridge dynamic_bridge --print-pairs | grep -i zed
```

Example pairs:

```
- 'zed_interfaces/msg/BoundingBox2Df' (ROS 2) <=> 'zed_interfaces/BoundingBox2Df' (ROS 1)
- 'zed_interfaces/msg/BoundingBox2Di' (ROS 2) <=> 'zed_interfaces/BoundingBox2Di' (ROS 1)
- 'zed_interfaces/msg/BoundingBox3D'  (ROS 2) <=> 'zed_interfaces/BoundingBox3D'  (ROS 1)
- 'zed_interfaces/msg/Keypoint2Df'    (ROS 2) <=> 'zed_interfaces/Keypoint2Df'    (ROS 1)
- 'zed_interfaces/msg/Keypoint2Di'    (ROS 2) <=> 'zed_interfaces/Keypoint2Di'    (ROS 1)
- 'zed_interfaces/msg/Keypoint3D'     (ROS 2) <=> 'zed_interfaces/Keypoint3D'     (ROS 1)
- 'zed_interfaces/msg/Object'         (ROS 2) <=> 'zed_interfaces/Object'         (ROS 1)
- 'zed_interfaces/msg/ObjectsStamped' (ROS 2) <=> 'zed_interfaces/ObjectsStamped' (ROS 1)
- 'zed_interfaces/msg/Skeleton2D'     (ROS 2) <=> 'zed_interfaces/Skeleton2D'     (ROS 1)
- 'zed_interfaces/msg/Skeleton3D'     (ROS 2) <=> 'zed_interfaces/Skeleton3D'     (ROS 1)
```

To bridge all topics:

```bash
ros2 run ros1_bridge dynamic_bridge --bridge-all-topics
```