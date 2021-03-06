project(PlotJuggler)
cmake_minimum_required(VERSION 2.8)

link_directories( /usr/lib/x86_64-linux-gnu )

find_package(Qt5 REQUIRED COMPONENTS Core Widgets PrintSupport Concurrent Xml)


set(CMAKE_AUTOMOC ON)
SET(CMAKE_AUTOUIC ON)
set(CMAKE_INCLUDE_CURRENT_DIR ON)


set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -fPIC")

include_directories(
    ${Qt5Widgets_INCLUDE_DIRS}
    ${Qt5Concurrent_INCLUDE_DIRS}
    ${Qt5PrintSupport_INCLUDE_DIRS}
    ${Qt5Xml_INCLUDE_DIRS}
    #${Qt5OpenGl_INCLUDE_DIRS}
    )


include_directories( ./qwt/src ./common ./color_widgets/include ./plotter_gui)


set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)



SET(CMAKE_INSTALL_PREFIX  "/usr/local" )

add_subdirectory( common)
add_subdirectory( color_widgets )
add_subdirectory( qwt/src )
add_subdirectory( plotter_gui )

add_subdirectory( plugins/DataLoadCSV )
add_subdirectory( plugins/DataStreamSample )

INSTALL(FILES plugins/statepublisher_base.h DESTINATION ${CMAKE_INSTALL_PREFIX}/include/PlotJuggler )
INSTALL(FILES plugins/dataloader_base.h DESTINATION     ${CMAKE_INSTALL_PREFIX}/include/PlotJuggler )
INSTALL(FILES plugins/datastreamer_base.h DESTINATION   ${CMAKE_INSTALL_PREFIX}/include/PlotJuggler )

#########################  create a package ####################################

SET(CPACK_GENERATOR "TGZ;DEB")
SET(CPACK_DEBIAN_PACKAGE_MAINTAINER "Davide Faconti")
SET(CPACK_PACKAGE_CONTACT "faconti@icarustechnology.com")


SET(CPACK_PACKAGING_INSTALL_PREFIX "/usr/local/")
SET(CPACK_INCLUDE_TOPLEVEL_DIRECTORY 0)

SET(CPACK_PACKAGE_DESCRIPTION_SUMMARY "PlotJuggler: juggle with data")
SET(CPACK_PACKAGE_VENDOR "Icarus Technology")

SET(CPACK_PACKAGE_VERSION_MAJOR "0")
SET(CPACK_PACKAGE_VERSION_MINOR "2")
SET(CPACK_PACKAGE_VERSION_PATCH "0")
SET(CPACK_PACKAGE_VERSION "0.2.0")

SET(CPACK_PACKAGE_NAME "plotjuggler${CPACK_DEBIAN_PACKAGE_ARCHITECTURE}")

SET(CPACK_DEBIAN_PACKAGE_DEPENDS "qt5-default libqt5core5a libqt5concurrent5 libqt5gui5 libqt5opengl5 libqt5printsupport5 libqt5xml5")

set(CPACK_PACKAGE_INSTALL_DIRECTORY "PlotJuggler")

INCLUDE(CPack)
