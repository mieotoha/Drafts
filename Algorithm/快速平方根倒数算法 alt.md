今天我们来讲一下这段被载入史册的魔法(代码)——快速平方根倒数算法

> 事先说明：
> - 文章有来自维基百科的内容，因此本文采用CC BY-SA 3.0协议
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

接下来，我们需要将向量中的各个元素比上向量的长度，也就是

$$
\frac{x}{\sqrt{x^2+y^2+z^2}}
$$

$$
\frac{y}{\sqrt{x^2+y^2+z^2}}
$$

$$
\frac{z}{\sqrt{x^2+y^2+z^2}}
$$

或者乘以向量长度的倒数，也就是

$$
x \cdot \frac{1}{\sqrt{x^2+y^2+z^2}}
$$

后一种做法使得其它元素(y和z)可以直接乘以倒数计算的结果，而倒数计算这部分也可以进行优化

在计算机中，乘法计算相当的快，速度是除法计算的许多倍，显然，倒数计算这一过程会浪费很多时间和资源

在计算光照的场景下，一个3D模型往往有上千个三角形平面，如果每一条光线的向量都要单位化，那么花费的时间太长了，玩家是无法接受的

__那么，如果求的是倒数的近似值，并且算法很快，就能够节省大量的时间__

(以下摘自维基百科)
于是，快速平方根倒数算法诞生了，此算法比直接使用浮点数除法要[快四倍](https://zh.wikipedia.org/wiki/%E5%B9%B3%E6%96%B9%E6%A0%B9%E5%80%92%E6%95%B0%E9%80%9F%E7%AE%97%E6%B3%95)，而若使用与《雷神之锤III竞技场》同为1999年发布的[Pentium III](https://zh.wikipedia.org/wiki/Pentium_III "Pentium III")中的[SSE](https://zh.wikipedia.org/wiki/SSE "SSE")指令rsqrtss计算，则计算平方根倒数的收敛速度更慢，[精度也更低](https://zh.wikipedia.org/wiki/%E5%B9%B3%E6%96%B9%E6%A0%B9%E5%80%92%E6%95%B0%E9%80%9F%E7%AE%97%E6%B3%95#cite_note-14)

## 代码分析

接下来我们回到魔法(代码)的第一行

```c
float q_rsqrt(float number){  
 ......  
}
```

第一行很简单，这个函数要求传入一个浮点数值`number`，它就是`x²+y²+z²`的值，而这个函数会计算这个值的平方根倒数

```c
long i;                           // 32位整形  
float x2, y;                      // 32位单精度浮点数  
const float threehalfs = 1.5F;    // 32位单精度浮点数常量
```

`threehalfs`的意思是`二分之三`

```c
x2 = number * 0.5F;
y = number;
```

接下来也只是很简单的将形参除以2后放入`x2`，完整的形参放入`y`

__现在，重点来了__

## IEEE 754标准

```c
i = * (long * ) &y;                      // evil floating point bit level hacking
```

首先，我们需要知道`IEEE 754`标准是什么，这是理解“evil floating point bit level hacking”这行魔法(代码)的重要知识

(以下摘自维基百科，有删改)
**[IEEE](https://zh.wikipedia.org/wiki/%E7%94%B5%E6%B0%94%E7%94%B5%E5%AD%90%E5%B7%A5%E7%A8%8B%E5%B8%88%E5%8D%8F%E4%BC%9A "电气电子工程师协会")二进制浮点数算术标准**（**IEEE 754**）是[浮点数](https://zh.wikipedia.org/wiki/%E6%B5%AE%E9%BB%9E%E6%95%B8 "浮点数")运算标准，这个标准定义了表示浮点数的格式（包括负零[-0](https://zh.wikipedia.org/wiki/-0 "-0")）与反常值，一些特殊数值（（[无穷](https://zh.wikipedia.org/wiki/%E7%84%A1%E7%AA%AE "无穷")（Inf）与[非数值](https://zh.wikipedia.org/wiki/NaN "NaN")（NaN））

其实32位浮点数表达方式的灵感来源于科学计数法，让我们先复习一下十进制中的科学计数法

$$
0.00000000000000000016 = 1.6 \times 10^{-19}
$$

这个`10`便是`十进制`，它的指数决定了`1.6`的“位置”

类似的，在二进制中我们可以这样表示任意一个数字(乘2取整法)

$$
11111.01 = 1.11101 \times 2^{4}
$$

不过这样不但会浪费大量空间，而且精度低

举个栗子，在表达十进制中类似于二分之一(0.5)、四分之一(0.25)、八分之一(0.125)这样的数字时，二进制能很方便的转变为`0.1`、`0.01`、`0.001`……这样的数字

而一旦表达十进制中的`0.1`时，二进制就需要在空间和精度之间取舍，比如选择精度时就会变成`0.0001100110011001100110011001100110011001100110011001101`，即便是这样也还是会有损失

当然，上个世纪的天才们想到了更好的方法来利用这32位

---

## 引用

1. 维基百科.  [平方根倒数速算法](https://zh.wikipedia.org/wiki/%E5%B9%B3%E6%96%B9%E6%A0%B9%E5%80%92%E6%95%B0%E9%80%9F%E7%AE%97%E6%B3%95). (中文) 
2. 维基百科. [IEEE 754](https://zh.wikipedia.org/wiki/IEEE_754). (中文)

---

<center><a rel="license" href="http://creativecommons.org/licenses/by-sa/3.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/3.0/88x31.png" /></a><br />本作品采用<a rel="license" href="http://creativecommons.org/licenses/by-sa/3.0/">知识共享署名-相同方式共享 3.0 国际许可协议</a>进行许可</center>