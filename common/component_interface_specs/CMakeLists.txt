cmake_minimum_required(VERSION 3.14)
project(component_interface_specs)

find_package(autoware_cmake REQUIRED)
autoware_package()

ament_auto_add_library(component_interface_specs INTERFACE)

ament_auto_package(EXPORT_LIBRARY_TARGETS )
