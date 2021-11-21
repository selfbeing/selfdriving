# Path-Planning-Project

---

## Simulator

在这里 [releases tab](<https://github.com/udacity/self-driving-car-sim/releases>)下载模拟器.

## Goals

本项目的目标是在虚拟公路上安全导航，其他车辆以50 MPH限速+10 MPH行驶。你将获得汽车的定位和传感器融合数据，还有一个公路周围路径点的稀疏地图列表。车辆应尽量接近50英里/小时的速度行驶，这意味着在可能的情况下超过较慢的车辆，注意其他车辆也会尝试改变车道。除非从一条车道开到另一条车道，否则车辆应不惜一切代价避免撞到其他车辆，并始终在标记的道路车道内行驶。这辆车应该能够在6946米的公路上绕一圈。由于汽车正试图以每小时50英里的速度行驶，因此完成一个循环需要5分钟多一点的时间。此外，车辆的总加速度不应超过10 m/s^2，且颠簸不应超过50 m/s^3。

### 高速地图在`data/highway_map.txt`

列表中的每个航路点都包含[x,y,s,dx,dy]值。x和y是航路点的地图坐标位置，s值是沿道路到达该航路点的距离，单位为米，dx和dy值定义了指向公路环路外部的单位向量。
公路的航路点环绕一圈，因此frenet s值（沿公路的距离）从0变为6945.554。

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./path_planning`.

Here is the data provided from the Simulator to the C++ Program

### Main car's localization Data (No Noise)

[x] The car's x position in map coordinates

[y] The car's y position in map coordinates

[s] The car's s position in frenet coordinates

[d] The car's d position in frenet coordinates

[yaw] The car's yaw angle in the map

[speed] The car's speed in MPH

### Previous path data given to the Planner

//Note: Return the previous list but with processed points removed, can be a nice tool to show how far along
the path has processed since last time.

[previous_path_x] The previous list of x points previously given to the simulator

[previous_path_y] The previous list of y points previously given to the simulator

#### Previous path's end s and d values

[end_path_s] The previous list's last point's frenet s value

[end_path_d] The previous list's last point's frenet d value

#### Sensor Fusion Data, a list of all other car's attributes on the same side of the road. (No Noise)

[sensor_fusion] A 2d vector of cars and then that car's [car's unique ID, car's x position in map coordinates, car's y position in map coordinates, car's x velocity in m/s, car's y velocity in m/s, car's s position in frenet coordinates, car's d position in frenet coordinates.

## 细节

1.这款车使用完美的控制器，每0.02秒访问列表中的每一个（x,y）点。（x,y）点的单位是米，点的间距决定了汽车的速度。列表中从一个点到下一个点的矢量指示汽车的角度。测量切向和径向加速度以及总加速度的变化率。计划者接收到的（x,y）点路径的总加速度不应超过10 m/s^2，同时冲击不应超过50 m/s^3。（注意：由于这是BETA，这些要求可能会改变。此外，目前的jerk超过0.02秒的间隔，最好在1秒内平均总加速度，并从中测量jerk。

2.在模拟器运行和路径规划器返回路径之间会有一些延迟，优化代码通常不会很长，可能只有1-3个时间步。在此延迟期间，模拟器将继续使用上次给出的点，因为这是一个好主意，可以存储最后使用的点，这样您就可以有平滑转换。上一个路径对于此转换很有帮助，因为它们显示了给定给模拟器控制器的最后一个点，并且处理的点已被删除。您可以返回一个扩展上一个路径的路径，或者确保创建一个新路径，该路径与上一个路径平滑过渡。

## Tips

A really helpful resource for doing this project and creating smooth trajectories was using <http://kluge.in-chemnitz.de/opensource/spline/>, the spline function is in a single hearder file is really easy to use.

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
  * Run either `install-mac.sh` or `install-ubuntu.sh`.
  * If you install from source, checkout to commit `e94b6e1`, i.e.

    ```
    git clone https://github.com/uWebSockets/uWebSockets 
    cd uWebSockets
    git checkout e94b6e1
    ```
