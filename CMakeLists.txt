cmake_minimum_required (VERSION 3.8 FATAL_ERROR)
project (ProjectName VERSION 0.1 LANGUAGES CXX)

set(BINARY_FOLDER "${CMAKE_SOURCE_DIR}/bin")

set (SOURCES

)
set (MAIN_SOURCE
    src/main.cpp
    ${SOURCES}
)
set (TEST_SOURCES
    tests/catch.hpp
    tests/tests_main.cpp
    tests/tests.cpp
    ${SOURCES}
)

add_executable (project ${MAIN_SOURCE})
set_target_properties(project PROPERTIES
    CXX_STANDARD 17
    CXX_STANDARD_REQUIRED YES
    CXX_EXTENSIONS NO
    RUNTIME_OUTPUT_DIRECTORY "${BINARY_FOLDER}"
)

add_executable (project_tests ${TEST_SOURCES})
set_target_properties(project_tests PROPERTIES
    CXX_STANDARD 17
    CXX_STANDARD_REQUIRED YES
    CXX_EXTENSIONS NO
    RUNTIME_OUTPUT_DIRECTORY "${BINARY_FOLDER}"
)

set (GNU_COMPILE_OPTIONS
    -ansi
    -pedantic
    -Wall
    -Wextra
    -Wshadow
)
set (CLANG_COMPILE_OPTIONS
    -ansi
    -pedantic
    -Wall
    -Wextra
)
set (MSVC_COMPILE_OPTIONS
    /W4
)

if (GNU)
    target_compile_options (${project} PRIVATE ${GNU_COMPILE_OPTIONS})
    target_compile_options (${project_tests} PRIVATE ${GNU_COMPILE_OPTIONS})
elseif (clang)
    target_compile_options (${project} PRIVATE ${CLANG_COMPILE_OPTIONS})
    target_compile_options (${project_tests} PRIVATE ${CLANG_COMPILE_OPTIONS})
elseif (MSVC)
    target_compile_options (${project} PRIVATE ${MSVC_COMPILE_OPTIONS})
    target_compile_options (${project_tests} PRIVATE ${MSVC_COMPILE_OPTIONS})
endif ()
