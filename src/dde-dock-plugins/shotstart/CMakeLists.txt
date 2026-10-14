# SPDX-FileCopyrightText: 2022 UnionTech Software Technology Co., Ltd.
#
# SPDX-License-Identifier: GPL-3.0-or-later

cmake_minimum_required( VERSION 3.1.0 )
# 必须是 shot-start-plugin：与自己的 gschema 模块名
# com.deepin.dde.dock.module.shot-start-plugin 一致。
# 原先写的 deepin-screen-recorder-plugin 与 recordtime 同名，两者会安装到
# 同一个 lib/dde-dock/plugins/deepin-screen-recorder-plugin.so 互相覆盖，
# 而且 dock 里按名字把 deepin-screen-recorder-plugin 排除了（那是录屏计时插件）。
set(PLUGIN_NAME "shot-start-plugin")

project(PLUGIN_NAME)

file(GLOB SRCS "*.h" "*.cpp")

find_package(PkgConfig REQUIRED)
find_package(Qt5Widgets REQUIRED)
find_package(Qt5Svg REQUIRED)
find_package(Qt5DBus REQUIRED)
find_package(DtkWidget REQUIRED)

pkg_check_modules(QGSettings REQUIRED gsettings-qt)

add_definitions("${QT_DEFINITIONS} -DQT_PLUGIN")
add_library(${PLUGIN_NAME} SHARED ${SRCS} res.qrc)
target_include_directories(${PLUGIN_NAME} PUBLIC
    ${DtkWidget_INCLUDE_DIRS}
    ${QGSettings_INCLUDE_DIRS}
    )
target_link_libraries(${PLUGIN_NAME} PRIVATE
    ${Qt5DBus_LIBRARIES}
    ${DtkWidget_LIBRARIES}
    ${Qt5Widgets_LIBRARIES}
    ${Qt5Svg_LIBRARIES}
    ${QGSettings_LIBRARIES}
    )

set(CMAKE_INSTALL_PREFIX "/usr")
install(TARGETS ${PLUGIN_NAME} LIBRARY DESTINATION lib/dde-dock/plugins)
