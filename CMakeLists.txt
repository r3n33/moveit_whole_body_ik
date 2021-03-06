cmake_minimum_required(VERSION 2.8.3)
project(moveit_whole_body_ik)

find_package(Boost REQUIRED system thread)

find_package(catkin REQUIRED COMPONENTS
  moveit_ros_robot_interaction
  moveit_visual_tools
  moveit_core
  moveit_ros_planning
  cmake_modules
  pluginlib
  roscpp
  srdfdom
  urdf
)
find_package(Eigen REQUIRED)
find_package(LAPACK REQUIRED)

catkin_package(
  LIBRARIES

  INCLUDE_DIRS
    whole_body_kinematics_plugin/include
  CATKIN_DEPENDS
    moveit_ros_robot_interaction
    moveit_visual_tools
    pluginlib
    moveit_core
    moveit_ros_planning
)

include_directories(whole_body_kinematics_plugin/include
                    ${catkin_INCLUDE_DIRS}
		    )

include_directories(SYSTEM
                    ${EIGEN_INCLUDE_DIRS}
                    ${Boost_INCLUDE_DIRS}
                    )

link_directories(${Boost_LIBRARY_DIRS})
link_directories(${catkin_LIBRARY_DIRS})

add_subdirectory(whole_body_kinematics_plugin)

install(
  FILES
    whole_body_kinematics_plugin_description.xml
  DESTINATION
    ${CATKIN_PACKAGE_SHARE_DESTINATION})
