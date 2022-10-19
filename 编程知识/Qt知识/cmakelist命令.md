> [!tip]  !!!注意，cmakelist.txt不区分大小写

## 命令
> [!tip] 命令介绍
> set 命令用来设置变量
>add_exectuable 告诉工程生成一个可执行文件。
>add_library 则告诉生成一个库文件。
>
```CMake
project(HELLO)
set(SRC_LIST main.c)
add_executable(hello ${SRC_LIST})
```
 第一行 **project** 不是强制性的，但最好始终都加上。这一行会引入两个变量
  - **HELLO_BINARY_DIR** 和 **HELLO_SOURCE_DIR**
同时，cmake自动定义了两个等价的变量
 - **PROJECT_BINARY_DIR** 和 **PROJECT_SOURCE_DIR**
***
> [!info] 可以通过**message**来输出变量的值
```cmake
message(${PROJECT_SOURCE_DIR})
```

### 个人构建过程
 - 在编写好cmakelist后在该目录下创建**build**文件夹
 - cd到该目录下执行`cmake .. -G"Unix Makefiles"`命令
 - 执行`make`命令

## 实现



## 参考
[cmake 学习笔记(一)_dbzhang800的博客-CSDN博客](https://blog.csdn.net/dbzhang800/article/details/6314073)
