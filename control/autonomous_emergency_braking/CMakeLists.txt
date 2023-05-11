cmake_minimum_required(VERSION 3.14)
project(autonomous_emergency_braking)

find_package(autoware_cmake REQUIRED)
autoware_package(USE_AMENT_EX)

ament_ex_find_package(PCL REQUIRED)

set(AEB_NODE ${PROJECT_NAME}_node)
ament_ex_add_library(${AEB_NODE} SHARED
  src/node.cpp
)

ament_target_dependencies(${AEB_NODE} SYSTEM PCL)

rclcpp_components_register_node(${AEB_NODE}
  PLUGIN "autoware::motion::control::autonomous_emergency_braking::AEB"
  EXECUTABLE ${PROJECT_NAME}
)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
endif()

ament_ex_package(
  INSTALL_TO_SHARE
  launch
  config
)
