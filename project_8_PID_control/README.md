# Controls-PID

该项目实现了一个PID控制器，通过适当调整转向角使汽车保持在车道上。

## Overview

<table style="width:100%">
  <tr>
    <th>
      <p align="center">
       <img src="./img/control_none.gif" alt="Overview" width="80%">
      </p>
    </th>
    <th>
      <p align="center">
       <img src="./img/control_p.gif" alt="Overview" width="80%">
      </p>
    </th>
    <th>
      <p align="center">
       <img src="./img/control_pid.gif" alt="Overview" width="80%">
      </p>
    </th>
  </tr>
  </table>
  
## 什么是PID控制器

**比例-积分-微分控制器**（PID控制器）是最常见的控制回路反馈机制之一。PID控制器连续计算**误差函数**（在我们的例子中是距离车道中心的距离），并根据比例（P）、积分（I）和微分（D）项进行校正。

### PID参数的选择

PID控制器的行为取决于三个主要参数，即**比例**、**积分**和**微分增益**。这三个参数中的每一个都控制各自控制器响应的强度。

1. **比例增益**调节给定误差变化时输出变化的大小。如果比例增益过高，系统可能会变得不稳定。
2. **积分增益**与误差大小和误差持续时间成比例。通过这种方式，控制器能够消除纯比例控制器产生的残余稳态误差（即纯比例控制器仅在误差非零时运行），并且能够处理系统偏差。
3. **微分增益**决定计算响应时考虑的误差变化率。换句话说，如果期望的设定点越来越接近（=误差减小），则必须平滑响应，以避免超出目标。微分分量有利于系统的稳定性和稳定时间。

在当前项目中，通过定性检查模拟器中的驾驶行为来手动调整参数，以响应参数的变化。参数验证也可以在无头模式可用的模拟器中轻松自动执行。

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
* [uWebSockets](https://github.com/uWebSockets/uWebSockets)
  * Run either `./install-mac.sh` or `./install-ubuntu.sh`.
  * If you install from source, checkout to commit `e94b6e1`, i.e.

    ```
    git clone https://github.com/uWebSockets/uWebSockets 
    cd uWebSockets
    git checkout e94b6e1
    ```

    Some function signatures have changed in v0.14.x. See [this PR](https://github.com/udacity/CarND-MPC-Project/pull/3) for more details.
* Simulator. You can download these from the [project intro page](https://github.com/udacity/self-driving-car-sim/releases) in the classroom.

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./pid`.
