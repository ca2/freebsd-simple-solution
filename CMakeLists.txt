cmake_minimum_required(VERSION 3.17)
project(basis)



set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_EXTENSIONS OFF)
message(STATUS "CMAKE_SYSTEM_NAME is ${CMAKE_SYSTEM_NAME}")


if(${CMAKE_SYSTEM_NAME} STREQUAL "FreeBSD")
   set(default_node node_freebsd)
   set(default_draw2d draw2d_cairo)
   set(PLATFORM_NAME freebsd)
endif()

if($ENV{XDG_CURRENT_DESKTOP} STREQUAL "GNOME")
   set(GNOME true)
endif()



if(GNOME)

   list(APPEND app_common_dependencies desktop_environment_gnome)

endif()



add_compile_definitions(UNICODE)
add_compile_definitions(_UNICODE)


set(LIBRARY_OUTPUT_PATH ${CMAKE_CURRENT_SOURCE_DIR}/time-${PLATFORM_NAME}/cmake)
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_CURRENT_SOURCE_DIR}/time-${PLATFORM_NAME}/cmake)


link_directories(${LIBRARY_OUTPUT_PATH})
link_directories(${CMAKE_CURRENT_SOURCE_DIR}/archive/storage-${PLATFORM_NAME}/library/x64/basis)
link_directories(${CMAKE_CURRENT_SOURCE_DIR}/archive/storage-${PLATFORM_NAME}/third/library/x64/basis)


include_directories(.)
include_directories($ENV{HOME}/__config)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/source)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/source/app)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/source/app/_include)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/source/include)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/archive)
if(PLATFORM_POSIX)
   include_directories(${CMAKE_CURRENT_SOURCE_DIR}/archive/platform-posix)
   include_directories(${CMAKE_CURRENT_SOURCE_DIR}/archive/platform-posix/_include)
endif()
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/archive/platform-${PLATFORM_NAME})
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/archive/platform-${PLATFORM_NAME}/_include)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/archive/third-${PLATFORM_NAME}/include)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/archive/third-${PLATFORM_NAME}/third/include)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/archive/third-${PLATFORM_NAME}/third/include/include)




add_subdirectory(source/app/acme)
add_subdirectory(archive/platform-posix/acme_posix)
add_subdirectory(archive/platform-freebsd/acme_freebsd)
add_subdirectory(source/console/helloearth)
add_subdirectory(source/app/apex)
add_subdirectory(archive/platform-posix/apex_posix)
add_subdirectory(archive/platform-freebsd/apex_freebsd)
add_subdirectory(source/app/aqua)
add_subdirectory(source/console/hellosolarsystem)
add_subdirectory(source/console/readlines)
add_subdirectory(source/app/aura)
add_subdirectory(archive/platform-posix/aura_posix)
add_subdirectory(archive/platform-freebsd/aura_freebsd)
add_subdirectory(archive/platform-freebsd/node_freebsd)
add_subdirectory(source/app/draw2d_cairo)
add_subdirectory(archive/platform-freebsd/desktop_environment_gnome)
add_subdirectory(source/app/app)





