cmake_minimum_required(VERSION 3.5.0)
project(PGlab9 VERSION 0.1.0 LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 11)

# include and src dirs

include_directories("include")
file(GLOB all_SRCS
    "${PROJECT_SOURCE_DIR}/include/*.h"
    "${PROJECT_SOURCE_DIR}/include/*.hpp"
    "${PROJECT_SOURCE_DIR}/src/*.cpp"
    "${PROJECT_SOURCE_DIR}/src/*.c"
)

add_executable(PGlab9 ${all_SRCS})
target_include_directories(PGlab9 PRIVATE include/)

# GLFW

set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)

add_subdirectory("lib/glfw")
target_link_libraries(PGlab9 glfw)
find_package(OpenGL REQUIRED)
target_link_libraries(PGlab9 OpenGL::GL)

# GLEW

include_directories("lib/glew/include")
link_directories("lib/glew/lib")
add_subdirectory("lib/glew/build/cmake")

target_link_libraries(PGlab9 glew_s)

# GLM from lib folder

include_directories("lib/glm")
add_subdirectory("lib/glm")