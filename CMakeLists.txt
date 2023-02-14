cmake_minimum_required(VERSION 3.18)
project(base VERSION 1.0.0 )

if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Release)
endif()

if(APPLE)
  message(STATUS "APPLE")
else()
  message(STATUS "UNIX")
endif()

set(CMAKE_C_FLAGS "-DHAVE_CONFIG_H -Wall -Wextra")
set(CMAKE_CXX_FLAGS "-DHAVE_CONFIG_H -std=c++11 -Wall -Wextra")
set(CMAKE_CXX_FLAGS_DEBUG "-g")
set(CMAKE_CXX_FLAGS_RELEASE "-O3")
set(CMAKE_INSTALL_PREFIX /opt/dialoid)

find_path(BOOST_ROOT NAMES boost/version.hpp HINTS "/opt/dialoid/include")
message(STATUS "Boost_ROOT: ${BOOST_ROOT}")
set(BOOST_LIBRARYDIR "/opt/dialoid/lib")
set(Boost_NO_SYSTEM_PATHS ON)
set(Boost_DEBUG 1)

find_package(Boost 1.75 REQUIRED COMPONENTS system filesystem thread regex locale )

if(NOT Boost_FOUND)
    message(FATAL_ERROR "Could not find boost!")
endif()

if(Boost_FOUND)
    message(STATUS "Boost_INCLUDE_DIRS: ${Boost_INCLUDE_DIRS}")
    message(STATUS "Boost_LIBRARIES: ${Boost_LIBRARIES}")
    message(STATUS "Boost_VERSION: ${Boost_VERSION}")
endif()

include_directories(${Boost_INCLUDE_DIRS})
link_directories(${Boost_LIBRARY_DIRS})

###find package
#find_package(PkgConfig REQUIRED)
#set(ENV{PKG_CONFIG_PATH} "/opt/dialoid/lib/pkgconfig:/opt/dialoid/lib64/pkgconfig:/usr/lib64/pkgconfig:/usr/local/Cellar/openssl@1.1/1.1.1l_1/lib/pkgconfig:")

set(DEBUG 1)

#configure_file (
#  "${PROJECT_SOURCE_DIR}/config.h.in"
#  "${PROJECT_SOURCE_DIR}/config.h"
#  )

include_directories("${PROJECT_SOURCE_DIR}")
include_directories("./src")
include_directories("/opt/dialoid/include")


add_subdirectory(src)

install(TARGETS ${PROJECT_NAME})