cmake_minimum_required(VERSION 3.14)
project(tier4_planning_launch)

find_package(autoware_cmake REQUIRED)
autoware_package()

ament_auto_package(EXPORT_LIBRARY_TARGETS 
  INSTALL_TO_SHARE
  launch
)
