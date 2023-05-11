cmake_minimum_required(VERSION 3.14)
project(interpolation)

find_package(autoware_cmake REQUIRED)
autoware_package(USE_AMENT_EX)

ament_ex_add_library(interpolation SHARED
  src/linear_interpolation.cpp
  src/spline_interpolation.cpp
  src/spline_interpolation_points_2d.cpp
  src/spherical_linear_interpolation.cpp
)

if(BUILD_TESTING)
  file(GLOB_RECURSE test_files test/**/*.cpp)

  ament_add_ros_isolated_gtest(test_interpolation ${test_files})
  ament_ex_target_add_package_dependencies(test_interpolation TEST_DEPS)

  target_link_libraries(test_interpolation
    interpolation
  )
endif()

ament_ex_package()
