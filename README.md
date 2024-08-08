
ROS2 tips:
```
ros2 pkg create my_cpp_library --build-type ament_cmake
colcon build
colcon test

colcon build --cmake-args -DCPPTEST_COVERAGE=ON
colcon test --packages-select my_cpp_library
colcon test-result --test-result-base build/my_cpp_library/
colcon test-result

make cpptestcov-compute
make cpptestcov-report
```
