```
Author：lgx
Date：2022.08.22 10:03:36
Email:geniuslgx@mail.ustc.edu.cn
```

**chrono**是C++的一个头文件名，有着自己的子命名空间，除了一些特殊的元素，chrono头文件下的元素不是直接定义在std命名空间下，而是定义在**std::chrono**命名空间下。

# 1. duration

> 可以简单的理解成：**1个数值和1个单位**

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
> //构造days，用1个double类型的值来表示天数，单位为std::ratio<24 * 60 * 60, 1>，以秒为基准
> typedef std::chrono::duration<double, std::ratio<24 * 60 * 60, 1>> days;
> // d1表示1天，d2表示2.5天
> days d1(1);
> days d2(2.5);
> cout<<"d2 are "<<d2.count()<<" days"<<endl; //通过成员函数count()来得到当前对象的Rep的值
> /*
>     输出结果：
>     d2 are 2.5 days
> */
> ```
>
>  每个duration类都有3个**静态成员函数**：**max()*、*min()*、*zero()**，分别返回该类中的Rep的类型所能表达的最大值、最小值、0值的**duration对象**，单位与该类的Period相同。
>
> ```c++
> typedef std::chrono::duration<double, std::ratio<24 * 60 * 60, 1>> days;
> days max_ = days::max();
> cout <<"max_.count()= "<< max_.count() << endl; 
> days min_ = days::min();
> cout << "min_.count()= " << min_.count() << endl;
> days zero_ = days::zero();
> cout << "zero_.count()= " << zero_.count() << endl;
> /*
> 输出结果：
>     max_.count()= 1.79769e+308
>     min_.count()= -1.79769e+308
>     zero_.count()= 0
> */
> ```



## 1.2 已定义类型

>在**std::chrono**命名空间下
>
>| type         | Representation                             | Period                |
>| :----------- | :----------------------------------------- | :-------------------- |
>| hours        | *signed integral type* of at least 23 bits | `ratio<3600,1>`       |
>| minutes      | *signed integral type* of at least 29 bits | `ratio<60,1>`         |
>| seconds      | *signed integral type* of at least 35 bits | `ratio<1,1>`          |
>| milliseconds | *signed integral type* of at least 45 bits | `ratio<1,1000>`       |
>| microseconds | *signed integral type* of at least 55 bits | `ratio<1,1000000>`    |
>| nanoseconds  | *signed integral type* of at least 64 bits | `ratio<1,1000000000>` |

## 1.3  操作

>同类型的duration对象，可以直接加减，或者使用**obj1+=obj2**、**obj1-=obj2**、或者**自增、自减**。
>
>duration对象可以直接乘除自己的Rep对应类型的变量。
>
>```c++
>typedef std::chrono::duration<double, std::ratio<24 * 60 * 60, 1>> days;
>days d1(1.0);
>days d2(2.5);
>days d3 = d1 / 2.;  //d3的Rep的类型为double，可以直接除以2.
>cout << "(d1 + d2).count()= " << (d1 + d2).count() << endl; //同类型的duration对象直接相加
>cout << "d3.count()= " << d3.count() << endl;
>/*
>输出结果：
>	(d1 + d2).count()= 3.5
>	d3.count()= 0.5
>*/
>```
>
>不同类型的duration对象，若可以**自动隐式转换**，也可以直接相加减
>
>````c++
>typedef std::chrono::duration<double, std::ratio<24 * 60 * 60, 1>> days;
>typedef std::chrono::duration<double, std::ratio<30*24 * 60 * 60, 1>> months;
>// 定义1个月对象、2个月对象
>months m1(1),m2(2);
>//定义25天对象，15天对象
>days d25(25),d15(15);
>m1 += d25;
>d15 += m2;
>cout << "1 month plus 25 days= " << m1.count() << " months" << endl;
>cout << "15 days plus 2 months= " << d15.count() << " days" << endl;
>/*
>输出结果：
>	1 month plus 25 days= 1.83333 months
>	15 days plus 2 months= 75 days
>*/
>````
>
>若不能自动隐式转换，则需用通过**duration_cast<目标类型>(要转换的变量)**来显示转化，可能会有**精度损失**
>
>````c++
>std::chrono::hours h1(1); // 定义1小时对象
>std::chrono::minutes min45(45); // 定义45分钟对象
>// 已定义类型中，小单位加大单位一般不会报错，如分钟加小时
>min45 += h1;
>cout << "45 minutes plus 1 hour= " << min45.count() << " minutes" << endl;
>// h1 += min45; //不能自动隐式转换，会报错
>min45 = minutes(45);
>// std::chrono::hours的Rep类型为整型，无法表示小数，min45转换过去被截断为0，产生精度损失
>h1 += std::chrono::duration_cast<std::chrono::hours>(min45); 
>cout << "1 hour plus 45 minutes= " << h1.count() << " hours" << endl;
>/*
>输出结果：
>	45 minutes plus 1 hour= 105 minutes
>	1 hour plus 45 minutes= 1 hours
>*/
>````

# 2. Time points

# 3. Clocks

