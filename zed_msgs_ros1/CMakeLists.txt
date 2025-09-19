cmake_minimum_required(VERSION 3.5)

project(zed_interfaces)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
## Generate symbols for IDE indexer
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)


find_package(catkin REQUIRED COMPONENTS
  std_msgs
  geometry_msgs
  sensor_msgs
  #actionlib_msgs
  message_generation
  message_runtime
  message_runtime
  shape_msgs
)

add_message_files( 
    DIRECTORY msg 
    FILES
    BoundingBox2Df.msg
    BoundingBox2Di.msg
    BoundingBox3D.msg
    Keypoint2Df.msg
    Keypoint2Di.msg
    Keypoint3D.msg
    Object.msg
    ObjectsStamped.msg
    Skeleton2D.msg
    Skeleton3D.msg
    RGBDSensors.msg
    PlaneStamped.msg
    PosTrackStatus.msg
  )

#add_action_files(DIRECTORY action FILES act.action)

generate_messages(
    DEPENDENCIES
    #actionlib_msgs
    std_msgs
    geometry_msgs
    sensor_msgs
    shape_msgs
)

catkin_package(
    CATKIN_DEPENDS 
    message_generation 
    message_runtime
    std_msgs 
    geometry_msgs 
    sensor_msgs
    #actionlib_msgs
)