cmake_minimum_required(VERSION 3.14)
project(motion_utils)

find_package(autoware_cmake REQUIRED)
autoware_package()

ament_auto_add_library(motion_utils SHARED
  src/motion_utils.cpp
  src/distance/distance.cpp
  src/marker/marker_helper.cpp
  src/resample/resample.cpp
  src/trajectory/interpolation.cpp
  src/trajectory/path_with_lane_id.cpp
  src/vehicle/vehicle_state_checker.cpp
)

if(BUILD_TESTING)
  file(GLOB_RECURSE test_files test/**/*.cpp)

  ament_add_ros_isolated_gtest(test_motion_utils ${test_files})

  ament_auto_target_add_package_dependencies(test_motion_utils TEST_DEPS)

  target_link_libraries(test_motion_utils
    motion_utils
  )
endif()

ament_auto_package(EXPORT_LIBRARY_TARGETS )
