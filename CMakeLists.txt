cmake_minimum_required(VERSION 3.10.0)
project(RayCast VERSION 0.1.0 LANGUAGES C CXX)

include(CTest)
enable_testing()

add_executable(RayCast src/main.cpp)

target_include_directories(RayCast PUBLIC include)

set_property(TARGET RayCast PROPERTY CXX_STANDARD 17)
