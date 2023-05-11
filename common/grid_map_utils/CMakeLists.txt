cmake_minimum_required(VERSION 3.5)
project(grid_map_utils)

if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 17)
  set(CMAKE_CXX_STANDARD_REQUIRED ON)
  set(CMAKE_CXX_EXTENSIONS OFF)
endif()
if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

find_package(autoware_cmake REQUIRED)
autoware_package(USE_AMENT_EX)

ament_ex_add_library(${PROJECT_NAME} SHARED
  src/polygon_iterator.cpp
)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()

  ament_add_gtest(test_${PROJECT_NAME}
    test/test_polygon_iterator.cpp
  )
  ament_ex_target_add_package_dependencies(test_${PROJECT_NAME} TEST_DEPS)
  target_link_libraries(test_${PROJECT_NAME}
    ${PROJECT_NAME}
  )

  add_executable(benchmark test/benchmark.cpp)
  ament_ex_target_add_package_dependencies(benchmark TEST_DEPS)
  target_link_libraries(benchmark
    ${PROJECT_NAME}
  )
endif()

ament_ex_package()
