
add_subdirectory(lib)

set(APP_SRCS
  base64.cc
  )

add_executable(base64 base64.cxx)
target_link_libraries(base64 PUBLIC b64)
