cmake_minimum_required(VERSION 3.14)
project(autoware_auto_tf2)

find_package(autoware_cmake REQUIRED)
autoware_package(USE_AMENT_EX)

ament_ex_add_library(autoware_auto_tf2 INTERFACE)

if(BUILD_TESTING)
  ament_add_ros_isolated_gtest(test_tf2_autoware_auto_msgs test/test_tf2_autoware_auto_msgs.cpp)
  ament_ex_target_add_package_dependencies(test_tf2_autoware_auto_msgs TEST_DEPS)
  target_link_libraries(test_tf2_autoware_auto_msgs autoware_auto_tf2)
endif()

ament_ex_package()
