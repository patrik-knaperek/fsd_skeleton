cmake_minimum_required(VERSION 3.0.4)
# TODO: Change name of package
project(fsd_common_msgs)

find_package(catkin REQUIRED COMPONENTS
  message_generation  # Needed to generate custom message types
  std_msgs
  roscpp
  rospy
  geometry_msgs
  )

add_message_files(  # Tell catkin which custom message files to include
  FILES
  Cone.msg
  ConeDetections.msg
  Map.msg
  ControlCommand.msg
  CarState.msg
  CarStateDt.msg
  Mission.msg
  )

generate_messages(
  DEPENDENCIES
  std_msgs
  geometry_msgs
)

catkin_package(
  CATKIN_DEPENDS message_runtime std_msgs geometry_msgs # Needed to generate custom messages
)
include_directories(
  # include
  ${catkin_INCLUDE_DIRS}
  ${roscpp_INCLUDE_DIRS}
  ${rospy_INCLUDE_DIRS}
)

