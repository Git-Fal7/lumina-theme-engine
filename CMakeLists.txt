# lumina-core/lumina-theme-engine build, CMake edition. EXPERIMENTAL.
#
# SPDX-License-Identifier: BSD-2-Clause
# SPDX-FileCopyrightText: Copyright 2022 Adriaan de Groot <adridg@FreeBSD.org>

cmake_minimum_required (VERSION 3.8.2)
set(PROJECT lumina-theme-engine)
project(${PROJECT})

# Find includes in the build directories
set(CMAKE_INCLUDE_CURRENT_DIR ON)

# Turn on automatic invocation of the MOC, UIC & RCC
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTORCC ON)

# Add a compiler flag
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall")

#Find pkgconfig
find_package(PkgConfig REQUIRED)

# Dependencies
find_package(Qt5 REQUIRED COMPONENTS Widgets X11Extras DBus ThemeSupport)
pkg_check_modules(LUMINA REQUIRED lumina)

add_subdirectory(src/lthemeengine)
add_subdirectory(src/lthemeengine-qtplugin)
add_subdirectory(src/lthemeengine-sstest)
add_subdirectory(src/lthemeengine-style)

install(
    DIRECTORY colors
    DESTINATION ${CMAKE_INSTALL_DATADIR}/lthemeengine/colors
    FILES_MATCHING
    PATTERN *.conf
)
install(
    DIRECTORY qss
    DESTINATION ${CMAKE_INSTALL_DATADIR}/lthemeengine/qss
    FILES_MATCHING
    PATTERN *.qss
)
install(
    DIRECTORY desktop_qss
    DESTINATION ${CMAKE_INSTALL_DATADIR}/lthemeengine/desktop_qss
    FILES_MATCHING
    PATTERN *.qss
)
