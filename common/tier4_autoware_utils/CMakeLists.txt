cmake_minimum_required(VERSION 3.14)
project(tier4_autoware_utils)

find_package(autoware_cmake REQUIRED)
autoware_package()

ament_auto_find_package(Boost REQUIRED)
ament_auto_find_package(PCL REQUIRED COMPONENTS common)

ament_auto_add_library(tier4_autoware_utils SHARED
  src/tier4_autoware_utils.cpp
  src/geometry/boost_polygon_utils.cpp
  src/math/sin_table.cpp
  src/math/trigonometry.cpp
  src/ros/msg_operation.cpp
)
ament_target_dependencies(tier4_autoware_utils SYSTEM PCL)
ament_target_dependencies(tier4_autoware_utils SYSTEM Boost)

if(BUILD_TESTING)
  find_package(ament_cmake_ros REQUIRED)

  file(GLOB_RECURSE test_files test/**/*.cpp)

  ament_add_ros_isolated_gtest(test_tier4_autoware_utils ${test_files})
  
  ament_auto_target_add_package_dependencies(test_tier4_autoware_utils TEST_DEPS)

  target_link_libraries(test_tier4_autoware_utils
    tier4_autoware_utils
  )
endif()

ament_auto_package(EXPORT_LIBRARY_TARGETS )
