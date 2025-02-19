cmake_minimum_required (VERSION 3.16)

project (Object-Viewer)

set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Werror -std=c++17")
set (source_dir "${PROJECT_SOURCE_DIR}/src/")
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin)

find_package(glfw3 3.3 REQUIRED)
find_package(OpenGL REQUIRED)
find_package(GLEW REQUIRED)

file (GLOB source_files "${source_dir}/*.cpp" 
	"${source_dir}/deps/*.cpp" 
	"${source_dir}/deps/*/*.cpp"
	"${source_dir}/deps/imgui/backends/imgui_impl_opengl3.cpp"
	"${source_dir}/deps/imgui/backends/imgui_impl_glfw.cpp")

add_executable (viewer ${source_files})
target_include_directories(viewer PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/src)
target_include_directories(viewer PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/src/deps/imgui)
target_link_libraries(viewer glfw)
target_link_libraries(viewer OpenGL::GL)
target_link_libraries(viewer GLEW)
