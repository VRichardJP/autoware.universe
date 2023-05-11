cmake_minimum_required(VERSION 3.14)
project(tier4_api_utils)

find_package(autoware_cmake REQUIRED)
autoware_package()

ament_auto_add_library(tier4_api_utils INTERFACE)

if(BUILD_TESTING)
  ament_add_ros_isolated_gtest(${PROJECT_NAME}_test test/test.cpp)
  ament_auto_target_add_package_dependencies(${PROJECT_NAME}_test TEST_DEPS)
  target_link_libraries(${PROJECT_NAME}_test tier4_api_utils)
endif()

ament_auto_package(EXPORT_LIBRARY_TARGETS )
