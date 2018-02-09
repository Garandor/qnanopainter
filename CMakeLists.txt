cmake_minimum_required(VERSION 3.1)

#QNanoPainter
# Find includes in corresponding build directories
set(CMAKE_INCLUDE_CURRENT_DIR ON)
# Instruct CMake to run moc automatically when needed.
set(CMAKE_AUTOMOC ON)

find_package(Qt5 REQUIRED Gui Quick)
find_package(OpenGL REQUIRED)

add_subdirectory(libqnanopainter)
