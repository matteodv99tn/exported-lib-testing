cmake_minimum_required(VERSION 3.20)
project(userlibrary LANGUAGES CXX)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

find_package(mdvlib REQUIRED)

add_executable(
    main
    main.cpp
)
target_link_libraries(
    main
    mdvlib::mdvlib
)
