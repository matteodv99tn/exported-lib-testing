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

set(CPACK_PACKAGE_NAME ${PROJECT_NAME})
set(CPACK_PACKAGE_VERSION "prerelease")
set(CPACK_PACKAGE_DESCRIPTION "My C++ library")
set(CPACK_PACKAGE_VENDOR "My Company")
set(CPACK_PACKAGE_CONTACT "support@mycompany.com")
# set(CPACK_RESOURCE_FILE_LICENSE "${CMAKE_SOURCE_DIR}/LICENSE")
set(CPACK_PACKAGE_HOMEPAGE_URL "https://github.com/mycompany/my_library")
set(CPACK_FILE_NAME "mdvlib")

set(CPACK_SOURCE_GENERATOR "TGZ")
set(CPACK_GENERATOR "DEB;TGZ")
set(CPACK_DEBIAN_PACKAGE_MAINTAINER "Matteo Dalle Vedove <email@example.com>")
# set(CPACK_DEBIAN_PACKAGE_DEPENDS "")
set(CPACK_DEBIAN_PACKAGE_SECTION "devl")
set(CPACK_DEBIAN_PACKAGE_PRIORITY "optional")
set(CPACK_DEB_COMPONENT_INSTALL "ON")
# set(CPACK_DEBIAN_FILE_NAME "mdvlib.deb")

include(CPack)
