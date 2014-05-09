cmake_minimum_required(VERSION 2.8.9)

# App configuration
set(APP_DOMAIN net)
set(APP_VENDOR cybercatalyst)
set(APP_NAME nativeapp)
set(APP_VERSION 1.0.0)
set(APP_TARGET ${APP_NAME})
set(APP_BINARY ${APP_NAME})
set(APP_PACKAGE ${APP_DOMAIN}.${APP_VENDOR}.${APP_NAME})
set(APP_ICON nativeapp64.png)
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

# Application manifest
configure_file(manifest.json
    ${CMAKE_CURRENT_BINARY_DIR}/manifest.json
)

install(FILES
    ${CMAKE_CURRENT_BINARY_DIR}/manifest.json apparmor.json
    ${CMAKE_CURRENT_BINARY_DIR}/src/${APP_BINARY}
        DESTINATION
    ${CMAKE_INSTALL_PREFIX}
)

# Desktop Link
configure_file(${APP_DESKTOP}.in
    ${CMAKE_CURRENT_BINARY_DIR}/${APP_DESKTOP}
)

install(FILES
    ${CMAKE_CURRENT_BINARY_DIR}/${APP_DESKTOP}
        DESTINATION
    ${DESKTOP_DIR}
)

# Sources
add_subdirectory(src)
