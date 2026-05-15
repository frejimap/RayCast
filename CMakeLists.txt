cmake_minimum_required(VERSION 3.28.0)

set(This RayCast)
set(ThisLib ${This}Lib)
project(${This} VERSION 0.1.0 LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

include(FetchContent)
# fetch SFML
FetchContent_Declare(SFML
    GIT_REPOSITORY https://github.com/SFML/SFML.git
    GIT_TAG 3.1.0
    GIT_SHALLOW ON
    EXCLUDE_FROM_ALL
    SYSTEM)
FetchContent_MakeAvailable(SFML)
# fetch google test
FetchContent_Declare(
    googletest
    GIT_REPOSITORY https://github.com/google/googletest.git
    GIT_TAG v1.17.0
    GIT_SHALLOW ON
)
# For Windows: Prevent overriding the parent project's compiler/linker settings
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)

enable_testing()

set(Headers
    ${CMAKE_CURRENT_LIST_DIR}/include/core.hpp
)

set(Sources
    ${CMAKE_CURRENT_LIST_DIR}/src/core.cpp
)

# create core library
add_library(${ThisLib} STATIC ${Sources} ${Headers})
target_include_directories(${ThisLib} PUBLIC ${CMAKE_CURRENT_LIST_DIR}/include)
target_link_libraries(${ThisLib} PRIVATE SFML::Graphics)

# google tests
add_subdirectory(gtests)

# compile executable
add_executable(${This} src/main.cpp)
target_include_directories(${This} PUBLIC ${CMAKE_CURRENT_LIST_DIR}/include)
target_link_libraries(${This} ${ThisLib})

set_property(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY VS_STARTUP_PROJECT ${This})
