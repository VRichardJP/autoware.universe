cmake_minimum_required(VERSION 3.14)
project(control_performance_analysis)

find_package(autoware_cmake REQUIRED)
autoware_package(USE_AMENT_EX)

ament_ex_find_package(Eigen3 REQUIRED)

rosidl_generate_interfaces(
        control_performance_analysis
        "msg/Error.msg"
        "msg/ErrorStamped.msg"
        "msg/DrivingMonitorStamped.msg"
        "msg/FloatStamped.msg"
        DEPENDENCIES builtin_interfaces std_msgs
)

ament_ex_add_library(
        control_performance_analysis_core SHARED
        src/control_performance_analysis_utils.cpp
        src/control_performance_analysis_core.cpp
)
target_link_libraries(control_performance_analysis_core
        Eigen3::Eigen
)

ament_ex_add_library(
        control_performance_analysis_node SHARED
        src/control_performance_analysis_node.cpp
)

if(${rosidl_cmake_VERSION} VERSION_LESS 2.5.0)
    rosidl_target_interfaces(control_performance_analysis_node
            control_performance_analysis "rosidl_typesupport_cpp")
    rosidl_target_interfaces(control_performance_analysis_core
            control_performance_analysis "rosidl_typesupport_cpp")
else()
    rosidl_get_typesupport_target(
            cpp_typesupport_target control_performance_analysis "rosidl_typesupport_cpp")
    target_link_libraries(control_performance_analysis_node "${cpp_typesupport_target}")
    target_link_libraries(control_performance_analysis_core "${cpp_typesupport_target}")
endif()

target_link_libraries(
        control_performance_analysis_node
        control_performance_analysis_core
)

rclcpp_components_register_node(
        control_performance_analysis_node
        PLUGIN "control_performance_analysis::ControlPerformanceAnalysisNode"
        EXECUTABLE control_performance_analysis_exe
)

ament_ex_package(
        INSTALL_TO_SHARE
        launch
        config
)
