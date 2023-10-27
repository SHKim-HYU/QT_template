cmake_minimum_required(VERSION 3.8)
project(Qt_template LANGUAGES C CXX)

# Set C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Find includes in the build directories and the include directory
set(CMAKE_INCLUDE_CURRENT_DIR ON)

# Find the QtWidgets library
find_package(Qt5 COMPONENTS Widgets Core Quick REQUIRED)

# Enable automatic UIC compilation
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTORCC ON)

set(QTWIDGET_HEADERS_DIR ${PROJECT_SOURCE_DIR}/include/QtWidgets)
set(DARKSTYLE_HEADERS_DIR ${PROJECT_SOURCE_DIR}/include/DarkStyleWindow)

include_directories(
    ${QTWIDGET_HEADERS_DIR}
    ${DARKSTYLE_HEADERS_DIR}
)

add_subdirectory(include/QtWidgets)
add_subdirectory(include/DarkStyleWindow)

# Source files
set(SOURCE_FILES
    src/main.cpp
    src/mainwindow.cpp
    src/mainwindow.ui
)

# Add a executable with the above sources
add_executable(${PROJECT_NAME} ${SOURCE_FILES})

target_link_libraries(${PROJECT_NAME}
    sub::QtWidgets
    sub::DarkStyleWindow
)

# Use the Widgets module from Qt 5
target_link_libraries(${PROJECT_NAME} 
    Qt5::Widgets 
    Qt5::Core
    Qt5::Gui
    Qt5::Network
    Qt5::Quick
)