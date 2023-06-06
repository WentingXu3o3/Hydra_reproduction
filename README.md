# Hydra_reproduction
Hydra算法复现
https://github.com/MIT-SPARK/Hydra

## 1.没有ROS装ROS（Robotic Operation System）
环境：Ubuntu 20.04
选择：ROS Noetic (recommended)
http://wiki.ros.org/noetic/Installation/Ubuntu

1.Installation
![image](https://github.com/WentingXu3o3/Hydra_reproduction/assets/59476953/e64bed25-2b02-455a-aad8-96cffe0dd1e7)
点进链接 配置ubuntu Repositories 给予权限 注意：这个software配置在程序库中 不在setting中![image](https://github.com/WentingXu3o3/Hydra_reproduction/assets/59476953/d98279d1-802d-450b-aaa1-1d53ad674252)

1.4安装，选择recommend

![image](https://github.com/WentingXu3o3/Hydra_reproduction/assets/59476953/b15005f2-33d3-441d-9205-ad8779725b60)
## 2.装ROS noetic:

![Screenshot 2023-06-06 at 11 57 03](https://github.com/WentingXu3o3/Hydra_reproduction/assets/59476953/26ff90f1-bb46-42eb-ad3b-500d2faaf2ef)
## 3.Building Hydra
```
mkdir -p catkin_ws/src
cd catkin_ws
catkin init
catkin config -DCMAKE_BUILD_TYPE=Release -DGTSAM_TANGENT_PREINTEGRATION=OFF \
              -DGTSAM_BUILD_WITH_MARCH_NATIVE=OFF -DOPENGV_BUILD_WITH_MARCH_NATIVE=OFF
catkin config --blacklist hdf5_map_io mesh_msgs_hdf5 label_manager mesh_tools \
                          rviz_map_plugin minkindr_python

cd src
git clone git@github.com:MIT-SPARK/Hydra.git hydra
```
```
vcs import . < hydra/install/hydra.rosinstall

rosdep install --from-paths . --ignore-src -r -y
sudo apt install libprotobuf-dev protobuf-compiler

cd ..
catkin build
```
catkin build需要全部成功
### 如果catkin build失败的话
检查错误 如果import em 或者empy 报错
则是empy没有装在python3的库中，可能装在了ubuntu系统python中，原因可能是pip或者sudo pip 造成

empy 用pip3来装 装在anaconda中
![image](https://github.com/WentingXu3o3/Hydra_reproduction/assets/59476953/1ae655bf-a659-44ac-a130-ba2654dc0700)
检查一下em
![image](https://github.com/WentingXu3o3/Hydra_reproduction/assets/59476953/4fbd0313-eddf-4969-b6b2-f3cc018919bf)
rospkg 也同样
![image](https://github.com/WentingXu3o3/Hydra_reproduction/assets/59476953/5dca77f2-933b-45c8-9678-165bf766fed5)

成功界面
![IMG_2031](https://github.com/WentingXu3o3/Hydra_reproduction/assets/59476953/907eb59a-0105-40ca-8b1d-0b68b267d582)



## 4.Running Hydra (Quickstart)
通过链接下载office包，文件较大，下载和解压都需要耐心
还可以在这里下载其他房间https://web.mit.edu/sparklab/datasets/uHumans2/ 
00h表示数据中没有人
uHumans 的数据只有如下
![Screenshot 2023-06-06 at 12 08 54](https://github.com/WentingXu3o3/Hydra_reproduction/assets/59476953/6c98eddb-b308-46db-81d8-5d1e97ab8db1)

### rosbag decompress path/to/bagfile 解压
53min
![IMG_2037](https://github.com/WentingXu3o3/Hydra_reproduction/assets/59476953/8cc6e993-0dbd-4af8-a1fd-10711eab5bd6)
orig为解压后的文件

![IMG_2036](https://github.com/WentingXu3o3/Hydra_reproduction/assets/59476953/ac95eb8d-af64-4a26-b2aa-786c813d8cb6)

### To start Hydra:
roslaunch hydra_dsg_builder uhumans2_incremental_dsg.launch start_visualizer:=true
### Then, start the rosbag in a separate terminal:另开一个terminal
![IMG_2033](https://github.com/WentingXu3o3/Hydra_reproduction/assets/59476953/16e27a81-86ff-4112-97f2-6816001d00ed)

## 5.效果
![IMG_2035](https://github.com/WentingXu3o3/Hydra_reproduction/assets/59476953/8984c566-808b-48ce-bed0-3f90e5eb749a)

![IMG_2039](https://github.com/WentingXu3o3/Hydra_reproduction/assets/59476953/0b6ddb3e-4686-40bb-8af6-4952de9cfa5e)

