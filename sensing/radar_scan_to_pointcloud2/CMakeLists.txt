cmake_minimum_required(VERSION 3.5)
project(radar_scan_to_pointcloud2)

# Dependencies
find_package(autoware_cmake REQUIRED)
autoware_package(USE_AMENT_EX)

# Targets
ament_ex_add_library(radar_scan_to_pointcloud2_node_component SHARED
  src/radar_scan_to_pointcloud2_node/radar_scan_to_pointcloud2_node.cpp
)

rclcpp_components_register_node(radar_scan_to_pointcloud2_node_component
  PLUGIN "radar_scan_to_pointcloud2::RadarScanToPointcloud2Node"
  EXECUTABLE radar_scan_to_pointcloud2_node
)

# Tests
if(BUILD_TESTING)
  list(APPEND AMENT_LINT_AUTO_EXCLUDE ament_cmake_uncrustify)

  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
endif()

# Package
ament_ex_package(
  INSTALL_TO_SHARE
  launch
)
