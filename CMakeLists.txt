
cmake_minimum_required(VERSION 3.10)

set(PROJECT_NAME Base64)
project(${PROJECT_NAME} VERSION 1.2.2 LANGUAGES C CXX)

set(BASE64_BUFFERSIZE "16777216" CACHE STRING "Select a buffersize a larger size should be faster, but takes more runtime memory. e.g. 4096, 65536, 16777216")

add_subdirectory(src)
add_subdirectory(examples)
