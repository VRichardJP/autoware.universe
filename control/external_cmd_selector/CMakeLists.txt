cmake_minimum_required(VERSION 3.14)
project(external_cmd_selector)

find_package(autoware_cmake REQUIRED)
autoware_package(USE_AMENT_EX)

ament_ex_add_library(external_cmd_selector_node SHARED
  src/external_cmd_selector/external_cmd_selector_node.cpp
)

rclcpp_components_register_node(external_cmd_selector_node
  PLUGIN "ExternalCmdSelector"
  EXECUTABLE external_cmd_selector
)

ament_ex_package(INSTALL_TO_SHARE
  launch
  config
)
