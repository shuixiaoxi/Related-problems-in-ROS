 

1、 针对每次都要source

Method1:echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc

Method2:gedit ~/.bashrc  在文件末尾添加 source ~/catkin_ws/devel/setup.bash

 

2、 针对仿真中，打开仿真机器人摄像头看到的画面的指令

```
rosrun image_view image_view image:=/camera/rgb/image_raw
 
3、 缺少ros包，安装的指令
sudo apt-get install ros-kinetic-包名
 
4、 创建工作空间
mkdir -p catkin_ws/src 
 
Attention:运行launch文件时不需要roscore来激活master，因为launch文件会默认运行roscore.
 
5、 打开深度摄像机以及普通摄像机的命令
rosrun image_view image_view image:=/camera/depth/image_raw（深度）
```

rosrun image_view image_view image:=/camera/rgb/image_raw

 

6、 运行xbot真是机器人的步骤

https://github.com/YunxiangLuo/ros/tree/master/chapter4/class2

 

7、 针对运行roslaunch robot_sim_demo robot_spawn.launch 时报（GazeboRosControlPlugin missing <legacyModeNS> while using DefaultRobotHWSim, defaults to true.）

在ROS-Academy-for-Beginners/robot_sim_demo/urdf文件中的xbot-u.gazebo中72行后加上<legacyModeNS>true</legacyModeNS>即可。

 

8、 针对运行roslaunch robot_sim_demo robot_spawn.launch 时报Failed to load nodelet [/cmd_vel_mux] of type [yocs_cmd_vel_mux/CmdVelMuxNodelet](类似这种load什么失败的一般就是没有下载，按照下1)下载应该就可以了)

1） sudo apt-get install ros-kinetic-yocs-cmd-vel-mux

2） 打开ROS-Academy-for-Beginners/robot_sim_demo文件中的package.xml

在34行后加<nodelet plugin="${prefix}/nodelets.xml"/>

 

9、 针对运行roslaunch robot_sim_demo robot_spawn.launch 时报[gazebo_gui-3] process has died [pid 3690, exit code 134, cmd /opt/ros/kinet

Method1：终端执行1.killall gzserver 2.  killall gzclient 

Method2：终端执行 export SVGA_VGPU10=0

如果两个单独操作都解决不了，则两个方法都操作后在运行仿真。

Method3：升级gazebo7.0--->7.16

步骤：1)、sudo sh -c 'echo "deb http://packages.osrfoundation.org/gazebo/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/gazebo-stable.list'

2）、sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys D2486D2DD83DB69272AFE98867170598AF249743

3）、sudo apt update

4）、sudo apt upgrade

 

10、      针对运行仿真，即roslaunch robot_sim_demo robot_spawn.launch后，再运行rosrun slam_sim_demo gmapping_demo.launch，如果出现仿真gazebo出现闪退或者后续运行的rosrun slam_sim_demo view_slam.launch中rviz界面的tf等几个属性报错（显红），大概率原因是虚拟机分配的运行内存不够，分配8G试试。

 

11、针对安装ROS，初始化时rosdep update 出错的解决办法

​    https://blog.csdn.net/super_sean/article/details/105433250

 

```
12、rosbag记录节点运行，运行rosbag record –a，仿真终端报错Compressed Depth Image Transport - Compression requires single-channel 32bit
     运行命令执行 rosbag record -a -x "(.*)/compressed(.*)" 命令
```

 
```
13、rosdep install --from-paths src --ignore-src --rosdistro=kinetic -y
 出现the following packages/stacks could not have their rosdep keys resolved to system dependencies
 运行
 rosdep update --include-eol-distros
 可以修复问题。
```
 
 14  ROS-Academy-for-Beginners ：gazebo9中模型不显示，但在view的collision中有模型碰撞图
       在对应模型的dae文件中的
 ```
   <transparent opaque="A_ONE">
              <color>1 1 1 0</color>
            </transparent>
 ```
 改为
 ```
    <transparent opaque="A_ONE">
              <color>1 1 1 1</color>     ######四个一
            </transparent>
            <transparency><float>1</float></transparency>
 ```
 
 15  运行py文件报错：/usr/bin/env: "python\r":没有那个文件或目录
     用VIM打开该文件
         按一下ESC
         输入
         :set ff=unix    #####千万别少了“:”冒号
         后回车
         输入
         :wq
         回车

 
 
