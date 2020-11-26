cmake_minimum_required(VERSION 3.5)
project(vstgui-drawing-example)

if(UNIX AND NOT APPLE)
    set(LINUX TRUE)
endif()

if(WIN32)
  add_definitions(-DUNICODE)
  add_definitions(-D_UNICODE)
endif()

add_subdirectory(vstgui/vstgui EXCLUDE_FROM_ALL)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/${CMAKE_BUILD_TYPE}/$<0:>")
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/${CMAKE_BUILD_TYPE}/libs/$<0:>")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/${CMAKE_BUILD_TYPE}/libs/$<0:>")

##########################################################################################
# VSTGUI drawing Example Application
##########################################################################################
set(target drawing)

set(${target}_sources
  source/drawing.cpp
  source/drawing.h
  source/drawingarea.cpp
  source/drawingarea.h
)

set(drawing_resources
  resource/Window.uidesc
)

set(drawing_font
)

##########################################################################################
vstgui_add_executable(${target} "${${target}_sources}" )
vstgui_add_resources(${target} "${drawing_resources}")
vstgui_add_resources(${target} "${drawing_font}" "Fonts")
vstgui_set_target_infoplist(${target} "resource/Info.plist")
vstgui_set_target_rcfile(${target} "resource/drawing.rc")
vstgui_set_cxx_version(${target} 14)
target_include_directories(${target} PRIVATE "vstgui")
