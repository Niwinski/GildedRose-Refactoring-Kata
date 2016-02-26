cmake_minimum_required(VERSION 2.8.4)
project(cpp)

if (MSVC)
	foreach(flag_var
			CMAKE_CXX_FLAGS CMAKE_CXX_FLAGS_DEBUG CMAKE_CXX_FLAGS_RELEASE
			CMAKE_CXX_FLAGS_MINSIZEREL CMAKE_CXX_FLAGS_RELWITHDEBINFO)
		if(${flag_var} MATCHES "/MD")
			string(REGEX REPLACE "/MD" "/MT" ${flag_var} "${${flag_var}}")
		endif(${flag_var} MATCHES "/MD")
	endforeach(flag_var)
endif ()
 
enable_testing()
find_package(GTest REQUIRED)
include_directories(${GTEST_INCLUDE_DIRS})

set(GILDED_ROSE_SOURCE_FILES
    GildedRose.cc
    GildedRose.h
    GildedRoseUnitTests.cc)

set(GILDED_ROSE_TEXT_TESTS_SOURCE_FILES
    GildedRose.cc
    GildedRose.h
    GildedRoseTextTests.cc)

set(SOURCE_FILES
    ${GILDED_ROSE_SOURCE_FILES}
    ${GILDED_ROSE_TEXT_TESTS_SOURCE_FILES})

add_executable(GildedRose ${GILDED_ROSE_SOURCE_FILES})
target_link_libraries(GildedRose ${GTEST_BOTH_LIBRARIES} ${CMAKE_THREAD_LIBS_INIT})

add_executable(GildedRoseTextTests ${GILDED_ROSE_TEXT_TESTS_SOURCE_FILES})
target_link_libraries(GildedRoseTextTests ${GTEST_BOTH_LIBRARIES} ${CMAKE_THREAD_LIBS_INIT})
