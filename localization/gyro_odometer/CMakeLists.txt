cmake_minimum_required(VERSION 3.14)
project(gyro_odometer)

find_package(autoware_cmake REQUIRED)
autoware_package(USE_AMENT_EX)

ament_ex_find_package(fmt REQUIRED)

ament_ex_add_library(gyro_odometer_node SHARED
  src/gyro_odometer_core.cpp
)

target_link_libraries(gyro_odometer_node fmt)

ament_ex_add_executable(${PROJECT_NAME}
  src/gyro_odometer_node.cpp
)

target_link_libraries(${PROJECT_NAME} gyro_odometer_node)

if(BUILD_TESTING)
  ament_add_ros_isolated_gtest(test_gyro_odometer
    test/test_main.cpp
    test/test_gyro_odometer_pubsub.cpp
    test/test_gyro_odometer_helper.cpp
  )
  ament_ex_target_add_package_dependencies(test_gyro_odometer TEST_DEPS)
  target_link_libraries(test_gyro_odometer
    gyro_odometer_node
  )
endif()


ament_ex_package(INSTALL_TO_SHARE
  launch
)
