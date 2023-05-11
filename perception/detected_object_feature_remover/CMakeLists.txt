cmake_minimum_required(VERSION 3.14)
project(detected_object_feature_remover)

find_package(autoware_cmake REQUIRED)
autoware_package(USE_AMENT_EX)

ament_ex_add_library(detected_object_feature_remover_node SHARED
  src/detected_object_feature_remover.cpp
)

rclcpp_components_register_node(detected_object_feature_remover_node
  PLUGIN "detected_object_feature_remover::DetectedObjectFeatureRemover"
  EXECUTABLE detected_object_feature_remover
)

ament_ex_package(
  INSTALL_TO_SHARE
    launch
)
