cmake_minimum_required(VERSION 3.15)
project(Project)

# Export compile commands
set(CMAKE_EXPORT_COMPILE_COMMANDS 1)

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

option(NO_BUILD_TESTS "" OFF)

if (NOT ${NO_BUILD_TESTS})
    message(STATUS "Building tests...")
    add_subdirectory(tests)
endif()

add_custom_target(build_finished ALL
    COMMENT "Build almost finished...")

add_custom_command(TARGET build_finished POST_BUILD
    COMMAND cp ${PROJECT_BINARY_DIR}/compile_commands.json ${PROJECT_SOURCE_DIR}/
)
message("Compile commands exported...")
