# 项目介绍

你的机器人被绑架并运到了一个新的地方！幸运的是，它有一张这个位置的地图，一个（嘈杂的）GPS初始位置估计，以及大量（嘈杂的）传感器和控制数据。
在这个项目中，将在C++中实现一个2维粒子滤波器。粒子过滤器将获得一张地图和一些初始定位信息（类似于GPS提供的信息）。在每个时间步，粒子滤波器也将获得观察和控制数据。

## 运行代码

本项目基于优达的模拟器，[此处](https://github.com/udacity/self-driving-car-sim/releases)下载。

该存储库包括两个文件，可用于为Linux或Mac系统设置和安装uWebSocketIO。对于windows，可以使用Docker、VMware甚至Ubuntu上的Windows10Bash来安装uWebSocketIO。
uWebSocketIO的安装完成后，可以通过从项目顶部目录执行以下操作来构建和运行主程序。

```
mkdir build
cd build
cmake ..
make
./particle_filter
```

完成项目需要编写的程序是`src/particle_filter.cpp`和`particle_filter.h`
以下是main.cpp用于uWebSocketIO与模拟器通信的主协议。
输入：模拟器提供给C++程序的值

```
// sense noisy position data from the simulator

["sense_x"] 

["sense_y"] 

["sense_theta"] 

// get the previous velocity and yaw rate to predict the particle's transitioned state

["previous_velocity"]

["previous_yawrate"]

// receive noisy observation data from the simulator, in a respective list of x/y values

["sense_observations_x"] 

["sense_observations_y"] 
```

输出：由C++程序提供给模拟器的值

```
// best particle values used for calculating the error evaluation

["best_particle_x"]

["best_particle_y"]

["best_particle_theta"] 

//Optional message data used for debugging particle's sensing and associations

// for respective (x,y) sensed positions ID label 

["best_particle_associations"]

// for respective (x,y) sensed positions

["best_particle_sense_x"] <= list of sensed x positions

["best_particle_sense_y"] <= list of sensed y positions
```

此项目的主要工作是构建“particle_filter.cpp”中的方法，直到模拟器输出显示：

```
Success! Your particle filter passed!
```

## 粒子滤波器的实现

此存储库的目录结构如下所示：

```
root
|   build.sh
|   clean.sh
|   CMakeLists.txt
|   README.md
|   run.sh
|
|___data
|   |   
|   |   map_data.txt
|   
|   
|___src
    |   helper_functions.h
    |   main.cpp
    |   map.h
    |   particle_filter.cpp
    |   particle_filter.h
```

### 粒子滤波器的输入

可以在`data`目录中找到粒子过滤器的输入。

#### 地图*

`map_data.txt`包括地标在任意笛卡尔坐标系上的位置（以米为单位）。每行有三列
1.x位置
2.y位置
3.地标id

### 模拟器提供的所有其他数据，如观察和控制

> * Map data provided by 3D Mapping Solutions GmbH.
