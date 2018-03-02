cmake_minimum_required(VERSION 2.8.3)
project(demo_rgbd_slimmed)

set(CMAKE_BUILD_TYPE Release)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  sensor_msgs
  std_msgs
  cv_bridge
  pcl_ros
)

find_package(Eigen3 REQUIRED QUIET)
find_package(PCL REQUIRED QUIET)
set(OpenCV_DIR $ENV{OPENCV2_INSTALL_DIR})
find_package(OpenCV 2 REQUIRED QUIET)

include_directories(
  ${catkin_INCLUDE_DIRS}
  ${OpenCV_INCLUDE_DIRS}
  ${EIGEN3_INCLUDE_DIR}
  ${PCL_INCLUDE_DIRS}
)

LIST(APPEND LINK_LIBS
  ${catkin_LIBRARIES}
  ${PCL_LIBRARIES}
  ${OpenCV_LIBRARIES}
)


catkin_package(
  CATKIN_DEPENDS roscpp std_msgs sensor_msgs cv_bridge pcl_ros
  DEPENDS EIGEN3 PCL OpenCV
)


## Declare executables
add_executable(featureTracking_rgbds src/featureTracking.cpp)
add_executable(visualOdometry_rgbds src/visualOdometry.cpp)
add_executable(processDepthmap_rgbds src/processDepthmap.cpp)

## Specify libraries to link a library or executable target against
target_link_libraries(featureTracking_rgbds ${LINK_LIBS})
target_link_libraries(visualOdometry_rgbds ${LINK_LIBS})
target_link_libraries(processDepthmap_rgbds ${LINK_LIBS})

