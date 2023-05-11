cmake_minimum_required(VERSION 3.14)
project(map_height_fitter)

find_package(autoware_cmake REQUIRED)
autoware_package()

ament_auto_find_package(PCL REQUIRED COMPONENTS common)

ament_auto_add_library(map_height_fitter SHARED
  src/map_height_fitter.cpp
)
ament_target_dependencies(map_height_fitter SYSTEM PCL)

ament_auto_package(EXPORT_LIBRARY_TARGETS )
