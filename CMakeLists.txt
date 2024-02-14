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
    GIT_REPOSITORY https://dehallxdo01.bachmann.at/bac/m1-libraries/m1_rapidjson.git
    GIT_TAG 2ea8e9b818ce1f870fd07c2b8a962d9a450f0464
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