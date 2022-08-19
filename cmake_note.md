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

## 0.4 动态库 vs 静态库

> |      |                  动态库                  |                    静态库                    |
> | :--: | :--------------------------------------: | :------------------------------------------: |
> | 后缀 |               .so 或 .dll                |                  .a 或 .lib                  |
> | 优点 | 目标程序较小，且可以动态更换指定的依赖库 | 直接整合到目标程序中，目标程序可**独立运行** |
> | 缺点 |           目标程序不可独立执行           |    目标程序较大，且升级时需要**重新编译**    |

# 1. g++(gcc)编译器

## 1.1 安装

> ``` bash
> apt install g++ gcc
> ```

## 1.2 基本流程

> - `g++ main.cpp -o main.out` 等价于以下命令
>   - 预处理生成.i文件（消去注释等）：`g++ -E main.cpp -o main.i`
>   - 编译生成.s文件（汇编语言）：`g++ -S main.i -o main.s`
>   - 汇编生气.o文件（二进制）`g++ -c main.s -o main.o`
>   - 链接生成.out文件（可执行文件）`g++ main.o -o main.out`

## 1.3 重要参数

>- **-g 编译带调试信息的可执行文件**
>
>  > -g选项告诉g++产生能被GNU调试器gdb使用的调试信息，以调试程序
>  >
>  > 如：`g++ -g main.cpp -o main`
>
>- **-O[n] 优化源代码**
>
>  > 优化：例如省略掉源代码中未使用过的变量、常量表达式直接用其结果表示等，会缩减代码量，从而提高运行效率
>  >
>  > O0：不优化
>  >
>  > O1：默认优化
>  >
>  > O2：完成O1优化外，还完成指令调整等。
>  >
>  > O3：包括循环展开和一些与处理特性相关的优化工作
>  >
>  > 优化等级越高，编译越慢，编译得到的可执行程序效率越高，通常使用**O2**优化
>  >
>  > 如：`g++ -O2 main.cpp -o main`
>
>- **-l 与 -L 指定库文件和指定库目录**
>
>  > -l （L的小写）指定库名
>  >
>  > 如：`g++ -l glob main.cpp` 在系统库目录中找**libglob.a**或者**libglob.so**
>  >
>  > 若系统默认的库目录中（/lib、/usr/lib和/usr/local/lib）没有指定的库文件，则需要-L来指定其库目录
>  >
>  > 如：`g++ -L /home/mylibfolder/ -l mylib main.cpp -o main	 `
>
>- **-I 指定头文件搜索目录**
>
>  > 若头文件在`/usr/include/`下，则不用指定；若不在，则需要用-I（i的大写）来指定
>  >
>  > 如：`g++ -I/myinclude main.cpp`
>
>- **-Wall -w 警告信息**
>
>  > -Wall 打印警告信息 如：`g++ -Wall main.cpp`
>  >
>  > -w关闭警告信息 如：`g++ -w main.cpp`，默认是关闭的
>
>- **-std 编译标准**
>
>  > 设置编译标准，默认标准试编译器（g++版本）而定
>  >
>  > 如：`g++ -std=c++11 main.cpp`
>
>- **-D 激活宏**
>
>  > 编译后，激活指定宏名
>  >
>  > 如：有main.cpp如下
>  >
>  > ```c++
>  > #include<iostream>
>  > int main(){
>  > 	#ifdef DEBUG
>  > 		std::cout<<"debug"<<std::endl;
>  > 	#endif
>  > 	return 0;
>  > }
>  > ```
>  >
>  > `g++ -DDEBUG main.cpp -o main`后执行`./main`会输出，debug
>  >
>  > 而`g++  main.cpp -o main`后执行./main，不会输出debug

## 1.4 静态库编译

>文件结构如下：
>
>```bash
>.
>├── include
>│   └── swap.h
>├── main.cpp
>└── src
>    └── swap.cpp
>```
>
>- **step1 汇编生成swap.o**
>
>  ```bash
>  cd src
>  g++ swap.cpp -c -I ../include
>  ```
>
>- **step2 生成静态库.a文件**
>
>  ```bash
>  ar rs libswap.a swap.o
>  ```
>
>  > r：将文件插入备存文件中。
>  >
>  > s：若备存文件中包含了对象模式，可利用此参数建立备存文件的符号表。
>  >
>  > [Linux ar命令](https://www.runoob.com/linux/linux-comm-ar.html)
>
>- **step3 链接生成可执行文件**
>
>  ```bash
>  cd ..
>  g++ main.cpp -l swap -L src/ -I include/ -o static_main
>  ```
>
>  注意，-l会**先搜索libxxxx.so文件**，若libxxxx.so不存在，才会搜索libxxxx.a文件。即若动态库存在，则最终编译生成的可执行文件依赖于动态库，否则才生成依赖于静态库的可执行文件。



## 1.5 动态库编译

>文件结构同静态库编译
>
>- **step1  生成动态库**
>
>> ```bash
>> cd src
>> g++ swap.cpp -I ../include/ -fPIC -shared -o libswap.so
>> ```
>>
>> -fPIC：表示与路径无关
>>>
>> -shared：表示生成动态库
>
>- **step2  编译**
>
>> ```bash
>> cd ..
>> g++ main.cpp -l swap -L src/ -I include/ -o dynamic_main
>> ```
>
>- **step3 指定动态库目录**
>
> >永久指定
> >
> >```bash
> >echo export LD_LIBRARY_PATH=/home/tmo/swap_demo/src:$LD_LIBRARY_PATH >> ~/.basrc
> >source ~/.bashrc
> >```
>
> > 临时指定
> >
> > ```bash
> > LD_LIBRARY_PATH=/home/tmo/swap_demo/src
> > ```

# 2. gdb调试器

> 只有带**-g**选项编译的可执行文件，才能用gdb调试
>
> 如：`g++ -g main.cpp -o m1`生成的m1可以调试，`g++ main.cpp -o m2`生成的m2不能调试

## 2.1  常用参数

> 以下命令括号内为简化使用，比如run(r)，直接输入r代表run
>
> - **启动gdb**
>
>   > ``` bash
>   > gdb [execfilename]
>   > # 或者进入gdb后，用file 或者 exec-file 指定
>   > gdb
>   > (gdb) file execfilename
>   > ```
>
> - **help(h)**
>
>   > 查看命令帮助，如：查看run的帮助
>   >
>   > ```bash
>   > (gdb) help r
>   > ```
>
> - **run(r)**
>
>   > 执行指定的execfilename，一次性执行完
>
> - **start**
>
>   > **单步执行**，停在第一条执行语句
>
> - **list(l)**
>
>   > 显示指定行，或指定函数周围的代码，如：显示第8行周围的代码、显示main函数周围的代码
>   >
>   > ```bash
>   > (gdb) l 8
>   > (gdb) l main
>   > ```
>   
> - **set **
>
>   > 设置变量的值，变量在当前环境下应该有定义。如：将变量sum设置为-1
>   >
>   > ```bash
>   > (gdb) set sum=-1;
>   > ```
>
> - **next(n)**
>
>   > 单步调试，**逐过程**，遇到函数**直接执行返回结果**
>
> - **step(s)**
>
>   > 单步调试，**逐语句**，遇到函数**跳入函数内部**
>
> - **backtrace(bt)**
>
>   > 显示当前的函数调用栈
>
> - **print(p)**
>
>   > 打印变量的值，及其地址，只打印一次。如：打印变量i的值及其地址
>   >
>   > ```bash
>   > (gdb) p i
>   > ```
>
> - **quit(q)**
>
>   > 退出gdb
>

## 2.2  断点

>- **break num**
>
>  > 在第num行设置断点，如：在第11行设置断点
>  >
>  > ``` bash
>  > (gdb) break 11
>  > ```
>
>- **info breakpoints**
>
>  > 查看当前已有的断点
>
>- **delete breakpoints num**
>
>  > 删除第num个断定，num为info breakpoints中显示的
>
>- **disable breakpoints  /  enable breakpoints**
>
>  > 禁用所有断点  /  启用所有断点
>
>- **continue(c)**
>
>  > 运行到下一个断点处
>
>- **display**
>
>  > 持续打印变量的值。
>  >
>  > ```bash
>  > (gdb) display i  # 持续打印变量i的值
>  > (gdb) i display  # 查看当被display的信息
>  > (gdb) undisplay num  # 删除第num个display点，或者用(gdb)delete display num 删除
>  > ```
>
>- **watch**
>
>  > 当变量发生变化时，打印其的old值与new值
>  >
>  > ```bash
>  > (gdb) watch sum  # 当sum的值变化时，打印其变化
>  > (gdb) i watch  # 查看当前watchpoints信息
>  > (gdb) delete num  # 删除第num个watchpoint
>  > ```

# 3. cmake

> CMake是一个跨平台的安装编译工具，可以用简单的语句来描述所有平台的安装(编译过程)。他能够输出各种各样的makefile或者project文件、

## 3.1 基本语法

> 格式：`指令(参数1 参数2 ...)` 或者指令(参数1;参数2 ...)
>
> 指令是大小写无关的，例如：`add_executable()`与`ADD_EXECUTABLE()`是相同的
>
> 参数和变量是大小写相关的，例如：`HELLO`与`hello`是不同的
>
> 变量使用`${变量名}`来取值，但是在if(IF)语句中**直接用变量名**

## 3.2 重要指令

> - **cmake_minimum_required**
>
>   >指定cmake的最小版本
>   >
>   >```cmake
>   ># 语法：
>   >cmake_minimum_required(VERSION version_number [FATAL_ERROR])
>   ># 如：要求Cmake的最小版本为3.0
>   >cmake_minimum_required(VERSION 3.0)
>   >```
>
> - **project**
>
> > 定义工程名称，并指定工程支持语言
> >
> > ```cmake
> > # 语法：
> > project(projectname [CXX] [C] [JAVA])
> > # 如：指定工程名称为hello，指定语言为c++
> > project(hello CXX)
> > ```
>
> - **set**
>
> > 显示设置变量
> >
> > ```cmake
> > # 语法：
> > set(<variable> <value>... [PARENT_SCOPE])
> > # 如：设置PADDLE_LIB_THIRD_PARTY_PATH的值为${PADDLE_LIB}/third_party/install/
> > set(PADDLE_LIB_THIRD_PARTY_PATH "${PADDLE_LIB}/third_party/install/")
> > ```
>
> - **include_directories**
>
>   > 向工程添加**多个**头文件搜索路径
>   >
>   > ```cmake
>   > # 语法：
>   > include_directories([AFTER][BEFORE][SYSTEM] dir1 dir2...)
>   > # 如：项工程中加入./include和/usr/local/myinclude头文件搜索目录
>   > include_directories(./include /usr/local/myinclude)
>   > ```
>
> - **link_directories**
>
>   > 向工程添加**多个**库文件搜索路径
>   >
>   > ```cmake
>   > # 语法：
>   > link_directories(dir1 dir2...)
>   > # 如：项工程中加入./lib和/usr/local/lib头文件搜索目录
>   > link_directories(./lib /usr/local/lib)
>   > ```
>
> - **add_library**
>
>   > 生成库文件 
>   >
>   > ```cmake
>   > # 语法：
>   > add_library(libname [SHARED | STATIC] src1 src2)
>   > # 如：通过SRC变量生成libswap.so 动态库
>   > add_library(swap SHARED ${SRC})
>   > ```
>
> - **add_compile_options**
>
>   >添加编译参数，即g++（gcc）编译器的参数
>   >
>   >```cmake
>   ># 语法：
>   >add_compile_options(<option> ...)
>   ># 如：设置c++11编译标准、输出警告信息、代码优化
>   >add_compile_options(-Wall -O2 -std=c++11)
>   >```
>
> - **add_executable**
>
>   > 生成可执行文件
>   >
>   > ```cmake
>   > # 语法：
>   > add_executable(execname src1 src2 ...)
>   > # 如：编译main.cpp生成可执行文件main
>   > add_executable(main main.cpp)
>   > ```
>
> - **target_link_libraries**
>
> > 为target添加需要的动态库
> >
> > ```cmake
> > # 语法：
> > target_link_libraries(target lib1 lib2)
> > # 如：将libswap.so动态库文件，链接到可执行文件main
> > target_link_libraries(main swap)
> > ```
>
> - **add_subdirectory**
>
> > 向当前工程添加存放源文件的子目录，该子目录中**必须要有个CMakeLists.txt文件**	
> >
> > ```cmake
> > # 语法：
> > add_subdirectory(src_dir [binary_dir] [EXCLUDE_FROM_ALL])
> > # 如：添加src子目录
> > add_subdirectory(src)
> > ```
> >
> > 
>
> - 2
> - 2
> - 2
> - 2

