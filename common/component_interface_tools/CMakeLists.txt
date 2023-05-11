cmake_minimum_required(VERSION 3.14)
project(component_interface_tools)

find_package(autoware_cmake REQUIRED)
autoware_package(USE_AMENT_EX)

ament_ex_add_executable(service_log_checker src/service_log_checker.cpp)

ament_ex_package(INSTALL_TO_SHARE launch)
