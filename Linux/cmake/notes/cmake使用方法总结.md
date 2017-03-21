#cmake使用方法总结
>参考这篇文章：http://www.hahack.com/codes/cmake/
>另一篇CMake实战教程
http://www.cnblogs.com/ph829/p/4759124.html

[TOC]
### 使用大体流程
```text
1. 编写代码文件
2. 在统一目录下，编写CMakeLists.txt文件，不同情况下编写类型可能不一样，具体参考下面介绍
3. 执行 命令 "cmake ."， 注意有个 "."
4. 执行命令 "make"
```

### 不同情况下CMakeLists.txt文件编写方法
#### 单个源文件
```text
# CMake 最低版本号要求
cmake_minimum_required (VERSION 2.8)
# 项目信息
project (Demo1)
# 指定生成目标
add_executable(Demo main.cc)
```
CMakeLists.txt 的语法比较简单，由命令、注释和空格组成，其中命令是不区分大小写的。符号 # 后面的内容被认为是注释。命令由命令名称、小括号和参数组成，参数之间使用空格进行间隔。
对于上面的 CMakeLists.txt 文件，依次出现了几个命令：
- cmake_minimum_required：指定运行此配置文件所需的 CMake 的最低版本；
- project：参数值是 Demo1，该命令表示项目的名称是 Demo1 。
- add_executable： 将名为 main.cc 的源文件编译成一个名称为 Demo 的可执行文件。

#### 多个源文件
- 方法一
```text
# CMake 最低版本号要求
cmake_minimum_required (VERSION 2.8)
# 项目信息
project (Demo2)
# 指定生成目标
add_executable(Demo main.cc MathFunctions.cc)
```
- 方法二（使用函数 `aux_source_directory(<dir> <variable>)`）
```text
# CMake 最低版本号要求
cmake_minimum_required (VERSION 2.8)
# 项目信息
project (Demo2)
# 查找当前目录下的所有源文件
# 并将名称保存到 DIR_SRCS 变量
aux_source_directory(. DIR_SRCS)
# 指定生成目标
add_executable(Demo ${DIR_SRCS})
````

#### 多个目录，多个源文件
- 目录结构
```text
./Demo3
    |
    +--- main.cc
    |
    +--- math/
          |
          +--- MathFunctions.cc
          |
          +--- MathFunctions.h
```

- 根目录中的 `CMakeLists.txt` 文件
```text
# CMake 最低版本号要求
cmake_minimum_required (VERSION 2.8)
# 项目信息
project (Demo3)
# 查找当前目录下的所有源文件
# 并将名称保存到 DIR_SRCS 变量
aux_source_directory(. DIR_SRCS)
# 添加 math 子目录
add_subdirectory(math)
# 指定生成目标
add_executable(Demo main.cc)
# 添加链接库
target_link_libraries(Demo MathFunctions)
```

- 子目录中的 `CMakeLists.txt` 文件
```text
# 查找当前目录下的所有源文件
# 并将名称保存到 DIR_LIB_SRCS 变量
aux_source_directory(. DIR_LIB_SRCS)
# 生成链接库
add_library (MathFunctions ${DIR_LIB_SRCS})
```

#### 自定义编译选项
