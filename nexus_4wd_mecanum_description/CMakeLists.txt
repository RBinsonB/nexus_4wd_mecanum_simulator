cmake_minimum_required(VERSION 3.0.2)
project(nexus_4wd_mecanum_description)

find_package(catkin REQUIRED COMPONENTS
  robot_state_publisher
  urdf
)

catkin_package(
#  INCLUDE_DIRS include
#  LIBRARIES nexus_4wd_mecanum_description
  CATKIN_DEPENDS robot_state_publisher urdf
#  DEPENDS system_lib
)


include_directories(
# include
 ${catkin_INCLUDE_DIRS}
)

