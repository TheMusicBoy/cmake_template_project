include(FetchContent)

function (add_from_fetch TARGET_NAME REPO_TYPE TAG_TYPE REPO TAG)
    if (NOT "${TAG}" STREQUAL "")
        FetchContent_Declare(
            ${TARGET_NAME}
            ${REPO_TYPE} ${REPO}
            ${TAG_TYPE} ${TAG}
        )
    else()
        FetchContent_Declare(
            ${TARGET_NAME}
            ${REPO_TYPE} ${REPO}
        )
    endif()

    FetchContent_MakeAvailable(${TARGET_NAME})
    FetchContent_GetProperties(${TARGET_NAME})

    if (NOT ${TARGET_NAME}_POPULATED)
        FetchContent_Populate(${TARGET_NAME})
        add_subdirectory(${${TARGET_NAME}_SOURCE_DIR} ${${TARGET_NAME}_BINARY_DIR})
    endif()
endfunction()

function (add_from_git TARGET_NAME REPO TAG)
    add_from_fetch(${TARGET_NAME} GIT_REPOSITORY GIT_TAG ${REPO} ${TAG})
endfunction()

# Fetched content


