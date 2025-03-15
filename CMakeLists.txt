cmake_minimum_required(VERSION 3.15)
project(GraphicsExamples)

set(CMAKE_CXX_STANDARD 20)

# dev
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

add_compile_definitions(ASSET_PATH="$${CMAKE_SOURCE_DIR}/assets")

# dependencies

include_directories(third_party)

## GLAD
add_library(glad STATIC third_party/glad/src/glad.c)
target_include_directories(glad PUBLIC third_party/glad/include)

## GLFW
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "")
set(GLFW_BUILD_TESTS OFF CACHE BOOL "")
set(GLFW_BUILD_DOCS OFF CACHE BOOL "")
set(GLFW_INSTALL OFF CACHE BOOL "")
add_subdirectory(third_party/glfw)

## ImGui
file(GLOB IMGUI_SRC_FILES third_party/imgui/*.cpp)
file(GLOB IMGUI_H_FILES third_party/imgui/*.h)
add_library(imgui STATIC ${IMGUI_SRC_FILES} ${IMGUI_H_FILES})
target_include_directories(imgui PUBLIC third_party/imgui)

## stb
include_directories(third_party/stb)

## Assimp
set(ASSIMP_NO_EXPORT ON CACHE BOOL "")
set(ASSIMP_BUILD_DRACO OFF CACHE BOOL "")
set(ASSIMP_BUILD_ASSIMP_TOOLS OFF CACHE BOOL "")
set(ASSIMP_BUILD_TESTS OFF CACHE BOOL "")
set(ASSIMP_INSTALL_PDB OFF CACHE BOOL "")
set(ASSIMP_WARNINGS_AS_ERRORS OFF)
set(ASSIMP_BUILD_ALL_IMPORTERS_BY_DEFAULT OFF CACHE BOOL "")
set(ASSIMP_BUILD_OBJ_IMPORTER ON CACHE BOOL "")
set(ASSIMP_BUILD_GLTF_IMPORTER ON CACHE BOOL "")
add_subdirectory(third_party/assimp)

## GLM
add_subdirectory(third_party/glm)

# subdirectories

add_subdirectory(shared)
add_subdirectory(Examples/OpenGL)

