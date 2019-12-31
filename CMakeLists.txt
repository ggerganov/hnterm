cmake_minimum_required (VERSION 3.10)
project(hnterm)

set(CMAKE_EXPORT_COMPILE_COMMANDS "on")
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

if (EMSCRIPTEN)
    #set (CMAKE_CXX_FLAGS "-s ALLOW_MEMORY_GROWTH=1 -s FETCH=1 -s ASSERTIONS=1 -s DISABLE_EXCEPTION_CATCHING=0")
else()
endif()

# options

option(HNTERM_ALL_WARNINGS            "hnterm: enable all compiler warnings" ON)
option(HNTERM_ALL_WARNINGS_3RD_PARTY  "hnterm: enable all compiler warnings in 3rd party libs" ON)

option(HNTERM_SANITIZE_THREAD         "hnterm: enable thread sanitizer" OFF)
option(HNTERM_SANITIZE_ADDRESS        "hnterm: enable address sanitizer" OFF)
option(HNTERM_SANITIZE_UNDEFINED      "hnterm: enable undefined sanitizer" OFF)

# sanitizers

if (HNTERM_SANITIZE_THREAD)
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -fsanitize=thread")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fsanitize=thread")
endif()

if (HNTERM_SANITIZE_ADDRESS)
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -fsanitize=address -fno-omit-frame-pointer")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fsanitize=address -fno-omit-frame-pointer")
endif()

if (HNTERM_SANITIZE_UNDEFINED)
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -fsanitize=undefined")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fsanitize=undefined")
endif()

# dependencies

add_subdirectory(third-party)

find_package(CURL REQUIRED)

# main

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

if (NOT CMAKE_BUILD_TYPE AND NOT CMAKE_CONFIGURATION_TYPES)
    set(CMAKE_BUILD_TYPE Release CACHE STRING "Build type" FORCE)
    set_property(CACHE CMAKE_BUILD_TYPE PROPERTY STRINGS "Debug" "Release" "RelWithDebInfo")
endif ()

if (HNTERM_ALL_WARNINGS)
    if (CMAKE_COMPILER_IS_GNUCC OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
        set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra -pedantic")
    else()
        # todo : windows
    endif()
endif()

add_subdirectory(src)
