cmake_minimum_required(VERSION 4.2)

project(i8080 C)


set(target i8080)
add_library(${target} STATIC
    i8080.c
    i8080.h
)
target_include_directories(${target} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

if(PROJECT_IS_TOP_LEVEL)
set(target i8080_tests)
add_executable(${target}
    i8080_tests.c
)
target_link_libraries(${target} PRIVATE i8080)

# copy cpu_tests

add_custom_command(TARGET ${target} POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory 
        ${CMAKE_CURRENT_SOURCE_DIR}/cpu_tests
        $<TARGET_FILE_DIR:${target}>/cpu_tests)
endif(PROJECT_IS_TOP_LEVEL)
