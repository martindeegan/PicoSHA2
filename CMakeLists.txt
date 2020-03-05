cmake_minimum_required(VERSION 3.5)
project(picosha2 CXX)

# find system dependencies
find_package(ament_cmake REQUIRED)

add_library(picosha2 INTERFACE)
target_include_directories(picosha2 INTERFACE "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>"
                                           "$<INSTALL_INTERFACE:include>")

ament_export_include_directories(include)
ament_export_libraries(picosha2)
ament_export_interfaces(export_picosha2 HAS_LIBRARY_TARGET)

install(
  TARGETS picosha2
  EXPORT export_picosha2
  RUNTIME DESTINATION bin
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib
  INCLUDES
  DESTINATION include)

install(DIRECTORY include/ DESTINATION include)

if(BUILD_TESTING)
    find_package(ament_cmake_gtest REQUIRED)

    ament_add_gtest(test_picosha2 test/test.cpp)
    target_link_libraries(test_picosha2 picosha2)
endif()

ament_package()
