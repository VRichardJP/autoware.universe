cmake_minimum_required(VERSION 3.14)
project(perception_utils)

find_package(autoware_cmake REQUIRED)
autoware_package(USE_AMENT_EX)

find_package(Boost REQUIRED)

ament_ex_add_library(perception_utils SHARED
  src/predicted_path_utils.cpp
  src/conversion.cpp
)

if(BUILD_TESTING)
  find_package(ament_cmake_ros REQUIRED)

  file(GLOB_RECURSE test_files test/**/*.cpp)

  ament_add_ros_isolated_gtest(test_perception_utils ${test_files})
  ament_ex_target_add_package_dependencies(test_perception_utils TEST_DEPS)
  target_link_libraries(test_perception_utils
    perception_utils
  )
endif()

ament_ex_package()
