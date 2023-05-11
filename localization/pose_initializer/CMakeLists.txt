cmake_minimum_required(VERSION 3.14)
project(pose_initializer)

find_package(autoware_cmake REQUIRED)
autoware_package()

ament_auto_add_executable(pose_initializer_node
  src/pose_initializer/pose_initializer_node.cpp
  src/pose_initializer/pose_initializer_core.cpp
  src/pose_initializer/gnss_module.cpp
  src/pose_initializer/ndt_module.cpp
  src/pose_initializer/stop_check_module.cpp
  src/pose_initializer/ekf_localization_trigger_module.cpp
  src/pose_initializer/ndt_localization_trigger_module.cpp
)

if(BUILD_TESTING)
  function(add_testcase filepath)
    get_filename_component(filename ${filepath} NAME)
    string(REGEX REPLACE ".cpp" "" test_name ${filename})
    ament_add_gmock(${test_name} ${filepath})
    ament_auto_target_add_package_dependencies(${test_name} TEST_DEPS)
    target_include_directories(${test_name} PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/include)
  endfunction()

  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
  add_testcase(test/test_copy_vector_to_array.cpp)
endif()

ament_auto_package(EXPORT_LIBRARY_TARGETS INSTALL_TO_SHARE
  launch
  config
)
