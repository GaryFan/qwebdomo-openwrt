cmake_minimum_required(VERSION 2.8.9)
project(qtserialport)

# Tell CMake to run moc when necessary:
set(CMAKE_AUTOMOC ON)
# As moc files are generated in the binary dir, tell CMake
# to always look for includes there:
set(CMAKE_INCLUDE_CURRENT_DIR ON)

find_package ( Qt5Core REQUIRED)

include_directories( "./src/serialport"
                     ${CMAKE_CURRENT_BINARY_DIR} )

include_directories( ${CMAKE_FIND_ROOT_PATH}/usr/include/QtCore ${Qt5Core_INCLUDE_DIRS} )
add_definitions( ${Qt5Core_DEFINITIONS} )
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${Qt5Core_EXECUTABLE_COMPILE_FLAGS}" )

set( src ./src/serialport/qserialport.cpp
         ./src/serialport/qserialport_unix.cpp
         ./src/serialport/qserialportinfo.cpp
         ./src/serialport/qserialportinfo_unix.cpp
         ./src/serialport/qttylocker_unix.cpp )
         
add_library( qtserialport SHARED ${src} )
set_target_properties( qtserialport PROPERTIES VERSION "5.1" )

target_link_libraries( qxmpp ${CMAKE_FIND_ROOT_PATH}/usr/lib/libQt5Core.so.5.0.2)