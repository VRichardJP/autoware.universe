cmake_minimum_required(VERSION 3.14)
project(component_state_monitor)

find_package(autoware_cmake REQUIRED)
autoware_package(USE_AMENT_EX)

ament_ex_add_library(${PROJECT_NAME} SHARED
  src/main.cpp
)

rclcpp_components_register_nodes(${PROJECT_NAME}
  "component_state_monitor::StateMonitor"
)

ament_ex_package(INSTALL_TO_SHARE config launch)
