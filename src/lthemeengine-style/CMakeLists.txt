project(lthemeengine-style)

add_definitions(-DUSE_WIDGETS)

set(app_SRCS
 plugin.cpp
 lthemeengineproxystyle.cpp
 ../lthemeengine/lthemeengine.cpp
)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/../)

add_library(lthemeengine-style MODULE ${app_SRCS})
target_link_libraries(lthemeengine-style PRIVATE Qt5::Widgets)
install(TARGETS lthemeengine-style DESTINATION "${CMAKE_INSTALL_LIBDIR}"/qt/plugins/styles)
