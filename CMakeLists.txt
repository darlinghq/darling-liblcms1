project(darling-liblcms1)

cmake_minimum_required(VERSION 2.4.0)
enable_language(C ASM)

if(COMMAND cmake_policy)
	cmake_policy(SET CMP0003 NEW)
endif(COMMAND cmake_policy)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -msse -msse2 -msse3 -w -nostdinc")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -D__DARWIN_UNIX03 -fPIC -w -ggdb -O0")
set(CMAKE_SHARED_LINKER_FLAGS "${CMAKE_SHARED_LINKER_FLAGS} -nostdlib -Wl,--version-script=${DARLING_TOP_DIRECTORY}/darwin.map")

include_directories(${CMAKE_CURRENT_SOURCE_DIR})
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/src)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)
include_directories(${DARLING_TOP_DIRECTORY}/platform-include)
include_directories(${DARLING_TOP_DIRECTORY}/src/libc/fbsdcompat)

add_definitions(-DSTDC_HEADERS=1)
add_definitions(-DHAVE_SYS_TYPES_H=1)
add_definitions(-DHAVE_SYS_STAT_H=1)
add_definitions(-DHAVE_STDLIB_H=1)
add_definitions(-DHAVE_STRING_H=1)
add_definitions(-DHAVE_MEMORY_H=1)
add_definitions(-DHAVE_STRINGS_H=1)
add_definitions(-DHAVE_INTTYPES_H=1)
add_definitions(-DHAVE_STDINT_H=1)
add_definitions(-DHAVE_UNISTD_H=1)
add_definitions(-DHAVE_DLFCN_H=1)

set(lcms_sources
    src/cmscnvrt.c
    src/cmserr.c
    src/cmsgamma.c
    src/cmsgmt.c
    src/cmsintrp.c
    src/cmsio1.c
    src/cmslut.c
    src/cmsmatsh.c
    src/cmsmtrx.c
    src/cmspack.c
    src/cmspcs.c
    src/cmswtpnt.c
    src/cmsxform.c
    src/cmssamp.c
    src/cmscam97.c
    src/cmsnamed.c
    src/cmsps2.c
    src/cmscam02.c
    src/cmsvirt.c
    src/cmscgats.c
    src/cmsio0.c
)

SET(CMAKE_INSTALL_RPATH "${CMAKE_INSTALL_PREFIX}/${CMAKE_INSTALL_LIBDIR}/darling")
SET(CMAKE_BUILD_WITH_INSTALL_RPATH TRUE) 
SET(CMAKE_INSTALL_RPATH_USE_LINK_PATH TRUE)

add_library(lcms SHARED ${lcms_sources})
target_link_libraries(lcms system)

install(TARGETS lcms DESTINATION ${CMAKE_INSTALL_LIBDIR}/darling)
