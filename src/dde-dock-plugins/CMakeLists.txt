# SPDX-FileCopyrightText: 2022 UnionTech Software Technology Co., Ltd.
#
# SPDX-License-Identifier: GPL-3.0-or-later

cmake_minimum_required( VERSION 3.1.0 )
set (PROJECT_NAME dde-dock-plugins)
project( ${PROJECT_NAME} )

add_subdirectory(recordtime)
# 截图快捷面板插件（shot-start-plugin）：此前因与 recordtime 同名而未构建
add_subdirectory(shotstart)



