cmake_minimum_required(VERSION 2.8.3)
project(goal_sender)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  actionlib
  geometry_msgs
  goal_sender_msgs
  move_base_msgs
  tf
  tf2
  tf2_ros
  tf2_geometry_msgs
)

###################################
## catkin specific configuration ##
###################################
catkin_package(
#  INCLUDE_DIRS include
  CATKIN_DEPENDS
    roscpp
    actionlib
    geometry_msgs
    goal_sender_msgs
    move_base_msgs
    tf
    tf2
    tf2_ros
    tf2_geometry_msgs
)

# check c++11 / c++0x
include(CheckCXXCompilerFlag)
  CHECK_CXX_COMPILER_FLAG("-std=c++11" COMPILER_SUPPORTS_CXX11)
  CHECK_CXX_COMPILER_FLAG("-std=c++0x" COMPILER_SUPPORTS_CXX0X)
if(COMPILER_SUPPORTS_CXX11)
  set(CMAKE_CXX_FLAGS "-std=c++11")
elseif(COMPILER_SUPPORTS_CXX0X)
  set(CMAKE_CXX_FLAGS "-std=c++0x")
else()
  message(FATAL_ERROR "The compiler ${CMAKE_CXX_COMPILER} has no C++11 support. Please use a different C++ compiler.")
endif()

include_directories(
  ${catkin_INCLUDE_DIRS}
)

add_executable(goal_sender_node src/goal_sender_node.cpp)
add_dependencies(goal_sender_node ${catkin_EXPORTED_TARGETS})
target_link_libraries(goal_sender_node
  ${catkin_LIBRARIES}
)

## Declare a C++ executable
add_executable(csv_goal_sender_node src/csv_goal_sender_node.cpp)
add_dependencies(csv_goal_sender_node ${catkin_EXPORTED_TARGETS})
target_link_libraries(csv_goal_sender_node
  ${catkin_LIBRARIES}
)
