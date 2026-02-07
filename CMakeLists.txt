cmake_minimum_required(VERSION 3.16)

# Declare project name
project(handmade_hero)

# Set the output directory for built projects
# This makes sure that the dynamic lib goes into the build directory automatically
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/$<CONFIGURATION>")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/$<CONFIGURATION>")

# Prevent installing to system directories
set(CMAKE_INSTALL_PREFIX "${CMAKE_BINARY_DIR}" CACHE INTERNAL "")

# Set executable name into a variable
set(EXECUTABLE_NAME ${PROJECT_NAME})

find_package(SDL3 REQUIRED CONFIG REQUIRED COMPONENTS SDL3-shared)
find_package(SDL3_ttf)

add_executable(${EXECUTABLE_NAME})

# Adding sources to the target
target_sources(${EXECUTABLE_NAME} PRIVATE src/main.cpp)

# Set C++ ver
target_compile_features(${EXECUTABLE_NAME} PUBLIC cxx_std_20)

# Link SDL to our own exes. This also makes its include directory available to us
target_link_libraries(${EXECUTABLE_NAME} PUBLIC SDL3_ttf::SDL3_ttf SDL3::SDL3)
