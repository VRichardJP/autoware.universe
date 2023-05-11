cmake_minimum_required(VERSION 3.14)
project(dummy_diag_publisher)

find_package(autoware_cmake REQUIRED)
autoware_package(USE_AMENT_EX)

ament_ex_add_executable(${PROJECT_NAME}
  src/dummy_diag_publisher_node.cpp
  src/dummy_diag_publisher_core.cpp
)

ament_ex_package(INSTALL_TO_SHARE
  launch
  config
)
