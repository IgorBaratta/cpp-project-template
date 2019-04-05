cmake_minimum_required (VERSION 3.8 FATAL_ERROR)
project (ProjectTemplate VERSION 0.1 LANGUAGES CXX)

set (SOURCES

)
set (MAIN_SOURCE
    src/main.cpp
)
set (TEST_SOURCES
    tests/catch.hpp
    tests/tests_main.cpp
    tests/tests.cpp
)

add_executable (project ${MAIN_SOURCE} ${SOURCES})
set_target_properties(project PROPERTIES
    CXX_STANDARD 17
    CXX_STANDARD_REQUIRED YES
    CXX_EXTENSIONS NO
)

add_executable (projectTest ${TEST_SOURCES} ${SOURCES})
set_target_properties(projectTest PROPERTIES
    CXX_STANDARD 17
    CXX_STANDARD_REQUIRED YES
    CXX_EXTENSIONS NO
)

set (GNU_COMPILE_FLAGS
    -ansi
    -pedantic
    -Wall
    -Wextra
    -Wshadow
)
set (CLANG_COMPILE_FLAGS
    -ansi
    -pedantic
    -Wall
    -Wextra
)
set (MSVC_COMPILE_FLAGS
    /W4
)

if (GNU)
    target_compile_options (${project} PRIVATE ${GNU_COMPILE_FLAGS})
    target_compile_options (${projectTest} PRIVATE ${GNU_COMPILE_FLAGS})
elseif (clang)
    target_compile_options (${project} PRIVATE ${CLANG_COMPILE_FLAGS})
    target_compile_options (${projectTest} PRIVATE ${CLANG_COMPILE_FLAGS})
elseif (MSVC)
    target_compile_options (${project} PRIVATE ${MSVC_COMPILE_FLAGS})
    target_compile_options (${projectTest} PRIVATE ${MSVC_COMPILE_FLAGS})
endif ()
