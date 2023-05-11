cmake_minimum_required(VERSION 3.14)
project(twist2accel)

find_package(autoware_cmake REQUIRED)
autoware_package(USE_AMENT_EX)

ament_ex_add_executable(twist2accel
  src/twist2accel_node.cpp
  src/twist2accel.cpp
)

ament_ex_package(
  INSTALL_TO_SHARE
  launch
)
