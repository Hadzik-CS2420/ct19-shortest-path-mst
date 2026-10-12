cmake_minimum_required(VERSION 3.24)
project(ct18-shortest-path-mst LANGUAGES CXX)
set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)


# Write build/compile_commands.json so C++ IntelliSense knows the real
# include paths and flags instead of guessing at them. The devcontainer
# points C_Cpp.default.compileCommands straight at this file.
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

add_executable(${PROJECT_NAME}
    src/main.cpp
    src/WeightedGraph.cpp
)
target_include_directories(${PROJECT_NAME} PRIVATE include)

# --- Google Test ---
include(FetchContent)
FetchContent_Declare(googletest
    URL https://github.com/google/googletest/archive/refs/tags/v1.14.0.zip)
# Windows: keep googletest from overriding the parent project's CRT setting.
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)

add_executable(run_tests
    tests/ct18_test.cpp
    src/WeightedGraph.cpp
)
target_include_directories(run_tests PRIVATE include)
target_link_libraries(run_tests GTest::gtest_main)
