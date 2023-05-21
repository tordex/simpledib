cmake_minimum_required(VERSION 3.11)
project(simpledib LANGUAGES C CXX)

set(SOURCE_SIMPLEDIB
    dib.cpp
)

set(HEADER_SIMPLEDIB
    dib.h
)

add_library(${PROJECT_NAME} ${SOURCE_SIMPLEDIB})

set_target_properties(${PROJECT_NAME} PROPERTIES
    CXX_STANDARD 11
    C_STANDARD 99
    PUBLIC_HEADER "${HEADER_SIMPLEDIB}"
)

# Export litehtml includes.
target_include_directories(${PROJECT_NAME} PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src>
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include/${PROJECT_NAME}>)
target_include_directories(${PROJECT_NAME} PRIVATE include/${PROJECT_NAME})

# install and export
install(TARGETS ${PROJECT_NAME}
    EXPORT simpledibTargets
    RUNTIME DESTINATION bin COMPONENT libraries
    ARCHIVE DESTINATION lib${LIB_SUFFIX} COMPONENT libraries
    LIBRARY DESTINATION lib${LIB_SUFFIX} COMPONENT libraries
    PUBLIC_HEADER DESTINATION include/simpledib
)
install(FILES cmake/simpledibConfig.cmake DESTINATION lib${LIB_SUFFIX}/cmake/simpledib)
install(EXPORT simpledibTargets FILE simpledibTargets.cmake DESTINATION lib${LIB_SUFFIX}/cmake/simpledib)
