project(lthemeengine-qtplugin)

set(SRC
  main.cpp
  lthemeengineplatformtheme.cpp
  ../lthemeengine/lthemeengine.cpp
)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/../)

add_library(lthemeengine-qtplugin MODULE ${SRC})
set_target_properties(lthemeengine-qtplugin PROPERTIES OUTPUT_NAME lthemeengine)
target_link_libraries(lthemeengine-qtplugin PRIVATE Qt5::Widgets Qt5::GuiPrivate Qt5::DBus Qt5::ThemeSupportPrivate Qt5::X11Extras)
install(TARGETS lthemeengine-qtplugin DESTINATION "${CMAKE_INSTALL_LIBDIR}"/qt/plugins/platformthemes)
