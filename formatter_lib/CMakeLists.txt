cmake_minimum_required(VERSION 3.4)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
project(formatter)
add_library(formatter STATIC formatter.cpp)
target_include_directories(formatter PUBLIC )
target_link_libraries(formatter formatter_ex)
