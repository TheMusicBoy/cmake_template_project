set(SRCROOT "${PROJECT_SOURCE_DIR}/tests")

function(test_case NAME)
    set(TESTS_PATH "${SRCROOT}/${NAME}" CACHE INTERNAL "TESTS_PATH")
endfunction()

function(test_libs)
    set(TEST_LIBS ${ARGN} CACHE INTERNAL "TEST_LIBS")
endfunction()

function(build_test FILE_NAME)
    set(SRC "${TESTS_PATH}/${FILE_NAME}")
    STRING(REGEX REPLACE "${SRCROOT}/" "" PRINT_TESTS_CASE ${TESTS_PATH})
    STRING(REGEX REPLACE "_" " " PRINT_TESTS_CASE ${PRINT_TESTS_CASE})

    STRING(REGEX REPLACE "\\..*" "" PRINT_TEST_NAME ${FILE_NAME})
    STRING(REGEX REPLACE "_" " " PRINT_TEST_NAME ${PRINT_TEST_NAME})

    STRING(REGEX REPLACE " " "" TARGET_NAME "${PRINT_TESTS_CASE}_${PRINT_TEST_NAME}")

    message(STATUS "Building test ${PRINT_TESTS_CASE} : ${PRINT_TEST_NAME} ---")
    message(STATUS "path: ${SRC}")
    add_executable(${TARGET_NAME} ${SRC})
    target_link_libraries(${TARGET_NAME} PUBLIC ${TEST_LIBS})
    set_target_properties(${TARGET_NAME} PROPERTIES LINKER_LANGUAGE CXX)
    message(STATUS "Built successfuly ---")
endfunction()

# Tests

