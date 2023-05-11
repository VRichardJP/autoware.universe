cmake_minimum_required(VERSION 3.14)
project(kalman_filter)

find_package(autoware_cmake REQUIRED)
autoware_package()

ament_auto_find_package(Eigen3 REQUIRED)

ament_auto_add_library(kalman_filter SHARED
  src/kalman_filter.cpp
  src/time_delay_kalman_filter.cpp
  include/kalman_filter/kalman_filter.hpp
  include/kalman_filter/time_delay_kalman_filter.hpp
)

target_link_libraries(kalman_filter
  Eigen3::Eigen
)

ament_auto_package(EXPORT_LIBRARY_TARGETS )
