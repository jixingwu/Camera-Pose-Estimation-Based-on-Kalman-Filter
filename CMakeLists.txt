cmake_minimum_required(VERSION 2.8)
project(directBA)

set(CMAKE_BUILD_TYPE Release)
set(CMAKE_CXX_FLAGS "-std=c++11")

#opencv
find_package(OpenCV REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})

#sophus
find_package(Sophus REQUIRED)
set(Sophus_LIBRARIES libSophus.so)
include_directories(${Sophus_INCLUDE_DIRS})

#eigen
include_directories("/usr/include/eigen3")

#pangolin
find_package(Pangolin REQUIRED)
include_directories(${Pangolin_INCLUDE_DIRS})

#G2O
list( APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake_modules )
set(G2O_ROOT /usr/local/include/g2o)
find_package(G2O REQUIRED)
include_directories(${G2O_INCLUDE_DIRS})
#include_directories("/usr/local/include/g2o")

add_executable(directBA_node directBA.cpp)
target_link_libraries(directBA_node
        ${OpenCV_LIBRARIES}
        ${Pangolin_LIBRARIES}
        ${Sophus_LIBRARIES}
        ${G2O_LIBARIES}
 ${G2O_CORE_LIBRARY} ${G2O_STUFF_LIBRARY} ${G2O_TYPES_SLAM3D} ${G2O_TYPES_SBA})
