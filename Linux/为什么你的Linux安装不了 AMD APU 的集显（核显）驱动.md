# 为什么你的Linux安装不了 AMD APU 的集显（核显）驱动

__副标题：为什么视频功能看起来并没有正常运行__

> 以我的配置(AMD A10-9700)为例，但广泛适用于AMD A系列处理器

### 问题的开始
为什么在我刷B……不是，是认真学习的时候系统监视器显示CPU占用率一路飙升啊！这个APU的集显可以暴打 NVIDIA GeForce 550 啊！

[![fkGjJO.png](https://z3.ax1x.com/2021/08/04/fkGjJO.png)](https://imgtu.com/i/fkGjJO)

用VLC看视频的时候

[![fktoQg.png](https://z3.ax1x.com/2021/08/04/fktoQg.png)](https://imgtu.com/i/fktoQg)

而如果是Windows10下的话曲线应该类似于这样

[![fkFlIx.png](https://z3.ax1x.com/2021/08/04/fkFlIx.png)](https://imgtu.com/i/fkFlIx)

我 很 好 奇

[![fkkmff.png](https://z3.ax1x.com/2021/08/04/fkkmff.png)](https://imgtu.com/i/fkkmff)

因为Ubuntu 设置中是这样显示的

[![fkiJDs.png](https://z3.ax1x.com/2021/08/04/fkiJDs.png)](https://imgtu.com/i/fkiJDs)

附加驱动中是这样显示的

[![fklyE8.png](https://z3.ax1x.com/2021/08/04/fklyE8.png)](https://imgtu.com/i/fklyE8)

而Blender里是这样显示的，而win10会显示我的CPU和集显

[![fkkYt0.png](https://z3.ax1x.com/2021/08/04/fkkYt0.png)](https://imgtu.com/i/fkkYt0)

在将VLC调整为下面这样之前它甚至不能正常退出

[![fktISS.png](https://z3.ax1x.com/2021/08/04/fktISS.png)](https://imgtu.com/i/fktISS)

[![fkt4W8.png](https://z3.ax1x.com/2021/08/04/fkt4W8.png)](https://imgtu.com/i/fkt4W8)

那么首先是

## AMD® Carrizo

> 这是 AMD 公司于2015年2月25日发布的关于系统级芯片“Carrizo”架构细节消息

[![fkiUU0.png](https://z3.ax1x.com/2021/08/04/fkiUU0.png)](https://imgtu.com/i/fkiUU0)

__说实话我看不出什么__
于是我翻了翻国外的上古文章（[原文](https://www.notebookcheck.net/AMD-Carrizo-Mainstream-APUs-Overview.144035.0.html)），其中有这么一段话

> You can obviously still use OpenCL with the graphics cores. AMD once again emphasizes the advantage of the powerful GPU compared to the mainstream processors from Intel.

译文：

> 显然，您仍然可以将OpenCL与图形内核一起使用。AMD再次强调，与英特尔的主流处理器相比，强大的GPU具有优势。

__诶那我的 Blender 怎么……__
这就很迷惑
那为什么用`Chrome`看视频的时候`CPU`会飙升呢？

## Chrome看视频CPU占用率高的原因

这可能和`Chrome`底层渲染框架`Skia`有关

[![fkrISI.png](https://z3.ax1x.com/2021/08/04/fkrISI.png)](https://imgtu.com/i/fkrISI)

> 英文版确实更好一些

`Skia`的主要功能是当`GPU`不可用或其驱动出现重大错误时通过`CPU`实现`OpenGL`来替代显卡的功能
__那就是说我的集显坏了或者是因为没有驱动__
可我就算翻 Linux 内核驱动代码我也不一定能明白啊
不过一些简单的命令我还是会一点的

## 检测显卡的命令

当前 VGA 接口的输出

```bash
# 当前 VGA 接口的输出
lspci -vnn | grep VGA -A 12
# lshw 是列出硬件(list hardware)，这里列出显示器
sudo lshw -C display
```

对应输出

[![fkiwCT.png](https://z3.ax1x.com/2021/08/04/fkiwCT.png)](https://imgtu.com/i/fkiwCT)

[![fkiYbn.png](https://z3.ax1x.com/2021/08/04/fkiYbn.png)](https://imgtu.com/i/fkiYbn)

### 分析
对目前问题最重要的输出分别是
第一条命令的
第二行：Subsystem
这条输出说明了系统现在正在使用的是`AMD/ATI Radeon R7 Graphics`
也就是说集成显卡正在被正常使用
倒数第二行： Kernel driver in use
这条输出说明内核驱动目前使用的是`amdgpu`

第二条命令的
第三行： product
也就是说显示输出用的确实是我的`R7 Graphics`集显
__(´･ω･`)?（大雾），啊？？？ヽ(゜Q。)ノ？__

## AMDGPU
> 那既然核显的驱动已经被集成到 Linux 内核里面了，那我更加好奇这到底是个什么东东了

```bash
# modinfo会显示kernel模块的对象文件，以显示该模块的相关信息
modinfo amdgpu
```

__很好我没懂__
那它总该实现了`OpenGL`或`OpenCL`吧

```bash
# 这一条是为了 glxinfo
sudo apt install mesa-utils
# 用于检测 OpenGL 的实现
glxinfo | grep OpenGl
```

__欸????????__
不过确实没有实现

[![fk8JEV.png](https://z3.ax1x.com/2021/08/04/fk8JEV.png)](https://imgtu.com/i/fk8JEV)

不过视频 SoC 依旧可用

[![fkia5V.png](https://z3.ax1x.com/2021/08/04/fkia5V.png)](https://imgtu.com/i/fkia5V)

## VAAPI（拓展）
以下是生草姬（Google 翻译）的翻译

[![fki08U.png](https://z3.ax1x.com/2021/08/04/fki08U.png)](https://imgtu.com/i/fki08U)

## 总结

- AMD A系列处理器的显卡驱动已经被内置于Linux 内核中了
- GPU 可用，但并没有实现OpenGL和OpenCL
- 对应视频功能的SoC可用，但需要在软件中手动设置使用VAAPI 

## 引用
[AMD 透露高性能、高能效系统级芯片“Carrizo”架构细节](https://www.amd.com/zh-hans/press-releases/press-release-2015feb25)
[AMD Carrizo Mainstream APUs Overview](https://www.notebookcheck.net/AMD-Carrizo-Mainstream-APUs-Overview.144035.0.html)
(en) [Wikipedia: Skia Graphics Engine](https://en.wikipedia.org/wiki/Skia_Graphics_Engine)
[万物皆可对比](https://versus.com/cn/amd-a10-9700-vs-intel-core-i5-10600k)
(en) [Wikipedia: Video Acceleration API](https://en.wikipedia.org/wiki/Video_Acceleration_API#Processeurs_Nvidia_et_AMD)

---

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/88x31.png" /></a><br />本作品采用<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/">知识共享署名-非商业性使用-禁止演绎 4.0 国际许可协议</a>进行许可。

作品所有权归属于：hattori-emi <a7b8i06c49@outlook.com>