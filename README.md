# Ouster_ROS_Gazebo_Rviz

---

## 硬體設備與環境

Geforce RTX 2080  
Ubuntu 18.04  
ROS Melodic  
Gazebo9  
CUDA 11  
Anaconda  
python 3.9.5  

---
## How to use  

---
### ROS Melodic: 
##### 參考安裝連結 http://wiki.ros.org/melodic/Installation/Ubuntu
1. 設定安裝源:  
  ```sh
  $ sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
  ```
2. keys:  
  ```sh
  $ sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116
  ```
3. install:  
  ```sh
  $ sudo apt-get update
  $ sudo apt-get install ros-melodic-desktop-full
  ```
3. (a) 如果安裝失敗且出下列錯誤:
  ```sh
    E: Failed to fetch http://us.archive.ubuntu.com/ubuntu/pool/universe/v/vtk6/libvtk6.3_6.3.0+dfsg1-11build1_amd64.deb  Connection failed [IP: 91.189.91.26 80]
    E: Unable to fetch some archives, maybe run apt-get update or try with --fix-missing?
  ```
3. (b) 則執行:  
  ```sh
  $ sudo apt-get update --fix-missing
  ```
3. (c) 完成後再次執行:  
  ```sh
  $ sudo apt-get install ros-melodic-desktop-full
  ```
4. 完成安裝ROS Melodic後先初始化:  
  ```sh
  $ sudo rosdep init
  $ rosdep update
  ```
5. 環境配置: 因為之前會與 ROS 的 PYTHON 2 有衝突所以個人沒有做此指令，不做下列環境配置的缺點就是，每次開新的terminal都要專為該terminal重新用 `source /opt/ros/melodic/setup.bash` 去激活 ROS Melodic 
  ```sh
  $ echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc source ~/.bashrc
  ```
5. (a) 有時候忘記很麻煩，所以怕忘記就用上述的配置，反正現在 ROS 全面使用 PYTHON 3 了應該不會再出錯。
6. 安裝 rosinstall:  
  ```sh
  $ sudo apt-get install python-rosinstall python-rosinstall-generator python-wstool build-essential 
  ```
7. 測試是否安裝成功:  
  ```sh
  $ roscore
  ```
9. Search gazebo version, version needs to be gazebo9.
  ```sh 
  $ dpkg -l|grep gazebo 
  ```
9. (a) 由於 ros-melodic-desktop-full 應該內建 gazebo9, 如果版本不對的要去查 gazebo 安裝特定版本方式
---

### Virtual Environment: 
  ```sh
  $ conda create --name ros_py3 python=3.9.5 
  $ conda activate ros_py3
  ```
---

### Run the demo

  ```sh
  $ source activate ros_py3
  $ source /opt/ros/melodic/setup.bash
  $ mkdir -p ~/catkin_ws/src
  $ cd ~/catkin_ws/src
  $ git clone https://github.com/wilselby/ouster_example
  $ cd ..
  $ catkin_make
  $ source ~/catkin_ws/devel/setup.bash
  $ roslaunch ouster_description os1_world.launch
  ```
  
##### 詳細結果可參考原作者: https://www.wilselby.com/2019/05/simulating-an-ouster-os-1-lidar-sensor-in-ros-gazebo-and-rviz/
