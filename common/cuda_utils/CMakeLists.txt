cmake_minimum_required(VERSION 3.5)
project(cuda_utils)

find_package(autoware_cmake REQUIRED)
autoware_package()

ament_auto_find_package(CUDA)

if(NOT ${CUDA_FOUND})
  message(WARNING "cuda is not found, so the cuda_utils package won't be built.")
  return()
endif()

ament_auto_add_library(cuda_utils INTERFACE)
ament_target_dependencies(cuda_utils SYSTEM INTERFACE CUDA)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
endif()

ament_auto_package(EXPORT_LIBRARY_TARGETS )
