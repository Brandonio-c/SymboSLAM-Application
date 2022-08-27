# For more information about using CMake with Android Studio, read the
# documentation: https://d.android.com/studio/projects/add-native-code.html

# Sets the minimum version of CMake required to build the native library.

cmake_minimum_required(VERSION 3.10.2)

#compiler stuff! ---------------------------------------

set(DCMAKE_CXX_FLAGS=-stdlib=libc++)
set(DCMAKE_CXX_STANDARD 17)
set(CMAKE_C_COMPILER /cygwin64/bin/gcc.exe)
set(CMAKE_CXX_COMPILER /cygwin64/bin/g++.exe)
set(CMAKE_CXX_STANDARD 17)
INCLUDE_DIRECTORIES (/cygwin64/usr/include -I /cygwin64/usr/include/X11)
LINK_DIRECTORIES    (/cygwin64/usr/include /cygwin64/usr/include/X11)
set (CMAKE_CXX_FLAGS "-lX11 -std=c++17")
find_package(X11 REQUIRED)
link_libraries(${X11_LIBRARIES})
include_directories(${X11_INCLUDE_DIR})

#compiler stuff! ---------------------------------------

# Declares and names the project.

project("SymboSLAM")

# Creates and names a library, sets it as either STATIC
# or SHARED, and provides the relative paths to its source code.
# You can define multiple libraries, and CMake builds them for you.
# Gradle automatically packages shared libraries with your APK.



set(HEADER_FILES include/Random_Drive.h include/Wall_follow.h include/comms.h include/Local_Map.h src/read_file.cpp )
set(SOURCE_FILES src/main.cpp src/Random_Drive.cpp src/Wall_follow.cpp src/comms.cpp src/save_maps.cpp include/save_maps.h  include/read_file.h )

include_directories(
         #random search project
        ${PROJECT_SOURCE_DIR}/src
        ${PROJECT_SOURCE_DIR}/include
)

add_library(SymboSLAM_CPP_Main SHARED src/main.cpp)


# Searches for a specified prebuilt library and stores the path as a
# variable. Because CMake includes system libraries in the search path by
# default, you only need to specify the name of the public NDK library
# you want to add. CMake verifies that the library exists before
# completing its build.

find_library( # Sets the name of the path variable.
              log-lib

              # Specifies the name of the NDK library that
              # you want CMake to locate.
              log )

# Specifies libraries CMake should link to your target library. You
# can link multiple libraries, such as libraries you define in this
# build script, prebuilt third-party libraries, or system libraries.

target_link_libraries( # Specifies the target library.
                       SymboSLAM_CPP_Main

                       # Links the target library to the log library
                       # included in the NDK.
                       ${log-lib} )

target_compile_features(SymboSLAM_CPP_Main PRIVATE cxx_std_17)
set_property(TARGET SymboSLAM_CPP_Main PROPERTY CXX_STANDARD 17)