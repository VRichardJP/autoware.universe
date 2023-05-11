cmake_minimum_required(VERSION 3.14)
project(stop_filter)

find_package(autoware_cmake REQUIRED)
autoware_package(USE_AMENT_EX)

ament_ex_add_executable(stop_filter
  src/stop_filter_node.cpp
  src/stop_filter.cpp
)

ament_ex_package(
  INSTALL_TO_SHARE
  launch
)
