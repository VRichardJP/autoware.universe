cmake_minimum_required(VERSION 3.14)
project(tier4_screen_capture_rviz_plugin)

find_package(autoware_cmake REQUIRED)
autoware_package(USE_AMENT_EX)

ament_ex_find_package(OpenCV REQUIRED)
ament_ex_find_package(Qt5 REQUIRED Core Widgets)
set(QT_LIBRARIES Qt5::Widgets)
set(CMAKE_AUTOMOC ON)
set(CMAKE_INCLUDE_CURRENT_DIR ON)

ament_ex_add_library(${PROJECT_NAME} SHARED
  src/screen_capture_panel.hpp
  src/screen_capture_panel.cpp
)

ament_target_dependencies(${PROJECT_NAME} SYSTEM OpenCV)

target_link_libraries(${PROJECT_NAME}
  ${QT_LIBRARIES}
)
pluginlib_export_plugin_description_file(rviz_common plugins/plugin_description.xml)

ament_ex_package(
  INSTALL_TO_SHARE
    plugins
)
