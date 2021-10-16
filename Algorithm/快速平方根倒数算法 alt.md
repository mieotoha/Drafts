(开场白：继承史诗，创造神话。大家好我是未絵音羽，当然也可以叫我洛诗旅)

今天我们来讲一下这段被载入史册的魔法(代码)——快速平方根倒数算法

> 事先说明：
> - 启发我写出这篇文章的是[这个视频](https://www.bilibili.com/video/BV1v64y1i7KH)
> - 这是32位时代的算法，请以32位为前提来读本篇所有的魔法(代码)
> - 要看懂这篇文章，你可能需要先掌握二进制的知识和高数的知识

先让我们看看这段魔法(代码)

```c
float q_rsqrt(float number){
long i;
float x2, y;
const float threehalfs = 1.5F;

x2 = number * 0.5F;
y = number;
i = * (long * ) &y;                      // evil floating point bit level hacking
i = 0x5f3759df - (i >> 1);               // what the fuck?
y = * (float * ) &i;
y = y * (threehalfs - (x2 * y * y));     // 1st iteration
// y = y * ( threehalfs - ( x2 * y * y ) ); // 2nd iteration, this can be removed
}
```

那么问题来了
- <del>WTF?</del>
- 为什么要计算平方根倒数？
- 这个`0x5f3759df`有什么用途？

虽然这段代码已经过时了，但是同学们拿它来预习浮点数标准和牛顿迭代法也是很不错的

## 为什么要计算平方根倒数？

首先，我们需要知道什么是**向量单位化**

单位向量在计算机图形学中只表示方向，它被用于计算各种物理效果，例如光照效果

图形学中一般用笛卡尔坐标系来描述向量，我们一般认为向量永远从原点(0, 0)开始

要将向量单位化，首先需要求出向量的长度，而求向量长度的公式是

$$
\sqrt{x^2+y^2+z^2}
$$

接下来，我们需要将向量中的各个元素比上向量的长度，以`x`为例，也就是

$$
\frac{x}{\sqrt{x^2+y^2+z^2}}
$$

或者乘以向量长度的倒数，也就是

$$
x \cdot \frac{1}{\sqrt{x^2+y^2+z^2}}
$$

后一种做法使得其它元素(y和z)可以直接乘以倒数的计算结果，而倒数计算这部分也可以进行优化

在计算机中，乘法计算相当的快，速度是除法计算的许多倍，显然，计算倒数这一过程会浪费很多时间和资源

在计算光照的场景下，一个3D模型往往有上千个三角形平面，如果每一个向量都要单位化，那么花费的时间太长了，玩家是无法接受的

__那么，如果求的是倒数的近似值，并且算法很快，就能够节省大量的时间__

于是，快速平方根倒数算法诞生了，此算法比直接使用浮点数除法要[快四倍](https://zh.wikipedia.org/wiki/%E5%B9%B3%E6%96%B9%E6%A0%B9%E5%80%92%E6%95%B0%E9%80%9F%E7%AE%97%E6%B3%95)，而若使用与《雷神之锤III竞技场》同为1999年发布的[Pentium III](https://zh.wikipedia.org/wiki/Pentium_III "Pentium III")中的[SSE](https://zh.wikipedia.org/wiki/SSE "SSE")指令rsqrtss计算，则计算平方根倒数的收敛速度更慢，[精度也更低](https://zh.wikipedia.org/wiki/%E5%B9%B3%E6%96%B9%E6%A0%B9%E5%80%92%E6%95%B0%E9%80%9F%E7%AE%97%E6%B3%95#cite_note-14)

---

## 引用

1.  [平方根倒数速算法](https://zh.wikipedia.org/wiki/%E5%B9%B3%E6%96%B9%E6%A0%B9%E5%80%92%E6%95%B0%E9%80%9F%E7%AE%97%E6%B3%95). (中文) 