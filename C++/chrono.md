```
Author：lgx
Date：2022.08.22 10:03:36
Email:geniuslgx@mail.ustc.edu.cn
```

**chrono**是C++的一个头文件名，有着自己的子命名空间，除了一些特殊的元素，chrono头文件下的元素不是直接定义在std命名空间下，而是定义在**std::chrono**命名空间下。





# 1. Duration

> 用来衡量时间跨度，如1分钟，2小时，10毫秒等
>
> Duration通过类模板来构造，类模板中包括**count representation(Rep)** 和 **period precision(Period)**
>
> 比如：10毫秒的Rep为10(int类型)，Period为**milli([ratio](./ratio.md)<1,1000>) **

# 2. Time points

# 3. Clocks

