cmake_minimum_required(VERSION 3.14)
project(time_utils)

find_package(autoware_cmake REQUIRED)
autoware_package(USE_AMENT_EX)

ament_ex_add_library(${PROJECT_NAME} SHARED src/time_utils/time_utils.cpp)

ament_ex_package()
