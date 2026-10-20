cmake_minimum_required(VERSION 4.3)
project(UP_Projects)

set(CMAKE_CXX_STANDARD 20)

# Намира всички .cpp файлове в проекта
file(GLOB_RECURSE CPP_FILES CONFIGURE_DEPENDS
        "${CMAKE_SOURCE_DIR}/*.cpp"
)

foreach(CPP_FILE IN LISTS CPP_FILES)

    # Пропуска файловете в build директориите
    if(CPP_FILE MATCHES "/cmake-build-" OR
            CPP_FILE MATCHES "/build/")
        continue()
    endif()

    # Взима относителния път
    file(RELATIVE_PATH REL_PATH
            "${CMAKE_SOURCE_DIR}"
            "${CPP_FILE}"
    )

    # Създава уникално име според директорията
    string(REPLACE "/" "_" TARGET_NAME "${REL_PATH}")
    string(REPLACE "\\" "_" TARGET_NAME "${TARGET_NAME}")
    string(REGEX REPLACE "\\.cpp$" "" TARGET_NAME "${TARGET_NAME}")

    # Създава отделна програма за всеки файл
    add_executable("${TARGET_NAME}" "${CPP_FILE}"
            Practicum-week1/zad13.cpp)

endforeach()