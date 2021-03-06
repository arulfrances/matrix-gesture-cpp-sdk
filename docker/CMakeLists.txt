project(gesture_build C CXX)
cmake_minimum_required(VERSION 2.8)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

find_package(OpenCV 3 REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})

find_package(CURL REQUIRED)
#set(CURL_LIBS ${CURL_LIBRARIES})

find_package(Threads REQUIRED)

find_package(OpenMP)
if (OPENMP_FOUND)
    set (CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
    set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
endif()

cmake_policy(SET CMP0015 NEW)
link_directories(.)
set(GESTURE_LIB
	libgesture.so
)

set(TEST_SRC
	example.cpp
)

add_executable(gesture_test ${TEST_SRC})
set_property(TARGET gesture_test PROPERTY CXX_STANDARD 11)

target_link_libraries(gesture_test ${GESTURE_LIB} ${OpenCV_LIBRARIES} ${CURL_LIBRARIES} ${CMAKE_THREAD_LIBS_INIT})
