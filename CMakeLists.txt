#
# Copyright: 2014 Jacob Dawid <jacob.dawid@cybercatalyst.net>
#
# This file is part of ubuntu-phone-native-template
#
# ubuntu-phone-native-template is free software: you can redistribute it
# and/or modify it under the terms of the GNU General Public License as
# published by the Free Software Foundation, either version 3 of the License,
# or (at your option) any later version.
#
# ubuntu-phone-native-template is distributed in the hope that it will be
# useful, but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General
# Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program.  If not, see <http://www.gnu.org/licenses/>.
#
# Authors: Jacob Dawid <jacob.dawid@cybercatalyst.net>
#

cmake_minimum_required(VERSION 2.8.9)

# App configuration
set(APP_ARCH all)
set(APP_SDK "ubuntu-sdk-14.04")
set(APP_DOMAIN net)
set(APP_VENDOR cybercatalyst)
set(APP_NAME nativeapp)
set(APP_VERSION 1.0.0)
set(APP_MAINTAINER "Example maintainer")
set(APP_DESCRIPTION "Example description")
set(APP_TARGET ${APP_NAME})
set(APP_BINARY ${APP_NAME})
set(APP_PACKAGE ${APP_DOMAIN}.${APP_VENDOR}.${APP_NAME})
set(APP_ICON_64 assets/appicon64.png)
set(APP_DESKTOP "${APP_PACKAGE}.desktop")

# Cmake configuration
set(CMAKE_AUTOMOC ON)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -fno-permissive -pedantic -Wall -Wextra -fPIC")
set(CMAKE_INSTALL_PREFIX /)
set(CMAKE_INSTALL_BINDIR /)

# Directories
set(QT_IMPORTS_DIR "/lib/${ARCH_TRIPLET}")
set(DATA_DIR /)
set(BIN_DIR /lib/${ARCH_TRIPLET}/bin)
set(DESKTOP_DIR ${DATA_DIR})

project(${APP_TARGET} C CXX)

# Standard install paths
include(GNUInstallDirs)

# ..
execute_process(
    COMMAND dpkg-architecture -qDEB_HOST_MULTIARCH
    OUTPUT_VARIABLE ARCH_TRIPLET
    OUTPUT_STRIP_TRAILING_WHITESPACE
)

configure_file(manifest.json.in ${CMAKE_CURRENT_BINARY_DIR}/manifest.json)
configure_file(apparmor.json.in ${CMAKE_CURRENT_BINARY_DIR}/${APP_DOMAIN}.${APP_VENDOR}.${APP_NAME}.json)
configure_file(desktop.in ${CMAKE_CURRENT_BINARY_DIR}/${APP_DESKTOP})
configure_file(${APP_ICON_64} ${CMAKE_CURRENT_BINARY_DIR}/${APP_NAME}64.png)

install(FILES
    ${CMAKE_CURRENT_BINARY_DIR}/${MANIFEST_JSON}
    ${CMAKE_CURRENT_BINARY_DIR}/${APPARMOR_JSON}
    ${CMAKE_CURRENT_BINARY_DIR}/src/${APP_BINARY}
        DESTINATION
    ${CMAKE_INSTALL_PREFIX}
)

install(FILES
    ${CMAKE_CURRENT_BINARY_DIR}/${APP_DESKTOP}
        DESTINATION
    ${DESKTOP_DIR}
)

# Sources
add_subdirectory(src)
