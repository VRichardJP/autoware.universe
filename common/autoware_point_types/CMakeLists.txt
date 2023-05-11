cmake_minimum_required(VERSION 3.14)
project(autoware_point_types)

find_package(autoware_cmake REQUIRED)
autoware_package(USE_AMENT_EX)

ament_ex_add_library(autoware_point_types INTERFACE)
ament_target_dependencies(autoware_point_types SYSTEM INTERFACE PCL)

if(BUILD_TESTING)
  ament_add_ros_isolated_gtest(test_autoware_point_types
    test/test_point_types.cpp
  )
  ament_ex_target_add_package_dependencies(test_autoware_point_types TEST_DEPS)
  target_link_libraries(test_autoware_point_types
    autoware_point_types
  )
endif()

ament_ex_package()
