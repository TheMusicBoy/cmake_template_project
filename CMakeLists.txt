cmake_minimum_required(VERSION 3.15)
project(TestMicroCtrl)


# Export compile commands
option(COMPILE_COMMANDS "" OFF)

if (${DEBUG})
    message(STATUS "Export compile_commands - ON")
    set(CMAKE_EXPORT_COMPILE_COMMANDS 1)
endif()


# Build settings
set(CMAKE_CXX_STANDARD 20)

option(DEBUG "" OFF)

if (${DEBUG})
    message(STATUS "Building with debug...")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -g")
endif()

# Building ---
add_subdirectory(thirdparty)
add_subdirectory(src)

option(BUILD_TESTS "" OFF)

if (${BUILD_TESTS})
    message(STATUS "Building tests...")
    add_subdirectory(tests)
endif()
