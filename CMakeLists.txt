cmake_minimum_required(VERSION 3.2)

# Set the project name and language
project(cpong C)

# Set the C standard
set(CMAKE_C_STANDARD 23)

# Use clang as the compiler
set(CMAKE_C_COMPILER "clang")
set(CMAKE_CXX_COMPILER "clang++")

# Specify the output directory for the build artifacts
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/../build)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/../build)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/../build)

# Set custom compiler flags for development
set(CUSTOM_CFLAGS "-Wall -Wextra -Wpedantic -Wshadow -Wformat=2 -Wconversion -Wuninitialized -Wstrict-overflow=5 -Wstrict-aliasing -fstrict-aliasing -ffunction-sections -fdata-sections")

# Apply the custom compiler flags
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${CUSTOM_CFLAGS}")

# Include directories for headers
include_directories(${CMAKE_SOURCE_DIR}/include)

# Source files
file(GLOB_RECURSE SOURCES ${CMAKE_SOURCE_DIR}/src/*.c)

# Add the executable
add_executable(${PROJECT_NAME} ${SOURCES})

# Link SDL2
find_package(SDL2 REQUIRED)
include_directories(${SDL2_INCLUDE_DIRS})
target_link_libraries(${PROJECT_NAME} ${SDL2_LIBRARIES})

# Apply the custom compiler flags to the target
target_compile_options(${PROJECT_NAME} PRIVATE ${CUSTOM_CFLAGS})
