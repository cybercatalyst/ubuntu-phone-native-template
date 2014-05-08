include(FindPkgConfig)
include_directories(${CMAKE_CURRENT_BINARY_DIR})

find_package(Qt5Core)
find_package(Qt5Widgets)

set(nativeapp_SRCS
    main.cpp
    mainwindow.cpp
)

set(nativeapp_HDRS
    mainwindow.h
)

qt5_wrap_ui(uic_HDRS
    mainwindow.ui
)

add_executable(nativeapp
    ${nativeapp_SRCS}
    ${nativeapp_HDRS}
    ${uic_HDRS}
)

qt5_use_modules(nativeapp Gui Widgets)

