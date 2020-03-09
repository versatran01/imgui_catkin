cmake_minimum_required(VERSION 3.10)
project(imgui_catkin)

find_package(catkin REQUIRED)
find_package(GLEW REQUIRED)
find_package(OpenGL REQUIRED)
find_package(glfw3 REQUIRED)

catkin_package(INCLUDE_DIRS include LIBRARIES ${PROJECT_NAME} CATKIN_DEPENDS
               DEPENDS)

add_library(
  ${PROJECT_NAME} SHARED
  src/imgui.cpp src/imgui_demo.cpp src/imgui_draw.cpp src/imgui_widgets.cpp
  src/imgui_impl_glfw.cpp src/imgui_impl_opengl3.cpp)
target_include_directories(${PROJECT_NAME} PUBLIC include)
target_include_directories(${PROJECT_NAME} PRIVATE include/imgui)
target_compile_features(${PROJECT_NAME} INTERFACE cxx_std_17)
target_link_libraries(${PROJECT_NAME} PUBLIC glfw GLEW::glew OpenGL::GL)

add_executable(imgui_demo_opengl3 src/demo_opengl3.cpp)
target_link_libraries(imgui_demo_opengl3 PUBLIC ${PROJECT_NAME})
