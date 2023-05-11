cmake_minimum_required(VERSION 3.14)
project(tier4_autoware_api_launch)

find_package(autoware_cmake REQUIRED)
autoware_package(USE_AMENT_EX)

ament_ex_package(INSTALL_TO_SHARE launch)
