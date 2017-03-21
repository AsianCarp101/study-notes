# 查找当前目录下所有源文件， 并将名称保存到 DIR_LIB_SRCS变量中
aux_source_directory (. DIR_LIB_SRCS)

# 生成链接库
add_library (MathFunctions ${DIR_LIB_SRCS})
