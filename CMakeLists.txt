cmake_minimum_required(VERSION 3.22)
project(another-raylib-cpp-cmake-template CXX) # If it doesn't build, be sure to check the launch.json and tasks.json and make sure all project names match.

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

include(FetchContent)

# Add dependencies with FetchContent
function(add_git_dependency libName gitURL gitTag)
    FetchContent_Declare(${libName}
        GIT_REPOSITORY ${gitURL}
        GIT_TAG ${gitTag}
        GIT_SHALLOW TRUE
        GIT_PROGRESS TRUE
    )
    FetchContent_MakeAvailable(${libName})
    target_compile_options(${libName} PRIVATE "-w")
endfunction()

## ADD ANY ADDITIONAL PROJECT DEPENDENCIES HERE ---------------------------------------------------------------

# Add Raylib
#set() - good for turning off specific things you don't want to buid.
set(BUILD_EXAMPLES OFF CACHE BOOL "" FORCE) # don't build the supplied examples
set(BUILD_GAMES OFF CACHE BOOL "" FORCE) # don't build the supplied example games
add_git_dependency( # add a new git dependency
    raylib # add raylib
    https://github.com/raysan5/raylib.git # link to raylib git repository
    5.5 # add raylib version tag (Note: Fetched dependency versions will always stay at the same tagged version)
)

# [Add more dependencies here]


# end of dependencies -------------------------------------------------------------------------------------------


## Project executable setup

# Adding our src files
# Define PROJECT_SOURCES as a list of all src files
file(GLOB_RECURSE PROJECT_SOURCES CONFIGURE_DEPENDS "${CMAKE_CURRENT_LIST_DIR}/src/*.cpp")

# Define PROJECT_INCLUDE to be the path to the include directory of the project
set(PROJECT_INCLUDE "${CMAKE_CURRENT_LIST_DIR}/src/")

# Declaring our executable
add_executable(${PROJECT_NAME})
target_sources(${PROJECT_NAME} PRIVATE ${PROJECT_SOURCES})
target_include_directories(${PROJECT_NAME} PRIVATE ${PROJECT_INCLUDE})


## TARGET LINK LIBRARIES HERE ------------------------------------------------------------------------------------

# IMPORTANT - BE SURE TO ADD ANY ADDED LIBRARIES HERE FOR LINKING


target_link_libraries(${PROJECT_NAME} PRIVATE raylib) # Here raylib is being privately linked.


# [add more target link libraries here]

# end of target link libraries ------------------------------------------------------------------------------------


# Project build settings
add_definitions(-DCMAKE_BUILD_TYPE=${CMAKE_BUILD_TYPE})

# Setting ASSETS_PATH to resources
if(CMAKE_BUILD_TYPE MATCHES "Debug")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O0 -DDEBUG")

    # Set the resources path macro to the absolute path on the dev machine
    target_compile_definitions(${PROJECT_NAME} PUBLIC ASSETS_PATH="${CMAKE_CURRENT_SOURCE_DIR}/resources/")
else()
    # Set the resources path macro in release mode to a relative path that assumes the resources folder is in the same directory as the game executable
    target_compile_definitions(${PROJECT_NAME} PUBLIC ASSETS_PATH="./resources/")
endif()

# Set common compiler flags
# SET(CMAKE_CXX_FLAGS  "${CMAKE_CXX_FLAGS} -Wall -Wswitch")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall")

#end of CMakeLists.txt