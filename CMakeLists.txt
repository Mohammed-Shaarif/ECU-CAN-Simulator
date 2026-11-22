cmake_minimum_required(VERSION 3.16)

project(AutomotiveECUSimulator LANGUAGES CXX)
add_compile_options(
    -Wall
    -Wextra
    -Wconversion
)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

include(CTest)

find_package(GTest REQUIRED)

add_executable(hello_test
    tests/hello_test.cpp
)

target_link_libraries(hello_test
    PRIVATE
    GTest::gtest_main
)

include(GoogleTest)
gtest_discover_tests(hello_test)
