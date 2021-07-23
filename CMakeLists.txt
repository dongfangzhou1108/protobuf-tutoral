cmake_minimum_required(VERSION 2.8.3)
project(ros_protocol_buffer_tutorial)

set(CMAKE_CXX_FLAGS "-std=c++11 -Wall")
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)

find_package(Protobuf REQUIRED)
include_directories(${Protobuf_INCLUDE_DIRS})
include_directories(${CMAKE_CURRENT_BINARY_DIR})
include_directories(proto)

add_library(addressbook_protobuf SHARED proto/addressbook.pb.cc)
target_link_libraries(addressbook_protobuf ${Protobuf_LIBRARIES})

add_executable(write_file src/write_file.cpp)
target_link_libraries(write_file addressbook_protobuf ${Protobuf_LIBRARIES})
add_executable(read_file src/read_file.cpp)
target_link_libraries(read_file addressbook_protobuf ${Protobuf_LIBRARIES})