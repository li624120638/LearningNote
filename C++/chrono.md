```
Author：lgx
Date：2022.08.22 10:03:36
Email:geniuslgx@mail.ustc.edu.cn
```

**chrono**是C++的一个头文件名，有着自己的子命名空间，除了一些特殊的元素，chrono头文件下的元素不是直接定义在std命名空间下，而是定义在**std::chrono**命名空间下。





# 1. Duration

## 1.1 构造使用

> ```c++
> template <class Rep, class Period = ratio<1> > class duration;
> ```
>
> 用来表示时间跨度，如1分钟，2小时，10毫秒等
>
> Duration通过类模板来构造，类模板中包括**count representation(Rep)** 和 **period precision(Period)**
>
> 比如：10毫秒的Rep为10(int类型)，Period为**milli([ratio](./ratio.md)<1,1000>) **
>
> ```c++
> //构造days，用1个double类型的值来表示天数，单位为std::ratio<24 * 60 * 60, 1>
> typedef std::chrono::duration<double, std::ratio<24 * 60 * 60, 1>> days;
> typedef std::chrono::duration<double, std::ratio<30*24 * 60 * 60, 1>> months;
> typedef std::chrono::duration<double, std::ratio<365*30 * 24 * 60 * 60, 1>> years;
> ```



## 1.2 已定义实例

>| type         | Representation                             | Period                |
>| :----------- | :----------------------------------------- | :-------------------- |
>| hours        | *signed integral type* of at least 23 bits | `ratio<3600,1>`       |
>| minutes      | *signed integral type* of at least 29 bits | `ratio<60,1>`         |
>| seconds      | *signed integral type* of at least 35 bits | `ratio<1,1>`          |
>| milliseconds | *signed integral type* of at least 45 bits | `ratio<1,1000>`       |
>| microseconds | *signed integral type* of at least 55 bits | `ratio<1,1000000>`    |
>| nanoseconds  | *signed integral type* of at least 64 bits | `ratio<1,1000000000>` |

## 1.3 

# 2. Time points

# 3. Clocks

