```
Author：lgx
Date：2022.08.22 10:23:52
Email:geniuslgx@mail.ustc.edu.cn
```

#include<ratio>

# 1. 构造使用

> ```c++
> template <intmax_t Numerator, intmax_t Denominator = 1> class ratio;
> ```
>
> 该模板用 **分子(numerator)** 和 **分母(denominator)**来表示一个分数，分子和分母都是**整型(intmax_t)**，他们的绝对值应该都在intmax_t可表示的范围内。
>
> ```c++
> // std::ratio<1,3> my_one_third 等价于以下：
> typedef std::ratio<1,3> one_third;
> one_third my_one_third;
> // std::ratio<1,4> my_one_fourth 等价于以下：
> typedef std::ratio<1,4> one_fourth;
> one_fourth my_one_fourth;
> ```
>
> 成员变量：**num**和**den**，都是**公有**的，可以直接调用
>
> ```c++
> std::ratio<1,4> my_one_fourth
> // 通过调用num和den成员来获得分子分母
> std::cout<<my_one_fourth.num<<"/"<<my_one_fourth.den<<endl;
> ```
>
> ratio不是该类型的一个对象，而是类型本身，在编译的时候使用**常量成员**(Numerator和Denominator是常数)来定义ratio。因此，ratio只能用来表示**constexpr常量**，而**不能表示变量**。
>
> 该模板常用于构造[**duration**](./chrono.md/#duration)
# 2. 已定义实例

>|  type   | definition                           | description |
>| :-----: | :----------------------------------- | :---------- |
>| `yocto` | `ratio<1,1000000000000000000000000>` | $10^{-24}$  |
>| `zepto` | `ratio<1,1000000000000000000000>`    | $10^{-21}$  |
>| `atto`  | `ratio<1,1000000000000000000>`       | $10^{-18}$  |
>| `femto` | `ratio<1,1000000000000000>`          | $10^{-15}$  |
>| `pico`  | `ratio<1,1000000000000>`             | $10^{-12}$  |
>| `nano`  | `ratio<1,1000000000>`                | $10^{-9}$   |
>| `micro` | `ratio<1,1000000>`                   | $10^{-6}$   |
>| `milli` | `ratio<1,1000>`                      | $10^{-3}$   |
>| `centi` | `ratio<1,100>`                       | $10^{-2}$   |
>| `deci`  | `ratio<1,10>`                        | $10^{-1}$   |
>| `deca`  | `ratio<10,1>`                        | $10^{1}$    |
>| `hecto` | `ratio<100,1>`                       | $10^{2}$    |
>| `kilo`  | `ratio<1000,1>`                      | $10^{3}$    |
>| `mega`  | `ratio<1000000,1>`                   | $10^{6}$    |
>| `giga`  | `ratio<1000000000,1>`                | $10^{9}$    |
>| `tera`  | `ratio<1000000000000,1>`             | $10^{12}$   |
>| `peta`  | `ratio<1000000000000000,1>`          | $10^{15}$   |
>|  `exa`  | `ratio<1000000000000000000,1>`       | $10^{18}$   |
>| `zetta` | `ratio<1000000000000000000000,1>`    | $10^{21}$   |
>| `yotta` | `ratio<1000000000000000000000000,1>` | $10^{24}$   |

# 3. 操作

> 算数操作和逻辑操作

## 3.1 算数操作

>**ratio_add**、**ratio_substract**、 **ratio_divide** 、**ratio_multiply**，都在**std**命名空间下。
>
>例：
>
>```c++
>typedef std::ratio<1,3> one_third;
>typedef std::ratio<1,4> one_fourth;
>typedef std::ratio_add<one_third,one_fourth>sum;
>std::cout << "sum = " << sum::num << "/" << sum::den;
>std::cout << " (which is: " << ( double(sum::num) / sum::den ) << ")" << std::endl;
>```
>
>输出：
>
>```bash
>sum = 7/12 (which is: 0.583333)
>```

## 3.2逻辑操作

> **ratio_equal**、**ratio_greater**、**ratio_greater_equal**、**ratio_less**、**ratio_less_equal**、**ratio_not_equal**，都在都在**std**命名空间下。
>
> 例：
>
> ```c++
> typedef std::ratio<1,3> one_third;
> typedef std::ratio<1,4> one_fourth;
> typedef std::ratio_equal<one_third,one_fourth>equal;
> std::cout << "1/3 == 1/4 ? " << std::boolalpha;  // 空出输出为bool类型而不是int
> // 调用公有成员value获得其值
> std::cout << equal::value << std::endl;
> ```
>
> 输出：
>
> ```bash
> 1/3 == 1/4 ? false
> ```
