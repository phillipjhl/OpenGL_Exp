cmake_minimum_required(VERSION 3.1)
project(3DTutorial)

# Set the C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

add_executable(3DTutorial main.cpp glad.c)

# Include GLFW headers
include_directories(/home/phillipjhl/Source/libraries/glfw/include include)

# GLFW library
add_library(glfw STATIC IMPORTED)
set_target_properties(glfw PROPERTIES
    IMPORTED_LOCATION /home/phillipjhl/Source/libraries/glfw/build/src/libglfw3.a
    INTERFACE_INCLUDE_DIRECTORIES /home/phillipjhl/Source/libraries/glfw/include
)

# Find and link the OpenGL library
find_library(OpenGL_LIB NAMES GL)
if(OpenGL_LIB)
    target_link_libraries(3DTutorial glfw ${OpenGL_LIB})
else()
    message(FATAL_ERROR "Could not find OpenGL library")
endif()