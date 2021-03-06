cmake_minimum_required(VERSION 2.8.3)
project(navigation)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  std_msgs
  geometry_msgs
  sensor_msgs
  rtklib_msgs
  eagleye_msgs
  coordinate
)

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES navigation
)

include_directories(
  include
  ${PROJECT_SOURCE_DIR}/include
  ${catkin_INCLUDE_DIRS}
)

add_library(navigation
  src/velocity_scale_factor.cpp
  src/distance.cpp
  src/yawrate_offset_stop.cpp
  src/yawrate_offset.cpp
  src/heading.cpp
  src/position.cpp
  src/slip_angle.cpp
  src/smoothing.cpp
  src/trajectory.cpp
  src/heading_interpolate.cpp
  src/position_interpolate.cpp
  src/height.cpp
  src/angular_velocity_offset_stop.cpp
)

target_link_libraries(navigation
  ${catkin_LIBRARIES}
)

install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.hpp"
)

install(TARGETS navigation
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
