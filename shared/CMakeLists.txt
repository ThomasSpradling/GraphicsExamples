file(GLOB_RECURSE SRC_FILES LIST_DIRECTORIES false RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} *.cpp)
file(GLOB_RECURSE HEADER_FILES LIST_DIRECTORIES false RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} *.h)

add_library(shared ${SRC_FILES} ${HEADER_FILES})
target_include_directories(shared PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

set_target_properties(shared PROPERTIES DEBUG_POSTFIX "")

set_property(TARGET shared PROPERTY CXX_STANDARD 20)
set_property(TARGET shared PROPERTY CXX_STANDARD_REQUIRED ON)
target_link_libraries(shared PUBLIC
    glad
    glm
    glfw
    assimp
    imgui
)
