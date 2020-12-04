PROJECT(peripheral-libs)
CMAKE_MINIMUM_REQUIRED(VERSION 3.5)
SET(CMAKE_CXX_STANDARD 17)
add_definitions(-DARM_MATH_CM4)
add_definitions(-D__FPU_USED)
add_definitions(-D__FPU_PRESENT)
add_definitions(-DHSE_VALUE=8000000UL)

SET(LIBRARY_NAME "peripheral")

MACRO(HEADER_DIRECTORIES return_list)
    FILE(GLOB_RECURSE new_list ${CMAKE_SOURCE_DIR} *.h)
    SET(dir_list "")
    FOREACH(file_path ${new_list})
        GET_FILENAME_COMPONENT(dir_path ${file_path} PATH)
        SET(dir_list ${dir_list} ${dir_path})
    ENDFOREACH()
    LIST(REMOVE_DUPLICATES dir_list)
    SET(${return_list} ${dir_list})
ENDMACRO()

HEADER_DIRECTORIES(header_dir_list)
include_directories(${header_dir_list})

file(GLOB_RECURSE SOURCES_CPP_LIBRARY ${CMAKE_SOURCE_DIR}/*.cpp)
file(GLOB_RECURSE SOURCES_C_LIBRARY ${CMAKE_SOURCE_DIR}/*.c)
file(GLOB_RECURSE HEADERS_LIBRARY ${CMAKE_SOURCE_DIR} *.h)

list(APPEND SOURCES_LIBRARY ${SOURCES_C_LIBRARY})
list(APPEND SOURCES_LIBRARY ${SOURCES_CPP_LIBRARY})

add_library(${LIBRARY_NAME} STATIC ${SOURCES_LIBRARY})
set_target_properties(${LIBRARY_NAME} PROPERTIES
    CXX_STANDARD 17
    CXX_STANDARD_REQUIRED YES
    CXX_EXTENSIONS NO
    PUBLIC_HEADER "${HEADERS_LIBRARY}"
)

####################################################################
##                        INSTALL LIBRARY                         ##
####################################################################

install(TARGETS ${LIBRARY_NAME}
    ARCHIVE DESTINATION ${CMAKE_INSTALL_PREFIX}/lib
    LIBRARY DESTINATION ${CMAKE_INSTALL_PREFIX}/lib
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_PREFIX}/include/peripheral)
