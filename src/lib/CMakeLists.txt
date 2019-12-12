
set(LIB_SRCS
  cencode.c
  cdecode.c
  )

set(LIB_HDRS
  ../include/b64/cdecode.h
  ../include/b64/cencode.h
  ../include/b64/decode.h
  ../include/b64/encode.h
  )

add_library(b64 ${LIB_SRCS} ${LIB_HDRS})
target_include_directories(b64 PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/../include>
  $<INSTALL_INTERFACE:include>
  )
target_compile_definitions(b64 PUBLIC BUFFERSIZE=${BASE64_BUFFERSIZE})

install(TARGETS b64 EXPORT base64-targets
  COMPONENT runtime
  RUNTIME DESTINATION bin
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib
  )

install(FILES
  ${LIB_HDRS}
  DESTINATION include/b64
  COMPONENT development
)
