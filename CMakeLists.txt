cmake_minimum_required(VERSION 3.10 FATAL_ERROR)
project(StickyProject)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_POSITION_INDEPENDENT_CODE TRUE)

# Try to find Nuke installation
if(WIN32)
    if(NOT DEFINED NUKE_INSTALL_PATH)
        set(NUKE_INSTALL_PATH "C:/Program Files/Nuke${NUKE_VERSION}")
    endif()
    
    include_directories(${NUKE_INSTALL_PATH}/include)
    link_directories(${NUKE_INSTALL_PATH})
endif()

# Build the plugin
add_library(StickyProject SHARED StickyProject.cpp)

if(WIN32)
    target_link_libraries(StickyProject DDImage)
    set_target_properties(StickyProject PROPERTIES SUFFIX ".dll")
endif()

# Set output directory
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib/Release)
