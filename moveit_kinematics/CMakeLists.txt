cmake_minimum_required(VERSION 3.10.2)
project(moveit_kinematics)

add_compile_options(-std=c++14)

find_package(ament_cmake REQUIRED)

find_package(Boost REQUIRED)
find_package(Eigen3 REQUIRED)
find_package(orocos_kdl REQUIRED)
find_package(tf2_kdl REQUIRED)
find_package(kdl_parser REQUIRED)
find_package(rclcpp REQUIRED)
find_package(random_numbers REQUIRED)
find_package(class_loader REQUIRED)
find_package(pluginlib REQUIRED)
find_package(moveit_core REQUIRED)
find_package(moveit_ros_planning REQUIRED)
find_package(moveit_msgs REQUIRED)

set(THIS_PACKAGE_INCLUDE_DIRS
    kdl_kinematics_plugin/include
    lma_kinematics_plugin/include
    srv_kinematics_plugin/include
    # cached_ik_kinematics_plugin/include
)

pluginlib_export_plugin_description_file(moveit_core kdl_kinematics_plugin_description.xml)
ament_export_libraries(${PROJECT_NAME} kdl_kinematics_plugin)

include_directories(${THIS_PACKAGE_INCLUDE_DIRS}
  ${rclcpp_INCLUDE_DIRS}
  ${tf2_kdl_INCLUDE_DIRS}
  ${class_loader_INCLUDE_DIRS}
  ${random_numbers_INCLUDE_DIRS}
  ${moveit_msgs_INCLUDE_DIRS}
  ${moveit_core_INCLUDE_DIRS}
)

include_directories(SYSTEM ${EIGEN3_INCLUDE_DIRS}
)


add_subdirectory(kdl_kinematics_plugin)
add_subdirectory(lma_kinematics_plugin)
add_subdirectory(srv_kinematics_plugin)
# add_subdirectory(ikfast_kinematics_plugin)
# add_subdirectory(cached_ik_kinematics_plugin)
add_subdirectory(test)

ament_export_include_directories(include)
ament_export_dependencies(pluginlib)
ament_export_dependencies(moveit_core)
ament_export_dependencies(moveit_ros_planning)
ament_package()
