cmake_minimum_required(VERSION 3.10)
project(ProjectWithLibrary)

# Set output directory for the final binary
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/../run)

# Include headers
include_directories(inc)

# Create a static library from the tools source
add_library(utils STATIC
    lib/tools.cpp
)

# Add main executable and link with the utils library
add_executable(greetings
    src/greetings.cpp
)

target_link_libraries(greetings PRIVATE utils)
