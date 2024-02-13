cmake_minimum_required(VERSION 3.22)
project(rabbit VERSION 1.0)

option(ENABLE_TESTING "Enables Unit Tests for Rabbit" OFF)

# Set header files
set(HEADER_FILES
    include/rabbit.hpp
)

# Fetch External Rapidjson
include(FetchContent)
FetchContent_Declare(
    rapidjson
    GIT_REPOSITORY http://dehallxdo01/bac/m1-libraries/m1_rapidjson.git
    GIT_TAG 85663b8a5ed7dd6f828446afdc8433094f5ac98f
)
FetchContent_MakeAvailable(rapidjson)

include_directories(
    include
    $<BUILD_INTERFACE:${CMAKE_BINARY_DIR}/_deps/rapidjson-src>
)

# Optionally, you can set up installation rules
install(FILES ${HEADER_FILES} DESTINATION include/rabbit)
install(DIRECTORY $<BUILD_INTERFACE:${CMAKE_BINARY_DIR}/_deps/rapidjson-src/include/rapidjson> 
DESTINATION include/rapidjson)

# Optionally, you can add tests
if(${ENABLE_TESTING})
    message(STATUS "Testing Enabled")
    enable_testing()
    add_subdirectory(test)
endif()