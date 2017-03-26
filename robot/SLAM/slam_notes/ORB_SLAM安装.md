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
终端输入：roscore
新打开终端，执行：roslaunch ExampleGroovyOrNewer.launch
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
	下面是最后一步：
	```text
	cd ~/catkin_ws
	source devel/setup.bash
	```
	现在我们就创建好了一个工作空间。
tips:因为运行工作空间中的ROS节点要频繁使用 `source devel/setup.bash` ，因此笔者建议将该命令加到 `.bashrc` 中： 执行命令：
```text
echo "source ~/catkin_ws/devel/setup.sh" >> ~/.bashrc
```
NOTE: catkin_ws是你的工作空间名字。
	3. 此时上述问题解决，再次执行
	```text
终端输入：roscore
新打开终端，执行：roslaunch ExampleGroovyOrNewer.launch
```

##### 上述过程完成后，遇到新的问题 `ERROR: cannot launch node of type [ORB_SLAM/ORB_SLAM]: can't locate node [ORB_SLAM] in package [ORB_SLAM]`
- 问题描述
执行下述命令后
```text
终端输入：roscore
新打开终端，执行：roslaunch ExampleGroovyOrNewer.launch
```
能够成功打开测试数据界面，但是命令行提示错误：
```text
ERROR: cannot launch node of type [ORB_SLAM/ORB_SLAM]: can't locate node [ORB_SLAM] in package [ORB_SLAM]
```

- 解决办法
出现这样的原因，一般都是因为设置的 “路径” 不对。这个 "路径" 包括：ROS的工作空间、ORB_SLAM的路径是否已经添加到ROS_PACKAGE_PATH里面去。 ** 具体体现在下面三个方面:**

   1. ROS系统的启动
   每次启动ROS系统时，执行 `roscore`。但是执行之前需要指出ROS系统的 `setup.bash`文件的位置，具体有两种方法可以解决：(以在Ubuntu14.04上安装indigo系统为例)
   ```text
   1、 在执行 roscore之前 执行 source /opt/ros/indigo/setup.bash
   但是这样做太麻烦，每次执行roscore的时候都需要运行这一句，所以可以找个一劳永逸的办法:
   2、在 ~/.bashrc 文件中，添加 "source /opt/ros/indigo/setup.bash"(引号里面的内容)，这样，每次启动终端，都自动帮我们执行上面那一句
   ```
   
   2. ROS系统自定义工作空间的启动
   关于如何自定义ROS系统的工作空间，可以参考官方文档，或者参考这篇中文博客 http://blog.csdn.net/github_30605157/article/details/52209434
   ```text
   启动自定义的工作空间，有两种方法。
   每次执行 `roscore` 都执行 `source ~/catkin_ws/devel/setup.sh`， 或者一劳永逸地解决，将这一句添加到 ～/.bashrc文件中
   ```
   3. 将ORB_SLAM程序的路径加入到ROS_PACKAGE_PATH中
   每次执行 `rosrun ... ` 之前，需要先执行 ` export ROS_PACKAGE_PATH=$ROS_PACKAGE_PATH:(你的ORB_SLAM文件夹绝对路径)`，以我为例：`export ROS_PACKAGE_PATH=${ROS_PACKAGE_PATH}:/home/liyayu/catkin_ws/src/ORB_SLAM`， 或者一劳永逸的将这句命令，添加到 ～/.bashrc中
   
   总之，经过上面个的步骤，～/.bashrc中应该有这样三句：
   ```text
1、source /opt/ros/indigo/setup.bash
export
2、ROS_PACKAGE_PATH=${ROS_PACKAGE_PATH}:/home/liyayu/catkin_ws/src/ORB_SLAM
3、source ~/catkin_ws/devel/setup.sh
   ```
但是，**问题来了**。当我按照上面的步骤完成时，执行
```text
终端输入：roscore
新打开终端，执行：roslaunch ExampleGroovyOrNewer.launch
```
却遇到当前这个问题。苦思良久，发现是犯了一个愚蠢的错误。** 从github上 git clone到ORB_SLAM程序，对程序进行第三方库和ORB_SLAM的编译，但是，在编译后我将ORB_SLAM却拷贝到其他的目录下，虽然更改了～/.bashrc中的 $ROS_PACKAGE_PATH，但是，却却是使用了之前编辑的ORB_SLAM，这才导致了这一错误。解决办法就是，重新编译ORB_SLAM即可**