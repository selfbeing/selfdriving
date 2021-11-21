# Controls-MPC

---

## 项目说明

### 概述

**模型预测控制（MPC）** 是一种先进的过程控制方法，它依赖于过程的动态模型。

MPC控制器框架由四个主要组件组成：

- **优化过程中考虑的轨迹**。这是由若干时间步间隔时间**dt**参数化的。显然，优化的变量数量与*N*成正比，因此在存在计算约束的情况下必须考虑这一点。

- **车辆模型**，这是一组描述系统行为和跨时间步更新的方程式。在我们的案例中，我们使用了一个简化的运动学模型（所谓的*bycicle模型*），由六个参数的状态描述：
-- **x**位置（*x轴*）
-- **y**位置（*y轴*）
-- **汽车的前进方向**
-- **车辆速度**
-- **cte**交叉跟踪错误
-- **epsi**方向错误
  车辆模型更新方程在[MPC.cpp](src/MPC.cpp)中的第117-123行实现.

- **约束**对控制器响应中的约束建模所需。例如，一辆汽车永远无法在一个时间步长内驾驶90度。在本项目中，我们将这些约束设置如下：
-- **转向**：在范围[-25°，25°]内
-- **加速度**：在从全制动到全油门的[-1,1]范围内

- **成本函数**：其优化基于整个控制过程。通常，成本函数是由不同项的和组成的。除了依赖于主要成本函数（例如交叉轨迹或航向误差）外，还存在其他成本函数项以加强控制器响应的平滑性（避免突然转向）。在本项目中，成本函数在[MPC.cpp](src/MPC.cpp)中的第54-79行执行.

## 调整参数

**N**和**dt**都是优化过程中的基本参数。特别是，**T=N*dt**构成了优化过程中考虑的*预测范围*。这些值必须根据以下几点进行调整：

- 较大的**dt**导致不太频繁的驱动，这反过来可能导致难以遵循连续参考轨迹（所谓的*离散化误差*）。尽管有一个大的*T*会有利于控制过程，但是考虑到在未来的预测太远在现实的场景中是没有意义的。
- 大**T**和小**dt**导致大**N**。如上所述，优化的变量数量与*N*成正比，因此将导致更高的计算成本。在当前项目中，我（通过在模拟器中目视检查车辆的行为）将这些参数设置为**N=10**和**dt=0.1**，则**T=1s**。

### 改变参考系

模拟器提供全球参考系统中的坐标。为了便于以后的计算，在[main.cpp](src/main.cpp)中的第94-102行将其转换为car自己的参考系.

### 处理延迟

为了模拟汽车立即启动指令的真实驾驶条件，在向模拟器发送数据消息之前引入了*100ms*延迟时间（在[main.cpp](src/main.cpp)中的第185行）. 为了处理延迟，将状态提前一个时间步预测，然后再将其反馈给解算器（在[main.cpp](src/main.cpp)中的第125-132行）.

---

## Dependencies

- cmake >= 3.5
- All OSes: [click here for installation instructions](https://cmake.org/install/)
- make >= 4.1
  - Linux: make is installed by default on most Linux distros
  - Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  - Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
- gcc/g++ >= 5.4
  - Linux: gcc / g++ is installed by default on most Linux distros
  - Mac: same deal as make - [install Xcode command line tools]((<https://developer.apple.com/xcode/features/>)
  - Windows: recommend using [MinGW](http://www.mingw.org/)
- [uWebSockets](https://github.com/uWebSockets/uWebSockets)
  - Run either `install-mac.sh` or `install-ubuntu.sh`.
  - If you install from source, checkout to commit `e94b6e1`, i.e.

    ```
    git clone https://github.com/uWebSockets/uWebSockets 
    cd uWebSockets
    git checkout e94b6e1
    ```

    Some function signatures have changed in v0.14.x. See [this PR](https://github.com/udacity/CarND-MPC-Project/pull/3) for more details.
- Fortran Compiler
  - Mac: `brew install gcc` (might not be required)
  - Linux: `sudo apt-get install gfortran`. Additionall you have also have to install gcc and g++, `sudo apt-get install gcc g++`. Look in [this Dockerfile](https://github.com/udacity/CarND-MPC-Quizzes/blob/master/Dockerfile) for more info.
- [Ipopt](https://projects.coin-or.org/Ipopt)
  - Mac: `brew install ipopt`
  - Linux
    - You will need a version of Ipopt 3.12.1 or higher. The version available through `apt-get` is 3.11.x. If you can get that version to work great but if not there's a script `install_ipopt.sh` that will install Ipopt. You just need to download the source from the Ipopt [releases page](https://www.coin-or.org/download/source/Ipopt/) or the [Github releases](https://github.com/coin-or/Ipopt/releases) page.
    - Then call `install_ipopt.sh` with the source directory as the first argument, ex: `bash install_ipopt.sh Ipopt-3.12.1`.
  - Windows: TODO. If you can use the Linux subsystem and follow the Linux instructions.
- [CppAD](https://www.coin-or.org/CppAD/)
  - Mac: `brew install cppad`
  - Linux `sudo apt-get install cppad` or equivalent.
  - Windows: TODO. If you can use the Linux subsystem and follow the Linux instructions.
- [Eigen](http://eigen.tuxfamily.org/index.php?title=Main_Page). This is already part of the repo so you shouldn't have to worry about it.
- Simulator. You can download these from the [releases tab](https://github.com/udacity/self-driving-car-sim/releases).
- Not a dependency but read the [DATA.md](./DATA.md) for a description of the data sent back from the simulator.

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./mpc`.
