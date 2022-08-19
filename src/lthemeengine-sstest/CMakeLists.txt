# lumina-core/lumina-theme-engine/lthemeengine-sstest build, CMake edition. EXPERIMENTAL.
#
# SPDX-License-Identifier: BSD-2-Clause
# SPDX-FileCopyrightText: Copyright 2022 Adriaan de Groot <adridg@FreeBSD.org>

add_executable(lthemeengine-sstest main.cpp)
target_link_libraries(lthemeengine-sstest PRIVATE ${LUMINA_LIBRARIES} Qt5::Widgets)

# Include header files
include_directories(
    ${LUMINA_INCLUDE_DIRS}
)

install(TARGETS lthemeengine-sstest)
