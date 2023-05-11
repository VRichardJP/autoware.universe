cmake_minimum_required(VERSION 3.14)
project(geo_pos_conv)

find_package(autoware_cmake REQUIRED)
autoware_package(USE_AMENT_EX)

ament_ex_add_library(geo_pos_conv SHARED
  src/geo_pos_conv.cpp
)

ament_ex_package()
