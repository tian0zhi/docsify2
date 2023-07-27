# C语言

## 一、从C语言->机器语言（编译&链接）

<p align="center">
        <img src="/Code/C/pic/fig2.png" width="120%"/>
</p>
<p align="center">C程序具体过程</p>

1.预编译:

删除注释；

宏替换；

预编译指令:#include #if #elif #endif；

2.编译:

词法,语法,语义的解析；

代码优化；

符号汇总(数据和函数名会生成符号)

3.汇编:

将汇编指令转化为二进制；

生成各个section；

生成符号表

4.链接:

合并各个section，调整段大小及段的起始位置，合并符号表，进行符号解析。


<p align="center">
        <img src="/Code/C/pic/fig1.png" width="120%"/>
</p>
<p align="center">编译与链接简化</p>

**c语言到机器可理解语言的过程简单可分为两步：**

 1. 编译 
 
	 编译器(gcc)将用户写好的.c文件编译（预编译、编译、汇编）成汇编指令文件.o。

 2. 链接

	 连接器ld将汇编指令文件.o与工程依赖的第三方库——静态库.a、动态库.so链接到一起，最终才生成可执行程序。

## 二、编译&链接工具——gcc、make、cmake

<p align="center">
        <img src="/Code/C/pic/fig3.png" width="120%"/>
</p>
<p align="center">一个简单的c工程</p>

<!-- tabs:start -->

#### **exec_start.c**

```c
#include <stdio.h>
#include "liba/a.h"
#include "libb/b.h"

// extern int a_veriable;

int main()
{
	printf("a_variable:%d\n",a_variable);
	printf("b_variable:%d\n",b_variable);
}
```

#### **liba/a.h**

```c
//a.h
#ifndef A_H
#define A_H

#ifdef __cplusplus
extern "C" {
#endif

extern int a_variable;

#ifdef __cplusplus
}
#endif

#endif /* HEAd_H */
```

#### **liba/a.c**

```c
#include "a.h"

int a_variable = 10;

```

#### **libb/b.h**

```c
//b.h
#ifndef B_H
#define B_H

#ifdef __cplusplus
extern "C" {
#endif

extern int b_variable;

#ifdef __cplusplus
}
#endif

#endif /* HEAd_H */
```

#### **libb/b.c**

```c
#include "b.h"

int b_variable = 100;
```

<!-- tabs:end -->

<p align="center">
        <img src="/Code/C/pic/fig4.png" width="120%"/>
</p>
<p align="center">这个简单的c工程生成可执行程序的过程</p>

为了避免每次都输入许多命令，Makefile(make)出现了。

#### ** Makefile  **

```makefile
# 定义编译器
CC = gcc
# 定义编译器标志，包括警告和调试信息
CFLAGS = -Wall -Wextra -g
# 源代码目录
SRCDIR = .
# 第一个库的源代码目录
LIBADIR = liba
# 第二个库的源代码目录
LIBBDIR = libb

# 默认目标，生成可执行文件mainexc
all: mainexc

# 生成可执行文件mainexc，依赖于a.o、b.o和main.o目标
mainexc: a.o b.o main.o
	$(CC) $(CFLAGS) a.o b.o main.o -o mainexc

# 生成a.o目标，将liba目录下的a.c编译成目标文件
a.o: $(LIBADIR)/a.c
	$(CC) $(CFLAGS) -c $< -o $@

# 生成b.o目标，将libb目录下的b.c编译成目标文件
b.o: $(LIBBDIR)/b.c
	$(CC) $(CFLAGS) -c $< -o $@

# 生成main.o目标，将src目录下的exec_start.c编译成目标文件
main.o: $(SRCDIR)/exec_start.c
	$(CC) $(CFLAGS) -c $< -o $@

# 清理生成的目标文件和可执行文件mainexc
clean:
	rm -f *.o mainexc

```
<p align="center">
        <img src="/Code/C/pic/fig5.png" width="120%"/>
</p>
<p align="center">一行命令解决</p>


进一步简化编译流程，cmake出现了。



#### ** CMakeLists.txt  **

```c
cmake_minimum_required(VERSION 3.10)

# 设置项目名称
project(c_demo)

# 添加可执行文件
add_executable(mainexc 
    exec_start.c 
    liba/a.c 
    libb/b.c
)

# 添加头文件搜索路径
include_directories(liba libb)

```

<p align="center">
        <img src="/Code/C/pic/fig5.png" width="120%"/>
</p>
<p align="center">一行命令解决</p>

### 欢迎使用Markdown

##### 新增图片上传功能

现在可以在文章中插入图片！

- 您可以插入外链图片，或上传本地图片到文档中。
- 可上传的单张图片最大20M，支持PNG、JPG格式。
- 若有其他疑问，欢迎咨询官网在线客服。

 

### Welcome to the Markdown

##### New feature! Insert pictures in your articles now!

You can insert pictures from external links, or upload ones.

The maximum size of the picture to upload is 20M. PNG and JPG are better.

Have any other questions, please contact our official customer service.
