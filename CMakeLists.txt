cmake_minimum_required(VERSION 3.18)

set(CMAKE_FIND_DEBUG_MODE TRUE)

project("tree-sitter-c-playground")

add_library(tree_sitter STATIC IMPORTED)

set_property(
  TARGET tree_sitter APPEND PROPERTY IMPORTED_CONFIGURATIONS DEBUG
)

set_target_properties(tree_sitter PROPERTIES
  IMPORTED_LINK_INTERFACE_LANGUAGES_DEBUG "CXX"
  IMPORTED_LOCATION_DEBUG "${tree_sitter_ROOT}/lib/libtree-sitter.a"
)

set_property(
  TARGET tree_sitter APPEND PROPERTY IMPORTED_CONFIGURATIONS RELEASE
)

set_target_properties(tree_sitter PROPERTIES
  IMPORTED_LINK_INTERFACE_LANGUAGES_RELEASE "CXX"
  IMPORTED_LOCATION_RELEASE "${tree_sitter_ROOT}/lib/libtree-sitter.a"
)
  
set_target_properties(tree_sitter PROPERTIES
  MAP_IMPORTED_CONFIG_MINSIZEREL Release
  MAP_IMPORTED_CONFIG_RELWITHDEBINFO Release
)

target_include_directories(tree_sitter INTERFACE "${tree_sitter_ROOT}/include")

add_executable(${PROJECT_NAME}
    "src/main.c"
)

target_link_libraries(${PROJECT_NAME} tree_sitter)
target_link_options(${PROJECT_NAME} PRIVATE "-static")

