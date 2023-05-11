cmake_minimum_required(VERSION 3.14)
project(map_tf_generator)

find_package(autoware_cmake REQUIRED)
autoware_package(USE_AMENT_EX)

ament_ex_find_package(PCL REQUIRED)

ament_ex_add_library(pcd_map_tf_generator_node SHARED
  src/pcd_map_tf_generator_node.cpp
)
ament_target_dependencies(pcd_map_tf_generator_node SYSTEM PCL)
# FIXME(VRichardJP) to remove after https://github.com/ament/ament_cmake/issues/451 is fixed
target_link_libraries(pcd_map_tf_generator_node ${PCL_LIBRARIES})

rclcpp_components_register_node(pcd_map_tf_generator_node
  PLUGIN "PcdMapTFGeneratorNode"
  EXECUTABLE pcd_map_tf_generator
)

ament_ex_add_library(vector_map_tf_generator_node SHARED
  src/vector_map_tf_generator_node.cpp
)

rclcpp_components_register_node(vector_map_tf_generator_node
  PLUGIN "VectorMapTFGeneratorNode"
  EXECUTABLE vector_map_tf_generator
)

if(BUILD_TESTING)
  function(add_testcase filepath)
    get_filename_component(filename ${filepath} NAME)
    string(REGEX REPLACE ".cpp" "" test_name ${filename})

    ament_add_gmock(${test_name} ${filepath})
    ament_ex_target_add_package_dependencies(${test_name} TEST_DEPS)
    target_include_directories(${test_name} PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/include)
  endfunction()

  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()

  add_testcase(test/test_uniform_random.cpp)
endif()

ament_ex_package(INSTALL_TO_SHARE
  launch
)
