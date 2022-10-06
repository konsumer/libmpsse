cmake_minimum_required(VERSION 3.11)
set(CMAKE_C_STANDARD 99)

find_package(PkgConfig)
include(GNUInstallDirs)

project (mpsse
  VERSION 1.3.2
  DESCRIPTION "Library for interfacing with SPI/I2C devices via FTDI's FT-2232 family of USB to serial chips"
  HOMEPAGE_URL "https://github.com/l29ah/libmpsse"
  LANGUAGES C)

add_compile_definitions(PACKAGE_VERSION="${CMAKE_PROJECT_VERSION}")

if ( CMAKE_COMPILER_IS_GNUCC )
    set(CMAKE_C_FLAGS "-fPIC ${CMAKE_C_FLAGS} -Wno-unused-result -Wall -Wextra")
endif()

if ( MSVC )
    set(CMAKE_CXX_FLAGS  "${CMAKE_CXX_FLAGS} /w")
endif()

if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Release)
endif()

set(CMAKE_C_FLAGS_DEBUG "-g")
set(CMAKE_C_FLAGS_RELEASE "-O3")

file(GLOB PROJECT_SOURCES CONFIGURE_DEPENDS "${CMAKE_CURRENT_LIST_DIR}/src/*.c")
set(PROJECT_INCLUDE "${CMAKE_CURRENT_LIST_DIR}/src/")

# TODO: I think ftdi has cmake-finder built-in, but I am just using pkg-config
pkg_check_modules(FTDI REQUIRED ftdi)

# TODO: add targets for examples (with define-options to disable)
# TODO: add target for python (disabled by default, with option to enable)

add_library(${PROJECT_NAME} SHARED)
target_link_libraries(${PROJECT_NAME} ${FTDI_LINK_LIBRARIES})
target_include_directories(${PROJECT_NAME} PUBLIC ${FTDI_INCLUDE_DIRS})
target_compile_options(${PROJECT_NAME} PUBLIC ${FTDI_CFLAGS_OTHER})
target_sources(${PROJECT_NAME} PRIVATE ${PROJECT_SOURCES})

set_target_properties(${PROJECT_NAME} PROPERTIES PUBLIC_HEADER src/mpsse.h)
install(TARGETS ${PROJECT_NAME} PUBLIC_HEADER)