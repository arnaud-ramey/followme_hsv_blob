### 1 - Required CMake Version
cmake_minimum_required(VERSION 2.8.3)
### 2- Package Name
project(followme_hsv_blob)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra") # add extra warnings
### 3 - Find other CMake/Catkin packages needed for build
set(DEPS  cv_bridge  followme_laser  image_transport)
find_package(OpenCV) #  will first find OpenCV3 - http://wiki.ros.org/opencv3
find_package(catkin REQUIRED COMPONENTS  ${DEPS})
### 4 - Message/Service/Action Generators (add_message_files(), add_service_files(), add_action_files())
# Nothing in this package
### 5 - Invoke message/service/action generation (generate_messages())
# Nothing in this package
### 6 - Specify package build info export (catkin_package())
catkin_package(
  INCLUDE_DIRS
  CATKIN_DEPENDS  ${DEPS}
)
### 7 - Libraries/Executables to build (add_library()/add_executable()/target_link_libraries())
include_directories(${catkin_INCLUDE_DIRS} ${OpenCV_INCLUDE_DIRS})
add_subdirectory(src)
### 8 - Tests to build (catkin_add_gtest())
# Nothing in this package
### 9 - Install rules (install())
install(DIRECTORY include/${PROJECT_NAME}/
   DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
   FILES_MATCHING PATTERN "*.h"
   PATTERN ".svn" EXCLUDE
)
