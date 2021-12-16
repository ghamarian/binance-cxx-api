cmake_minimum_required(VERSION 3.13.4 FATAL_ERROR)

project(binance-cxx-api)

set(PROJECT_VERSION_MAJOR 0)
set(PROJECT_VERSION_MINOR 1)
set(PROJECT_VERSION_PATCH 0)

set(CMAKE_CXX_STANDARD 11)

# Search path for CMake include files.
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

find_package(MbedTLS CONFIG REQUIRED PATHS "${CMAKE_SOURCE_DIR}/../mbedtls/build/cmake/" NO_DEFAULT_PATH)
find_package(jsoncpp CONFIG REQUIRED)
find_package(curl CONFIG REQUIRED)
find_package(libwebsockets CONFIG REQUIRED)

set(JSONCPP_LIBRARIES jsoncpp_object jsoncpp_static JsonCpp::JsonCpp) 
set(LIBWEBSOCKETS_LIBRARIES websockets)

file(GLOB_RECURSE LIBRARY_SRC "src/*.cpp" "include/*.h")

add_library(${PROJECT_NAME} SHARED ${LIBRARY_SRC})
target_link_libraries(${PROJECT_NAME} PUBLIC ${LIBWEBSOCKETS_LIBRARIES} ${JSONCPP_LIBRARIES} ${CURL_LIBRARIES})
target_link_libraries(${PROJECT_NAME} PUBLIC MbedTLS::mbedtls MbedTLS::mbedcrypto MbedTLS::mbedx509)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)

add_executable(example example.cpp)
target_include_directories(example PRIVATE "${JSONCPP_INCLUDE_DIRS}")
target_link_libraries(example ${PROJECT_NAME})

