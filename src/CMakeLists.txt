# Link against Qt modules
include(FindPkgConfig)
find_package(Qt5Core)
find_package(Qt5Widgets)

# This is need so our application will find generated
# source files.
include_directories(${CMAKE_CURRENT_BINARY_DIR})

# Application sources
set(${APP_BINARY}_SRCS
    main.cpp
    mainwindow.cpp
)

# Application headers
set(${APP_BINARY}_HDRS
    mainwindow.h
)

# Application ui-files
qt5_wrap_ui(${APP_BINARY}_UIS
    mainwindow.ui
)

# Build executable
add_executable(${APP_BINARY}
    ${${APP_BINARY}_SRCS}
    ${${APP_BINARY}_HDRS}
    ${${APP_BINARY}_UIS}
)

qt5_use_modules(${APP_BINARY} Gui Widgets)
