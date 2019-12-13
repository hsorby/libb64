
cmake_minimum_required(VERSION 3.10)

set(PROJECT_NAME Base64)
project(${PROJECT_NAME} VERSION 1.2.2 LANGUAGES C CXX)

get_property(IS_MULTI_CONFIG GLOBAL PROPERTY GENERATOR_IS_MULTI_CONFIG)

set(BASE64_BUFFERSIZE "16777216" CACHE STRING "Select a buffersize a larger size should be faster, but takes more runtime memory. e.g. 4096, 65536, 16777216")
set(BASE64_CHARSPERLINE "72" CACHE STRING "Select a chars per line value. e.g. 72, 80, -1 for no new lines.")

set(_PARAM_ANNOTATION "Install path prefix, prepended onto install directories.")
set(BASE64_INSTALL_PREFIX ${CMAKE_INSTALL_PREFIX} CACHE PATH ${_PARAM_ANNOTATION})
if(DEFINED INSTALL_PREFIX)
  set(BASE64_INSTALL_PREFIX ${INSTALL_PREFIX} CACHE PATH ${_PARAM_ANNOTATION} FORCE)
endif()
unset(INSTALL_PREFIX CACHE)

if(NOT IS_MULTI_CONFIG)
  set(_PARAM_ANNOTATION "Choose the type of build, options are: None(CMAKE_CXX_FLAGS or CMAKE_C_FLAGS used) Debug Release RelWithDebInfo MinSizeRel.")
  set(BASE64_BUILD_TYPE "Debug" CACHE STRING ${_PARAM_ANNOTATION})
  if(DEFINED BUILD_TYPE)
    set(BASE64_BUILD_TYPE ${BUILD_TYPE} CACHE STRING ${_PARAM_ANNOTATION} FORCE)
  endif()
  unset(BUILD_TYPE CACHE)
endif()

file(TO_CMAKE_PATH ${BASE64_INSTALL_PREFIX} _CMAKE_INSTALL_PREFIX)
set(CMAKE_INSTALL_PREFIX ${_CMAKE_INSTALL_PREFIX} CACHE INTERNAL "Internalise CMAKE_INSTALL_PREFIX, manipulate via BASE64_INSTALL_PREFIX" FORCE)
set(CMAKE_BUILD_TYPE ${BASE64_BUILD_TYPE} CACHE INTERNAL "Internalise CMAKE_BUILD_TYPE, manipulate via BASE64_BUILD_TYPE" FORCE)

mark_as_advanced(CMAKE_CONFIGURATION_TYPES)
mark_as_advanced(CMAKE_CODEBLOCKS_EXECUTABLE)
mark_as_advanced(QT_QMAKE_EXECUTABLE)
mark_as_advanced(CMAKE_EXECUTABLE_FORMAT)
mark_as_advanced(CMAKE_PREFIX_PATH)
if(APPLE)
  mark_as_advanced(CMAKE_OSX_ARCHITECTURES)
  mark_as_advanced(CMAKE_OSX_DEPLOYMENT_TARGET)
  mark_as_advanced(CMAKE_OSX_SYSROOT)
endif()

add_subdirectory(src)
add_subdirectory(examples)
