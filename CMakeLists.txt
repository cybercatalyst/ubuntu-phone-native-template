project(com.nativeapp C CXX)
cmake_minimum_required(VERSION 2.8.9)

set(CMAKE_AUTOMOC ON)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -fno-permissive -pedantic -Wall -Wextra -fPIC")

# Standard install paths
include(GNUInstallDirs)

set(APP_NAME nativeapp)
set(DESKTOP_FILE "${PROJECT_NAME}.desktop")
set(ICON_FILE nativeapp64.png)
set(EXEC "${APP_NAME}")

execute_process(
    COMMAND dpkg-architecture -qDEB_HOST_MULTIARCH
    OUTPUT_VARIABLE ARCH_TRIPLET
    OUTPUT_STRIP_TRAILING_WHITESPACE
)

set(CMAKE_INSTALL_PREFIX /)
set(CMAKE_INSTALL_BINDIR /)
set(DATA_DIR /)
set(ICON ${ICON_FILE})
set(QT_IMPORTS_DIR "/lib/${ARCH_TRIPLET}")
set(BIN_DIR /lib/${ARCH_TRIPLET}/bin)
set(DESKTOP_DIR ${DATA_DIR})
set(URLS_DIR ${DATA_DIR})

configure_file(manifest.json ${CMAKE_CURRENT_BINARY_DIR}/manifest.json)
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/manifest.json apparmor.json ${CMAKE_CURRENT_BINARY_DIR}/src/${EXEC} DESTINATION ${CMAKE_INSTALL_PREFIX})

file(GLOB_RECURSE I18N_SRC_FILES
     RELATIVE ${CMAKE_CURRENT_SOURCE_DIR}
     *.desktop.in)
list(SORT I18N_SRC_FILES)

configure_file(${DESKTOP_FILE}.in ${CMAKE_CURRENT_BINARY_DIR}/${DESKTOP_FILE})
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/${DESKTOP_FILE}
    DESTINATION ${DESKTOP_DIR})

install(FILES ${URLS_FILE} DESTINATION ${URLS_DIR})

add_subdirectory(src)
