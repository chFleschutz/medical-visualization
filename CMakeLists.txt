cmake_minimum_required(VERSION 3.12)

project(medical-visualization)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(Qt6 REQUIRED COMPONENTS Widgets OpenGLWidgets Charts)
if (NOT Qt6_FOUND)
    message(FATAL_ERROR "Qt6 not found. Please install Qt6.")
endif()

qt_standard_project_setup()
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)

file(GLOB_RECURSE SOURCES CONFIGURE_DEPENDS
    src/*.cpp
    src/*.h
    src/*.ui
)

qt_add_executable(medical-visualization
    ${SOURCES}
    resources.qrc
)

target_link_libraries(medical-visualization PRIVATE
    Qt6::Widgets
    Qt6::OpenGLWidgets
    Qt6::Charts
)

target_include_directories(medical-visualization PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}/src
)

set_target_properties(medical-visualization PROPERTIES
    WIN32_EXECUTABLE ON
    MACOSX_BUNDLE ON
)
