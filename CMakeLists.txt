cmake_minimum_required(VERSION 2.6)

project(3dv_tutorial)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_BUILD_TYPE Release)
find_package(OpenCV REQUIRED)
find_package(Ceres REQUIRED)

set(SRC_DIR	"${CMAKE_SOURCE_DIR}/examples")
set(BIN_DIR	"${CMAKE_SOURCE_DIR}/bin")

file(GLOB APP_SOURCES "${SRC_DIR}/*.cpp")
foreach(app_source ${APP_SOURCES})
    string(REPLACE ".cpp" "" app_name ${app_source})
    string(REPLACE "${SRC_DIR}/" "" app_name ${app_name})
    add_executable(${app_name} ${app_source})
    target_include_directories(${app_name} ${CERES_INCLUDE_DIRS})
    target_link_libraries(${app_name} ${OpenCV_LIBS} ${CERES_LIBRARIES})
    install(TARGETS ${app_name} DESTINATION ${BIN_DIR})
endforeach(app_source ${APP_SOURCES})
