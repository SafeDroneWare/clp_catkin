cmake_minimum_required(VERSION 2.8.3)
project(clp_catkin)

find_package(catkin REQUIRED)
catkin_package(
  INCLUDE_DIRS ${CATKIN_DEVEL_PREFIX}/include
)

include(ExternalProject)

file(MAKE_DIRECTORY ${CATKIN_DEVEL_PREFIX}/include)

ExternalProject_Add(clp_src
  URL https://www.coin-or.org/download/source/Clp/Clp-1.16.11.tgz
  CONFIGURE_COMMAND cd ../clp_src && ./configure -C --prefix=${CATKIN_DEVEL_PREFIX}
  BUILD_COMMAND cd ../clp_src && make -j8
  INSTALL_COMMAND cd ../clp_src && make install -j8
)

add_library(${PROJECT_NAME} src/dependency_tracker.cc)
add_dependencies(${PROJECT_NAME} clp_src)