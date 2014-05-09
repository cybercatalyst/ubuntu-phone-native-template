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
