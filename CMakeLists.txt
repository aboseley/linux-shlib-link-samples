cmake_minimum_required(VERSION 3.8)

project(test)


SET(CMAKE_SKIP_INSTALL_RPATH FALSE)
#SET(CMAKE_BUILD_WITH_INSTALL_RPATH TRUE)
#SET(CMAKE_INSTALL_RPATH "${CMAKE_INSTALL_PREFIX}/lib")
SET(CMAKE_INSTALL_RPATH_USE_LINK_PATH TRUE)
SET(CMAKE_INSTALL_RPATH "${CMAKE_INSTALL_PREFIX}/lib")


add_library(foo SHARED foo.c)

add_library(bar SHARED bar.c)
target_link_libraries(bar PRIVATE foo)
    
add_library(bar_s STATIC bar.c)
target_link_libraries(bar_s foo)

add_executable(app_d main.c)
target_link_libraries(app_d bar)

add_executable(app_s main.c)
target_link_libraries(app_s bar_s)

install( TARGETS app_s app_d bar foo
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION static_lib)
    


