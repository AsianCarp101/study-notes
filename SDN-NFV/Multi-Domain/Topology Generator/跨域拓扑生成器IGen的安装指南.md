##跨域拓扑生成器IGen的安装指南
[TOC]

###IGen介绍
参看 [IGen网页](http://informatique.umons.ac.be/networks/igen) 介绍

###IGen安装环境
- Perl
- 依赖模块包括
	1. Tk
	2. **Graph-0.20105**
	3. Statistics::Basic
	4. Number::Format
	5. Heap
说明：IGen开发比较久远，需要严格依赖Graph-0.20105，否则运行报错

###模块下载地址
Perl大多数模块可以直接到 [http://search.cpan.org](http://search.cpan.org)上下载，但是这个网站上面并不是都能下载到老版本。比如这次的Graph-0.20105版本的，就下载不到。
下载方式：直接在搜索框中搜索需要的module名就行

###安装方法（以Ubuntu系统为例）
- Perl安装
Ubuntu14.04自带Perl-5.18.2

- IGen安装
下载 igen-0.15.tar.gz，解压。执行
```cpp
cd igen
sudo ./INSTALL
```

- Tk安装
	1. 自动安装：Tk安装比较麻烦，在Ubuntu系统下使用比较简单，直接使用 `sudo apt-get install perl-tk`
	2. 手动安装：下载 `Tk-804.033.tar.gz`，解压然后执行：（我是Ubuntu下自动安装的，下面步骤是估计的）
	```cpp
	cd Tk-804.033
	perl MAKEFILE.PL
	make test
	sudo make install 或者 sudo ./INSTALL
	```
- Graph-0.20105安装
解压，然后执行：
```cpp
cd Graph-0.20105
perl MAKEFILE.PL
make test
sudo make install
```
说明：有的时候执行 `make test` 时并不是每次都能够得到 `make all ok` 这样的提示，不管，直接执行 `sudo make install`

- 其他模块安装
安装流程和Graph模块安装流程一致。

说明：在执行 `./igen-gui.pl` 时，提示缺什么模块，就到 CPAN上下载对应的模块，按照方面的方法安装即可