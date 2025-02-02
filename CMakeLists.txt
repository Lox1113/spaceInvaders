cmake_minimum_required(VERSION 3.19)
set(PROJECT_NAME "spaceInvaders")
project(${PROJECT_NAME})
set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -static")
set(SFML_STATIC_LIBRARIES TRUE)
set(SFML_DIR "${CMAKE_CURRENT_LIST_DIR}/libs/SFML-2.5.1/lib/cmake/SFML")
file(GLOB_RECURSE SOURCES "src/*.cpp" "src/*.hpp") #glob all the source files intp one place
file(COPY libs/SFML-2.5.1/bin/openal32.dll DESTINATION ${CMAKE_CURRENT_BINARY_DIR})
set(CMAKE_CXX_STANDARD 20)
link_libraries(stdc++fs) #link the filesystem
file(GLOB_RECURSE SCRF "src/*.cpp" "src/*.hpp")
include_directories("libs/")
include_directories("libs/FastNoise")
include_directories("src/Statemachine")
include_directories("src/GUI")
include_directories("src/Util")
add_executable(${PROJECT_NAME} ${SCRF} main.cpp laser.cpp laser.h bonhomme.cpp bonhomme.h vaisseau.cpp vaisseau.h mur.cpp mur.h alien.cpp alien.h alienManager.cpp alienManager.h)
find_package(SFML 2.5.1 COMPONENTS system window graphics network audio REQUIRED)
target_link_libraries(${PROJECT_NAME} sfml-audio sfml-graphics sfml-window sfml-system)