cmake_minimum_required(VERSION 3.14)
project(autoware_auto_common)

find_package(autoware_cmake REQUIRED)
autoware_package()

ament_auto_find_package(Eigen3 REQUIRED)

ament_auto_add_library(autoware_auto_common INTERFACE)
target_link_libraries(autoware_auto_common INTERFACE Eigen3::Eigen)

if(BUILD_TESTING)
  set(TEST_COMMON test_common_gtest)
  ament_add_ros_isolated_gtest(${TEST_COMMON}
    test/gtest_main.cpp
    test/test_bool_comparisons.cpp
    test/test_byte_reader.cpp
    test/test_float_comparisons.cpp
    test/test_mahalanobis_distance.cpp
    test/test_message_field_adapters.cpp
    test/test_template_utils.cpp
    test/test_angle_utils.cpp
    test/test_type_name.cpp
    test/test_type_traits.cpp
  )
  ament_auto_target_add_package_dependencies(${TEST_COMMON} TEST_DEPS)
  target_compile_options(${TEST_COMMON} PRIVATE -Wno-sign-conversion)
  target_link_libraries(${TEST_COMMON} autoware_auto_common)
endif()

ament_auto_package(EXPORT_LIBRARY_TARGETS )
