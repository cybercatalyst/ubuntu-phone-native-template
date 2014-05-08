include(FindPkgConfig)

# Qt modules
find_package(Qt5Core)
find_package(Qt5Widgets)

include_directories(${CMAKE_CURRENT_BINARY_DIR})

# Application sources
set(nativeapp_SRCS
    main.cpp
    mainwindow.cpp
)

# Application headers
set(nativeapp_HDRS
    mainwindow.h
)

# Application ui-files
qt5_wrap_ui(uic_HDRS
    mainwindow.ui
)

# Build executable
add_executable(${APP_NAME}
    ${nativeapp_SRCS}
    ${nativeapp_HDRS}
    ${uic_HDRS}
)

# Link against Qt modules
qt5_use_modules(${APP_NAME} Gui Widgets)
