#####################
# Generic cmake related.
#####################

cmake_minimum_required(VERSION 3.2)
project(myoutoftreetool VERSION 0.0.1 LANGUAGES CXX)

####################################
  #LLVM related
####################################
# Set custom cmake modules path
#set (CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/Modules")

# Find and use LLVM
find_package(LLVM REQUIRED CONFIG)
message(STATUS "Found LLVM ${LLVM_PACKAGE_VERSION}")
message(STATUS "Using LLVMConfig.cmake in: ${LLVM_DIR}")

include_directories(${LLVM_INCLUDE_DIRS})
add_definitions(${LLVM_DEFINITIONS})
message(STATUS "LLVM_DEFINITIONS = " ${LLVM_DEFINITIONS})

# Find the libraries that correspond to the LLVM components that we wish to use.
llvm_map_components_to_libnames(LLVM_LIBS core)
message(STATUS "Printing LLVM_LIBS = " ${LLVM_LIBS})
llvm_map_components_to_libnames(LLVM_LIBS support)
message(STATUS "Printing LLVM_LIBS = " ${LLVM_LIBS})

# Needed for compiling for resolving typename related issue.
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fno-rtti")

message(STATUS "Compiler custom flags are: ${CMAKE_CXX_FLAGS}")
message(STATUS "Compiler debug flags are: ${CMAKE_CXX_FLAGS_DEBUG}")
message(STATUS "Compiler release flags are: ${CMAKE_CXX_FLAGS_RELEASE}")

####################################
# Add source files
####################################

file(GLOB SOURCES
${PROJECT_SOURCE_DIR}/helloworld.cpp
)
add_executable(myoutoftreetool ${SOURCES})
# Output to root of build directory
set_target_properties( myoutoftreetool
    PROPERTIES
    ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}"
    LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}"
    RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}"
)
target_link_libraries(myoutoftreetool PRIVATE ${LLVM_LIBS})
# Use C++17 standard
target_compile_features(myoutoftreetool PRIVATE cxx_std_17)
