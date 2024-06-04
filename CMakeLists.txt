cmake_minimum_required(VERSION 3.14)

project(guitest)

include(FetchContent)

FetchContent_Declare(
  bigg
  GIT_REPOSITORY https://github.com/JoshuaBrookover/bigg.git
  GIT_TAG master
)
set( BIGG_EXAMPLES OFF )
FetchContent_MakeAvailable(bigg)

#add_executable( rungui main.cpp )

#target_link_libraries( rungui PUBLIC bigg )
set( SRC_FOLDER ${CMAKE_SOURCE_DIR}/src )
add_executable( cubes ${SRC_FOLDER}/main.cpp ${SRC_FOLDER}/fs_cubes.sc ${SRC_FOLDER}/vs_cubes.sc )
target_link_libraries( cubes bigg )
#set_target_properties( cubes PROPERTIES FOLDER "examples" )

add_shader( ${SRC_FOLDER}/vs_cubes.sc VERTEX   OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/shaders DX11_MODEL 5_0 GLSL 130 )
add_shader( ${SRC_FOLDER}/fs_cubes.sc FRAGMENT OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/shaders DX11_MODEL 5_0 GLSL 130 )

configure_debugging( cubes WORKING_DIR ${CMAKE_CURRENT_BINARY_DIR} )
