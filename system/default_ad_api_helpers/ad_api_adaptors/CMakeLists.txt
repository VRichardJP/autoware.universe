cmake_minimum_required(VERSION 3.14)
project(ad_api_adaptors)

find_package(autoware_cmake REQUIRED)
autoware_package(USE_AMENT_EX)

ament_ex_add_executable(initial_pose_adaptor
  src/initial_pose_adaptor.cpp
)

ament_ex_add_executable(routing_adaptor
  src/routing_adaptor.cpp
)

ament_ex_package(INSTALL_TO_SHARE config launch)
