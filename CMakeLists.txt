cmake_minimum_required(VERSION 2.8.12 FATAL_ERROR)
#-------------------------------------------------------------------------------
# Set Build Type
#-------------------------------------------------------------------------------
set(CMAKE_BUILD_TYPE Release)
add_definitions(-std=c++11)

project(shenzhen_cross)

set(CMAKE_INCLUDE_CURRENT_DIR ON)


    include_directories(
        ${CMAKE_CURRENT_SOURCE_DIR}
        ${CMAKE_CURRENT_SOURCE_DIR}/include
        ${CMAKE_CURRENT_SOURCE_DIR}/include/libconfig/
        ${CMAKE_CURRENT_SOURCE_DIR}/include/cjson/
        ${CMAKE_CURRENT_SOURCE_DIR}/include/eigen3/
        ${CMAKE_CURRENT_SOURCE_DIR}/include/base/
        ${CMAKE_CURRENT_SOURCE_DIR}/include/utils/
        ${CMAKE_CURRENT_SOURCE_DIR}/include/lidar
        ${CMAKE_CURRENT_SOURCE_DIR}/include/google
        ${CMAKE_CURRENT_SOURCE_DIR}/include/lidar/proto
    )

find_package(Boost COMPONENTS system REQUIRED)
include_directories(${BOOST_INCLUDE_DIRS})

add_subdirectory(./include/cjson)
add_subdirectory(./include/utils)
#add_subdirectory(./include/eigen3)
add_subdirectory(./include/base)
add_subdirectory(./include/lidar)
aux_source_directory(. SRC)
#link_directories(./lib /usr/local/boost1_54_lib)
link_directories(./lib)
add_executable(fusion_sj ${SRC})
target_link_libraries(fusion_sj lidar config++ cJson ${CMAKE_CURRENT_SOURCE_DIR}/lib/libboost_system.a base utils)

