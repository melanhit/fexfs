cmake_minimum_required(VERSION 3.0)
project(FexFS C)

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release)
endif()

include_directories(src)
add_subdirectory(src)
