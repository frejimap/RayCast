cmake_minimum_required(VERSION 3.28.0)

set(This RayCastTester)

set(Sources
   ${CMAKE_CURRENT_LIST_DIR}/src/tests.cpp
)

set(Headers
)

add_executable(${This} ${Sources} ${Headers})
target_include_directories(${This} PUBLIC
    ${CMAKE_CURRENT_LIST_DIR}/include
)
target_link_libraries(${This} PUBLIC
    GTest::gtest_main
    RayCastLib
)

include(GoogleTest)
gtest_discover_tests(${This})
