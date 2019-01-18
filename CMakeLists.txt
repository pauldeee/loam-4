cmake_minimum_required(VERSION 2.8.3)
project(loam)

## Compile as C++11, supported in ROS Kinetic and newer
# add_compile_options(-std=c++11)

## Find catkin macros and libraries
find_package(catkin REQUIRED COMPONENTS
  roscpp
  tf
  std_msgs
  sensor_msgs
  pcl_ros
  # laser_proc
  # laser_geometry
)

find_package( PCL 1.8 REQUIRED)
find_package( OpenCV REQUIRED )

message(STATUS "Using PCL version ${PCL_VERSION}")
message(STATUS "Using catkin version ${catkin_VERSION}")

###################################
## catkin specific configuration ##
###################################
## The catkin_package macro generates cmake config files for your package
## Declare things to be passed to dependent projects
## INCLUDE_DIRS: uncomment this if your package contains header files
## LIBRARIES: libraries you create in this project that dependent projects also need
## CATKIN_DEPENDS: catkin_packages dependent projects also need
## DEPENDS: system dependencies of this project that dependent projects also need
catkin_package(
  LIBRARIES
    ${PROJECT_NAME}
  INCLUDE_DIRS
  CATKIN_DEPENDS
    std_msgs
    sensor_msgs
    pcl_ros
#  LIBRARIES test
#  DEPENDS system_lib
)

include_directories(${catkin_INCLUDE_DIRS})

###########
## Build ##
###########
## Declare a C++ executable
add_executable(scanRegistration src/scanRegistration.cpp)
target_link_libraries(scanRegistration ${catkin_LIBRARIES} ${PCL_LIBRARIES} )

add_executable(laserOdometry src/laserOdometry.cpp)
target_link_libraries(laserOdometry ${catkin_LIBRARIES} ${PCL_LIBRARIES} ${OpenCV_LIBS})

add_executable(laserMapping src/laserMapping.cpp)
target_link_libraries(laserMapping ${catkin_LIBRARIES} ${PCL_LIBRARIES} ${OpenCV_LIBS})

add_executable(transformMaintenance src/transformMaintenance.cpp)
target_link_libraries(transformMaintenance ${catkin_LIBRARIES} ${PCL_LIBRARIES} )

# For Debug
set(CMAKE_BUILD_TYPE "Debug")
