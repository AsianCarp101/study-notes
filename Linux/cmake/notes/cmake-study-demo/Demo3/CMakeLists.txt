# CMake 最低版本号要求
cmake_minimum_required(VERSION 2.8)

# 项目信息
project (Demo3)

# 查找当前目录下所有源文件，并将名称存放在 DIR_SRCS 变量中
aux_source_directory (. DIR_SRCS)

# 添加 math 子目录
add_subdirectory(math)

# 指定生成目标
add_executable(Demo main.cc)

# 添加链接库
target_link_libraries(Demo MathFunctions)
