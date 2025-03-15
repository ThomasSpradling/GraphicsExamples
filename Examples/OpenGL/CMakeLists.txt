set(EXAMPLE_DIRS
    Hello/Hello
)

foreach(example ${EXAMPLE_DIRS})
    file(GLOB_RECURSE EXAMPLE_SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/${example}/*.cpp")
    file(GLOB_RECURSE EXAMPLE_HEADERS "${CMAKE_CURRENT_SOURCE_DIR}/${example}/*.h")

    string(REPLACE "/" "_" TARGET_NAME_INT ${example})
    string(APPEND TARGET_NAME "gl_" ${TARGET_NAME_INT})

    add_executable(${TARGET_NAME} ${EXAMPLE_SOURCES} ${EXAMPLE_HEADERS})

    set(EXAMPLE_OUTPUT ${CMAKE_BINARY_DIR}/bin/${example})
    set_target_properties(${TARGET_NAME} PROPERTIES
        RUNTIME_OUTPUT_DIRECTORY ${EXAMPLE_OUTPUT}
        CXX_STANDARD 20
        CXX_STANDARD_REQUIRED ON
    )
    
    target_link_libraries(${TARGET_NAME} PUBLIC
        shared
        glad
        glm
        glfw
        assimp
        imgui
    )
endforeach()
