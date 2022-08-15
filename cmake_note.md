```
Author:lgx
Date:2022.08.15 16:54:58
Email:geniuslgx@mail.ustc.edu.com
```

# 0. 各种关系

## 0.1 编译的4阶段

> 0. **编写**
>
>    > 用编辑器编写.c、.h、.cpp等文件
>
> 1. **预处理**
>
> >  - 处理所有预编译指令，如：#define、#include、#if、#elif、#else等
> >  - 删除所有注释
> >  - 生成.i文件
> >  - `gcc -E main.c -o main.i`
> 2. **编译**
>
> > - 高级语言（C/C++）----->中间代码（汇编语言）
> > - 扫码、语法分析、语义分析、源代码分析、目标代码生成、目标代码优化、符号汇总
> > - 生成.s文件
> > - `gcc -S main.i -o main.s`
>
> 3. **汇编**
>
> > - 中间代码（汇编语言）----->目标文件（二进制文件）
> >
> > - 根据汇编指令和特定平台，把汇编指令翻译成二进制形式
> > - 生成.o文件
> > - `gcc -c main.s -o main.o`
>
> 4. **链接**
>
>    > - 多个目标文件（二进制文件）结合库函数等。合成的能直接独立执行的执行文件
>    > - 输出.out(.exe)文件

## 0.1 gcc vs g++

> **GCC和gcc是不同的东西**
>
> **GCC**:GNU Compiler Collection(GUN 编译器集合)，它可以编译C、C++、Fortran、Pascal等语言
>
> **gcc**与**g++**都是是其中的一个子集，都是一个**编译器**
>
> ||gcc|g++|
> |:-:|:-:|:-:|
> |编译|.c后缀当作c程序|.c后缀文件当作cpp程序|
> |链接|不能自动和C++程序使用的库链接|自动和C++程序使用的库链接|

## 0.2 gcc(g++) vs make

> ||gcc|make|
> |:-:|:-:|:-:|
> |本质|编译器|命令工具|
> |用途|编译**1个**源文件|基于**makefile**，编译**多个**源文件|
> |关系|被调用|在makefile中调用gcc/g++|

## 0.3 make vs cmake

>|          |                       make                        |        cmake         |
>| :------: | :-----------------------------------------------: | :------------------: |
>| 产生原因 | 当存在多个源文件时，用gcc逐个编译，工作量大且复杂 | 编写makefile文件复杂 |
>|   输入   |                     makefile                      |    CMakeLists.txt    |
>|   输出   |                    可执行文件                     |       makefile       |
>
>一图胜千言：
>
>![cmake和make的区别](./images/cmake&make.jpg 'cmake和make的区别')
