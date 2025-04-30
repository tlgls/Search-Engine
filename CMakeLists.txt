cmake_minimum_required(VERSION 3.15)
project(FinalProjExamples)

# Set C++ standard to 17
set(CMAKE_CXX_STANDARD 17)

# Copy sample data if the directory exists
file(COPY sample_data/ DESTINATION sample_data/)

# Show compiler output and enable warnings
set(CMAKE_VERBOSE_MAKEFILE ON)

# Apply compiler options conditionally based on the compiler being used
if(MSVC)
    # MSVC-specific warning level
    add_compile_options(/W4)  # /W4 is equivalent to -Wall for MSVC
else()
    # For other compilers (e.g., GCC, Clang)
    add_compile_options(-Wall -Wextra -pedantic)
endif()

add_executable(rapidJSONExample rapidJSONExample.cpp)
add_executable(supersearch main.cpp DocumentParser.cpp IndexHandler.cpp porter2_stemmer.cpp QueryProcessor.cpp SearchEngine.cpp)
add_executable(testAVLTree testAVLTree.cpp)
add_test(testingAVLTree testAVLTree)

# This ensures we also link rapidjson
target_include_directories(rapidJSONExample PRIVATE rapidjson/)

set(CMAKE_VERBOSE_MAKEFILE OFF)
