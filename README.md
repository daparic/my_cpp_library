
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

STM32 firmware:
```
openocd -f interface/stlink-v2.cfg -f target/stm32g0x.cfg -c init -c "reset halt" -c "flash read_bank 0 blinky-fw.bin 0 0x20000" -c "reset" -c shutdown
openocd -f interface/stlink-v2.cfg -f target/stm32g0x.cfg -c init -c "reset halt" -c "flash write_image erase blinky-fw.bin 0x08000000" -c "reset" -c shutdown
```
