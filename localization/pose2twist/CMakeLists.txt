cmake_minimum_required(VERSION 3.14)
project(pose2twist)

find_package(autoware_cmake REQUIRED)
autoware_package(USE_AMENT_EX)

ament_ex_add_executable(pose2twist
  src/pose2twist_node.cpp
  src/pose2twist_core.cpp
)

ament_ex_package(
  INSTALL_TO_SHARE
  launch
)
