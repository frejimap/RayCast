cmake_minimum_required(VERSION 3.28.0)
project(RayCast VERSION 0.1.0 LANGUAGES C CXX)

include(CTest)
enable_testing()

include(FetchContent)
FetchContent_Declare(SFML
    GIT_REPOSITORY https://github.com/SFML/SFML.git
    GIT_TAG 3.1.0
    GIT_SHALLOW ON
    EXCLUDE_FROM_ALL
    SYSTEM)
FetchContent_MakeAvailable(SFML)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

add_executable(RayCast src/main.cpp)

set_property(TARGET RayCast PROPERTY CXX_STANDARD 17)

target_include_directories(RayCast PUBLIC "${CMAKE_CURRENT_LIST_DIR}/include")
target_link_libraries(RayCast PRIVATE SFML::Graphics)

set_property(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY VS_STARTUP_PROJECT RayCast)
