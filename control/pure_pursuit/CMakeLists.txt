cmake_minimum_required(VERSION 3.14)
project(pure_pursuit)

find_package(autoware_cmake REQUIRED)
autoware_package(USE_AMENT_EX)

find_package(Eigen3 REQUIRED)

# pure_pursuit_core
ament_ex_add_library(pure_pursuit_core SHARED
  src/pure_pursuit_core/planning_utils.cpp
  src/pure_pursuit_core/pure_pursuit.cpp
  src/pure_pursuit_core/interpolate.cpp
)

target_link_libraries(pure_pursuit_core
  Eigen3::Eigen
)

# pure_pursuit
ament_ex_add_library(pure_pursuit_lateral_controller SHARED
  src/pure_pursuit/pure_pursuit_lateral_controller.cpp
  src/pure_pursuit/pure_pursuit_viz.cpp
)

target_link_libraries(pure_pursuit_lateral_controller
  pure_pursuit_core
)

rclcpp_components_register_node(pure_pursuit_lateral_controller
  PLUGIN "pure_pursuit::PurePursuitLateralController"
  EXECUTABLE pure_pursuit_lateral_controller_exe
)

ament_ex_package(INSTALL_TO_SHARE
  launch
  config
)
