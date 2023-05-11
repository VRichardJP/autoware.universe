cmake_minimum_required(VERSION 3.14)
project(component_interface_utils)

find_package(autoware_cmake REQUIRED)
autoware_package(USE_AMENT_EX)

ament_ex_add_library(component_interface_utils INTERFACE)

ament_ex_package()
