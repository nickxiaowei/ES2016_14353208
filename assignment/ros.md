### ROS的安装以及体验cartographer ###

### ROS的安装 ###

根据

> http://wiki.ros.org/jade/Installation/Ubuntu

所给步骤完成实验。



- Setup up your sources.list

	`sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'`

- Set up your keys

	`sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 0xB01FA116`

- Installation

	`sudo apt-get update`

   安装完整包：

   `sudo apt-get install ros-jade-desktop-full`

- Initialize rosdep

   ```
sudo rosdep init
rosdep update
   ```

- Environment setup

   ```
echo "source /opt/ros/jade/setup.bash" >> ~/.bashrc
source ~/.bashrc
   ```

- Getting rosinstall

   `sudo apt-get install python-rosinstall`

- Obtain source code of the installed packages

   `apt-get source ros-jade-laser-pipeline`

至此ROS安装完成

### 谷歌Cartographer学习的安装 ###

1. 安装所有依赖项

   ```
sudo apt-get install -y google-mock libboost-all-dev  libeigen3-dev libgflags-dev 
libgoogle-glog-dev liblua5.2-dev libprotobuf-dev  libsuitesparse-dev libwebp-dev 
ninja-build protobuf-compiler python-sphinx  ros-indigo-tf2-eigen libatlas-base-dev 
libsuitesparse-dev liblapack-dev
   ```

2. 首先安装ceres solver，选择的版本是1.11

   ```
1.git clone https://github.com/hitcm/ceres-solver-1.11.0.git
2.cd ceres-solver-1.11.0/build
3.cmake ..
4.make 
5.sudo make install
   ```

3. 然后安装cartographer

   ```
1.git clone https://github.com/hitcm/cartographer.git
2.cd cartographer/build
3.cmake .. -G Ninja
4.ninja
5.ninja test
6.sudo ninja install
   ```

4. 安装cartographer_ros

   ```
1.mkdir catkin_ws
2.git clone https://github.com/hitcm/cartographer_ros.git
3.将得到的文件夹放入catkin_ws的src文件夹内
4.cd catkin_ws
5.catkin_make
   ```

5. 数据下载测试

   1.2d数据：https://storage.googleapis.com/cartographer-public-data/bags/backpack_2d/cartographer_paper_deutsches_museum.bag
   
   2.3d数据：https://storage.googleapis.com/cartographer-public-data/bags/backpack_3d/cartographer_3d_deutsches_museum.bag

   对ros的catkin_ws进行配置：

   ```
source ~/catkin_ws/devel/setup.bash
rospack profile
   ```

   然后运行launch文件即可：

   ```
roslaunch cartographer_ros demo_backpack_2d.launch bag_filename:=${HOME}/Downloads/cartographer_paper_deutsches_museum.bag
roslaunch cartographer_ros demo_backpack_3d.launch bag_filename:=${HOME}/Downloads/cartographer_3d_deutsches_museum.bag
   ```

### 最终得到的结果 ###

2d:

![](https://raw.githubusercontent.com/nickxiaowei/markdownpicture/master/ROS_2D.png)

3d:

![](https://raw.githubusercontent.com/nickxiaowei/markdownpicture/master/ROS_3D.png)
