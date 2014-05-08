include(FindPkgConfig)
find_package(Qt5Core)
find_package(Qt5Widgets)

set(nativeapp_SRCS
    main.cpp
    mainwindow.cpp
    mainwindow.h
    mainwindow.ui
)

add_executable(nativeapp ${nativeapp_SRCS})

qt5_use_modules(nativeapp Gui Widgets)

