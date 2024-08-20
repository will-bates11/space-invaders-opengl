cmake_minimum_required(VERSION 3.10)

# Set the project name and version
project(SpaceInvadersOpenGL VERSION 1.0)

# Set C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Define the executable output path
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR}/bin)

# Find required packages
find_package(OpenGL REQUIRED)
find_package(GLEW REQUIRED)
find_package(GLFW3 REQUIRED)

# Include directories
include_directories(${OPENGL_INCLUDE_DIRS} ${GLEW_INCLUDE_DIRS} ${GLFW3_INCLUDE_DIRS})

# Add source files
set(SOURCES
    src/main.cpp
)

# Add the executable
add_executable(SpaceInvaders ${SOURCES})

# Link libraries
target_link_libraries(SpaceInvaders ${OPENGL_LIBRARIES} ${GLEW_LIBRARIES} glfw)

# Set the startup project for Visual Studio
set_property(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY VS_STARTUP_PROJECT SpaceInvaders)

# Post-build steps to copy assets to the output directory
add_custom_command(TARGET SpaceInvaders POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory
    ${CMAKE_SOURCE_DIR}/assets $<TARGET_FILE_DIR:SpaceInvaders>/assets
)
