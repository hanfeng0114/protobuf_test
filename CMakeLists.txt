cmake_minimum_required (VERSION 2.6)
project (test_cp)

# The version number.
set (Tutorial_VERSION_MAJOR 0)
set (Tutorial_VERSION_MINOR 0)

set (CMAKE_CXX_COMPILER_VERSION 11)

find_package(Protobuf REQUIRED)
PROTOBUF_GENERATE_CPP(PROTO_SRCS PROTO_HDRS ${PROJECT_SOURCE_DIR}/config/addressbook.proto)
include_directories("${PROJECT_BINARY_DIR}")

# add the binary tree to the search path for include files
# so that we will find TutorialConfig.h

# add the MathFunctions library?
set (A_FILES
        ${PROJECT_SOURCE_DIR}/src/add_person.cc)

set (L_FILES
        ${PROJECT_SOURCE_DIR}/src/list_people.cc)

# add the executable
add_executable (add_person ${A_FILES} ${PROTO_SRCS} ${PROTO_HDRS})
add_executable (list_person ${A_FILES} ${PROTO_SRCS} ${PROTO_HDRS})
target_link_libraries(add_person ${PROTOBUF_LIBRARIES} protobuf)
target_link_libraries(list_person ${PROTOBUF_LIBRARIES} protobuf)
