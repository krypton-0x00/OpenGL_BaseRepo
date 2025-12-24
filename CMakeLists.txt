cmake_minimum_required(VERSION 3.10)
project(OpenGLProject)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Set source files
set(SOURCES
    src/main.cpp
    src/glad.c
)

# Include GLAD headers
include_directories(include)

# Find GLFW
find_package(glfw3 REQUIRED)
find_package(glm REQUIRED)

# If glfw3 not found, try pkg-config
if (NOT glfw3_FOUND)
    find_package(PkgConfig REQUIRED)
    pkg_check_modules(GLFW REQUIRED glfw3)
    include_directories(${GLFW_INCLUDE_DIRS})
endif()

# Find OpenGL
find_package(OpenGL REQUIRED)

# Create executable
add_executable(opengl_app ${SOURCES})

# Link libraries
target_link_libraries(opengl_app
    OpenGL::GL
    glfw
    glm::glm
)

