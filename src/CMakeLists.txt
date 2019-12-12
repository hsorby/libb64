
add_subdirectory(lib)

set(APP_SRCS
  base64.cc
  )

add_executable(base64 base64.cxx)
target_link_libraries(base64 PUBLIC b64)

install(TARGETS base64 EXPORT base64-targets
  COMPONENT runtime
  RUNTIME DESTINATION bin
  )

include(CMakePackageConfigHelpers)

set(BUILD_TREE_CONFIG_DIR ${PROJECT_BINARY_DIR})
set(BASE64_CONFIG_VERSION_FILE "${BUILD_TREE_CONFIG_DIR}/base64-config-version.cmake")
write_basic_package_version_file(
  ${BASE64_CONFIG_VERSION_FILE}
  VERSION ${Base64_VERSION}
  COMPATIBILITY AnyNewerVersion
)

set(BASE64_CONFIG_CMAKE_FILE "${BUILD_TREE_CONFIG_DIR}/base64-config.cmake")
file(WRITE "${BASE64_CONFIG_CMAKE_FILE}" "include(\"\${CMAKE_CURRENT_LIST_DIR}/base64-targets.cmake\")\n")

set(BASE64_TARGETS_FILE "${BUILD_TREE_CONFIG_DIR}/base64-targets.cmake")
export(EXPORT base64-targets FILE ${BASE64_TARGETS_FILE})

if(WIN32)
  set(CONFIG_PACKAGE_LOCATION ${PROJECT_NAME}/CMake)
else()
  set(CONFIG_PACKAGE_LOCATION lib/cmake/${PROJECT_NAME})
endif()
install(EXPORT base64-targets
  FILE base64-targets.cmake
  DESTINATION ${CONFIG_PACKAGE_LOCATION}
  COMPONENT development
  )

install(FILES
    ${BASE64_CONFIG_CMAKE_FILE}
    ${BASE64_CONFIG_VERSION_FILE}
  DESTINATION ${CONFIG_PACKAGE_LOCATION}
  COMPONENT development
  )
