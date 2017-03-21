# ORB_SLAM的安装指南
[TOC]
###安装参考教程
官方推荐
>https://github.com/raulmur/ORB_SLAM
>另一篇中文帖子
>http://blog.csdn.net/Fishmemory/article/details/53288140

###安装过程中遇到的问题及解决方案
####安装ros出现的问题
- 由于官网提供的没有Ubuntu14.04版本的ros的安装方法。
1. 参考这篇帖子上的ros安装方法即可
>[Ubuntu14.04安装和配置ROS Indigo](http://www.jianshu.com/p/04be841e2293)

说明：官网上执行的安装是安装 ` Fuerte, Groovy and Hydro` 版本的ROS，这是支持Ubuntu14.04以前的版本，在Ubuntu14.04中，使用indigo版本的ROS。故需要执行的是 `sudo apt-get install ros-indigo-desktop-full`

** 注意**，在官方github推荐的ORB_SLAM的安装中，fuerte是指的ROS版本fuerte，但是在Ubuntu14.04下，需要安装的是indigo，需要将官方推荐的安装教程中的fuerte替换为indigo

####编译ORB_SLAM项目需要注意的事情
特别需要注意的是，如果ROS安装的版本是ROS Indigo，需要将根目录下的manifest.xml文件中的opencv2依赖一行的代码去掉！
具体操作就是：
```text
打开manifest.xml文件，注释掉:
<!-- <depend package="opencv2"/> -->
````

##### 编译ORB_SLAM错误
- 错误描述
```text
执行roscore
新打开终端，执行 roslaunch ExampleGroovyOrNewer.launch
```
遇到错误为：
```text
raise ResourceNotFound(name, ros_paths=self._ros_paths)
ResourceNotFound: ORB_SLAM
ROS path [0]=/opt/ros/indigo/share/ros
ROS path [1]=/opt/ros/indigo/share
ROS path [2]=/opt/ros/indigo/stacks
```
- 错误原因
是因为没有将ORB_SLAM的项目没有放在ROS的workspace里面
- 解决办法一
	1. 将ORB_SLAM放入ROS的默认workspace中
	2. 执行 `echo $ROS_PACKAGE_PATH` 查看默认的workspace， 我电脑得到的是 `/opt/ros/indigo/share:/opt/ros/indigo/stacks`
	3. 将ORB_SLAM整个移动到上面的文件路径中（不推荐）
- 解决办法二
	1. 生成ROS的workspace
	2. 依次执行下面命令
	```text
	mkdir -p ~/catkin_ws/src
	```
	NOTE: catkin_ws是工作空间的名字，当然你可以随意指定；src是存放功能包的地方，该名称不能自定义，必须是src；-p意思是如果父目录不存在就同时创建父目录。
	```text
	cd ~/catkin_ws/src
	catkin_init_workspace
	```
	或者
	```text
	cd ~/catkin_ws
	wstool init src
	```
	使用下面的命令来编译工作空间：
	```text
	cd ~/catkin_ws
	catkin_make
	```
	3. 