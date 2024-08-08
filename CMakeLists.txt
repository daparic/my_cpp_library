cmake_minimum_required(VERSION 3.8)
project(my_cpp_library)

if (NOT CMAKE_C_STANDARD)
    set(CMAKE_C_STANDARD 99)
endif()

if (NOT CMAKE_CXX_STANDARD)
    set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

if(CPPTEST_COVERAGE)
    include("${CMAKE_CURRENT_LIST_DIR}/cmake/cpptest-coverage.cmake")
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
# uncomment the following section in order to fill in
# further dependencies manually.
# find_package(<dependency> REQUIRED)

include_directories(include/my_cpp_library)
set(HEADER_FILES include/my_cpp_library/library_header.h)
add_library(my_lib src/my_cpp_library.cpp ${HEADER_FILES})
# add_library(my_lib src/my_cpp_library.cpp)
add_executable(main src/main.cpp)
target_link_libraries(main PUBLIC my_lib)
install(TARGETS main DESTINATION lib/${PROJECT_NAME}/)
ament_export_targets(my_lib HAS_LIBRARY_TARGET)
install(DIRECTORY include/my_cpp_library DESTINATION include)
install(
    TARGETS my_lib
    EXPORT my_lib
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    RUNTIME DESTINATION bin
    INCLUDES DESTINATION include)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  # the following line skips the linter which checks for copyrights
  # comment the line when a copyright and license is added to all source files

  find_package(ament_cmake_gtest REQUIRED)
  set(TESTFILES test/main.cpp test/savings_account_test.cpp)
  ament_add_gtest(${PROJECT_NAME}_test ${TESTFILES})
  target_link_libraries(${PROJECT_NAME}_test my_lib)
  install(TARGETS ${PROJECT_NAME}_test DESTINATION lib/${PROJECT_NAME})

  set(ament_cmake_copyright_FOUND TRUE)
  # the following line skips cpplint (only works in a git repo)
  # comment the line when this package is in a git repo and when
  # a copyright and license is added to all source files
  set(ament_cmake_cpplint_FOUND TRUE)
  # ament_lint_auto_find_test_dependencies()
endif()

ament_package()
