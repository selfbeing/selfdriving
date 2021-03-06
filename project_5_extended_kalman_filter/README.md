# Extended Kalman Filter Project(EKF)

## Project Description

该代码实现了C++中的扩展卡尔曼滤波器。通过模拟激光雷达和雷达测量，检测在车辆周围行驶的自行车。将使用卡尔曼滤波器、激光雷达测量和雷达测量来跟踪自行车的位置和速度。

---

## Dependencies

* cmake >= 3.5
  * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools]((<https://developer.apple.com/xcode/features/>)
  * Windows: recommend using [MinGW](http://www.mingw.org/)

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
   * On windows, you may need to run: `cmake .. -G "Unix Makefiles" && make`
4. Run it: `./ExtendedKF path/to/input.txt path/to/output.txt`. You can find
   some sample inputs in 'data/'.
    * eg. `./ExtendedKF ../data/sample-laser-radar-measurement-data-1.txt output.txt`
