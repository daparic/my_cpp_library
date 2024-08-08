
# ROS2 tips:

## Create project:
```
source /opt/ros/humble/setup.bash
ros2 pkg create my_cpp_library --build-type ament_cmake
```

## Add C/C++ files and googletest testcases:
```
$ find . -type f \( -name '*.h' -o -name '*.cpp' \)
./include/my_cpp_library/library_header.h
./install/my_cpp_library/include/my_cpp_library/library_header.h
./src/main.cpp
./src/my_cpp_library.cpp
./test/main.cpp
./test/savings_account_test.cpp
```

## Prepare `cmake`
```
# copy from Parasoft folder to here and adjust `CPPTEST_COMPILER_ID`
ls -l cmake/cpptest-coverage.cmake

# edit this
ls -l CMakeLists.txt
```

## Build
```
colcon build --cmake-args -DCPPTEST_COVERAGE=ON
colcon test

# other miscellaneous commands below
colcon build
colcon test --packages-select my_cpp_library
colcon test-result --test-result-base build/my_cpp_library/
colcon test-result
```

## Generate Parasoft coverage report:
```
cd build/my_cpp_library/
make cpptestcov-compute
make cpptestcov-report
```
