cmake_minimum_required(VERSION 3.14)
project(obstacle_collision_checker)

find_package(autoware_cmake REQUIRED)
autoware_package(USE_AMENT_EX)

ament_ex_add_library(obstacle_collision_checker SHARED
  src/obstacle_collision_checker_node/obstacle_collision_checker.cpp
  src/obstacle_collision_checker_node/obstacle_collision_checker_node.cpp
)

rclcpp_components_register_node(obstacle_collision_checker
  PLUGIN "obstacle_collision_checker::ObstacleCollisionCheckerNode"
  EXECUTABLE obstacle_collision_checker_node
)

if(BUILD_TESTING)
  ament_add_ros_isolated_gtest(test_obstacle_collision_checker
    test/test_obstacle_collision_checker.cpp
  )
  ament_ex_target_add_package_dependencies(test_obstacle_collision_checker TEST_DEPS)
  target_link_libraries(test_obstacle_collision_checker obstacle_collision_checker)
endif()

ament_ex_package(
  INSTALL_TO_SHARE
    launch
    config
)
