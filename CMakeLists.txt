cmake_minimum_required(VERSION 3.20)
project(mdvlib LANGUAGES CXX)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

include(GNUInstallDirs)

add_library(
    mdvlib
    src/library.cpp
)
target_include_directories(
    mdvlib
    PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}/include>
    $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
)

install(
    TARGETS mdvlib
    EXPORT MdvlibTargets
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    INCLUDES DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
)

install(
    EXPORT MdvlibTargets
    FILE mdvlibTargets.cmake
    NAMESPACE mdvlib::
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/mdvlib
)

install(
    DIRECTORY ${CMAKE_CURRENT_LIST_DIR}/include/
    DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
)

include(CMakePackageConfigHelpers)
configure_package_config_file(
    ${CMAKE_CURRENT_LIST_DIR}/Config.cmake.in
    ${CMAKE_CURRENT_BINARY_DIR}/mdvlibConfig.cmake
    INSTALL_DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/mdvlib
)

install(
    FILES ${CMAKE_CURRENT_BINARY_DIR}/mdvlibConfig.cmake
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/mdvlib
)
