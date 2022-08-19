cmake_minimum_required(VERSION 3.11.0)

project(lumina-theme-engine LANGUAGES CXX)

include(GNUInstallDirs)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_VISIBILITY_PRESET hidden)
set(CMAKE_VISIBILITY_INLINES_HIDDEN 1)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)
set(QT_MINIMUM_VERSION "5.12.0")

ADD_DEFINITIONS(-DQT_DISABLE_DEPRECATED_BEFORE=0x050C00 -DUSE_WIDGETS)

#Find pkgconfig
find_package(PkgConfig REQUIRED)

find_package(Qt5 ${QT_MINIMUM_VERSION} COMPONENTS Widgets Concurrent LinguistTools DBus ThemeSupport X11Extras REQUIRED)
find_package(Qt5Gui ${QT_MINIMUM_VERSION} CONFIG REQUIRED Private)

pkg_check_modules(LUMINA REQUIRED lumina)

get_target_property(QT_LRELEASE_EXECUTABLE Qt5::lrelease IMPORTED_LOCATION)

if(QT_LRELEASE_EXECUTABLE)
    message(STATUS "Found lrelease executable: " ${QT_LRELEASE_EXECUTABLE})
else()
    message(FATAL_ERROR "Could NOT find lrelease executable")
endif()

get_filename_component(QT_QTPATHS_EXECUTABLE ${QT_LRELEASE_EXECUTABLE} DIRECTORY)
set(QT_QTPATHS_EXECUTABLE ${QT_QTPATHS_EXECUTABLE}/qtpaths)

if(EXISTS ${QT_QTPATHS_EXECUTABLE})
    message(STATUS "Found qtpaths executable: " ${QT_QTPATHS_EXECUTABLE})
else()
    message(FATAL_ERROR "Could NOT find qtpaths executable")
endif()

execute_process(COMMAND ${QT_QTPATHS_EXECUTABLE} --plugin-dir OUTPUT_VARIABLE PLUGINDIR OUTPUT_STRIP_TRAILING_WHITESPACE)
message(STATUS "Plugin path: " ${PLUGINDIR})

add_subdirectory(src/lthemeengine)
add_subdirectory(src/lthemeengine-qtplugin)
add_subdirectory(src/lthemeengine-sstest)
add_subdirectory(src/lthemeengine-style)

install(DIRECTORY qss DESTINATION ${CMAKE_INSTALL_DATADIR}/lthemeengine)
install(DIRECTORY desktop_qss DESTINATION ${CMAKE_INSTALL_DATADIR}/lthemeengine)
install(DIRECTORY colors DESTINATION ${CMAKE_INSTALL_DATADIR}/lthemeengine)
