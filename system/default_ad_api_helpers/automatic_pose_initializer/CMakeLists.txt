cmake_minimum_required(VERSION 3.14)
project(automatic_pose_initializer)

find_package(autoware_cmake REQUIRED)
autoware_package(USE_AMENT_EX)

ament_ex_add_executable(automatic_pose_initializer
  src/automatic_pose_initializer.cpp
)

ament_ex_package(INSTALL_TO_SHARE launch)
