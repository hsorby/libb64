
add_executable(example1 c-example1.c)
target_link_libraries(example1 PUBLIC b64)

add_executable(example2 c-example2.c)
target_link_libraries(example2 PUBLIC b64)
