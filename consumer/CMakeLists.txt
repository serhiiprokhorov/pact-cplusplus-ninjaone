cmake_minimum_required(VERSION 3.16)
 
#added by Serhii Prokhorov
cmake_policy(SET CMP0091 NEW)

# set the project name
project(pact-cpp-consumer VERSION 0.1.1)

# specify the C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Initialize Conan
INCLUDE(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
CONAN_BASIC_SETUP()

if(MSVC)
    add_compile_options(
        $<$<CONFIG:>:/MT> #---------|
        $<$<CONFIG:Debug>:/MTd> #---|-- Statically link the runtime libraries
        $<$<CONFIG:Release>:/MT> #--|
    )
endif()

add_subdirectory(src)

# Install library
install(TARGETS pact-cpp-consumer DESTINATION lib)
install(FILES include/consumer.h include/matchers.h DESTINATION include)

## Add test
enable_testing()
add_subdirectory(test)
