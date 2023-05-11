cmake_minimum_required(VERSION 3.14)
project(vehicle_velocity_converter)

find_package(autoware_cmake REQUIRED)
autoware_package(USE_AMENT_EX)

ament_ex_add_executable(vehicle_velocity_converter
  src/vehicle_velocity_converter_node.cpp
  src/vehicle_velocity_converter.cpp
)
ament_target_dependencies(vehicle_velocity_converter)

ament_ex_package(
  INSTALL_TO_SHARE
  launch
  config
)
