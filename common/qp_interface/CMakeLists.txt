cmake_minimum_required(VERSION 3.14)
project(qp_interface)

find_package(autoware_cmake REQUIRED)
autoware_package()

ament_auto_find_package(Eigen3 REQUIRED)
ament_auto_find_package(proxsuite REQUIRED)

# after find_package(osqp_vendor) in ament_auto_find_build_dependencies
ament_auto_find_package(osqp REQUIRED)
# NOTE(VRichardJP) the way autoware wants to access osqp headers (through prefix osqp/*.h)
# is inconsistent with the way osqp_vendor install and export them:
# - installed directly /opt/ros/humble/include/osqp/*.h
# - but exported with -I/opt/ros/humble/include/osqp
# so the following hack is necessary
get_target_property(OSQP_INCLUDE_SUB_DIR osqp::osqp INTERFACE_INCLUDE_DIRECTORIES)
get_filename_component(OSQP_INCLUDE_DIR ${OSQP_INCLUDE_SUB_DIR} PATH)

set(QP_INTERFACE_LIB_SRC
  src/qp_interface.cpp
  src/osqp_interface.cpp
  src/osqp_csc_matrix_conv.cpp
  src/proxqp_interface.cpp
)

set(QP_INTERFACE_LIB_HEADERS
  include/qp_interface/qp_interface.hpp
  include/qp_interface/osqp_interface.hpp
  include/qp_interface/osqp_csc_matrix_conv.hpp
  include/qp_interface/proxqp_interface.hpp
)

ament_auto_add_library(${PROJECT_NAME} SHARED
  ${QP_INTERFACE_LIB_SRC}
  ${QP_INTERFACE_LIB_HEADERS}
)
target_compile_options(${PROJECT_NAME} PRIVATE -Wno-error=old-style-cast -Wno-error=useless-cast)

# NOTE(VRichardJP) see explanation above
target_include_directories(qp_interface
  SYSTEM PUBLIC
    "${OSQP_INCLUDE_DIR}"
)

target_link_libraries(${PROJECT_NAME}
  Eigen3::Eigen
  osqp::osqp
)

ament_target_dependencies(${PROJECT_NAME}
  proxsuite
)

# NOTE(VRichardJP) see explanation above
# crucial so downstream package builds because osqp_interface exposes osqp.hpp
ament_export_include_directories("${OSQP_INCLUDE_DIR}")
# crucial so the linking order is correct in a downstream package: libosqp_interface.a should come before libosqp.a
# ament_export_libraries(osqp::osqp)

if(BUILD_TESTING)
  set(TEST_SOURCES
    test/test_osqp_interface.cpp
    test/test_csc_matrix_conv.cpp
    test/test_proxqp_interface.cpp
  )
  set(TEST_OSQP_INTERFACE_EXE test_osqp_interface)
  ament_add_ros_isolated_gtest(${TEST_OSQP_INTERFACE_EXE} ${TEST_SOURCES})
  ament_auto_target_add_package_dependencies(${TEST_OSQP_INTERFACE_EXE} TEST_DEPS)
  target_link_libraries(${TEST_OSQP_INTERFACE_EXE} ${PROJECT_NAME})
endif()

ament_auto_package(EXPORT_LIBRARY_TARGETS INSTALL_TO_SHARE
)
