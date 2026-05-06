cmake_minimum_required(VERSION 3.23)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(ray-tracer VERSION 1.0)

find_package(glfw3 REQUIRED)

# GLAD LIBRARY
add_library(GLAD dependencies/glad/src/glad.c)
target_include_directories(GLAD PUBLIC dependencies/glad/include)

# GLFW MODULE
add_library(GLFWModule INTERFACE)
target_sources(GLFWModule INTERFACE modules/graphics/GLFW_setup.hpp)
target_link_libraries(GLFWModule INTERFACE GLAD)
target_link_libraries(GLFWModule INTERFACE glfw)

# GRAPHICS MODULE
add_library(GraphicsModule INTERFACE)
target_sources(GraphicsModule INTERFACE modules/graphics/DisplayDrawer.hpp)
target_link_libraries(GraphicsModule INTERFACE GLAD)
target_include_directories(GraphicsModule INTERFACE dependencies/shader)

# CAMERA MODULE
add_library(CameraModule INTERFACE)
target_sources(CameraModule INTERFACE modules/camera/camera.hpp)
target_link_libraries(CameraModule INTERFACE GLAD)
target_include_directories(CameraModule INTERFACE dependencies/shader)

# INPUT MODULE
add_library(InputModule INTERFACE)
target_sources(InputModule INTERFACE modules/camera/processInput.hpp)
target_include_directories(InputModule INTERFACE CameraModule)
target_include_directories(InputModule INTERFACE dependencies/glm)

# MATH MODULE
add_library(MathModule INTERFACE)
target_sources(MathModule INTERFACE modules/physics/math_functions.hpp)
target_include_directories(MathModule INTERFACE dependencies/glm)


add_executable(ray-tracer version/new/main.cpp)
target_link_libraries(ray-tracer PRIVATE 
    GLFWModule     
    GraphicsModule 
    CameraModule
    InputModule
    MathModule
)
