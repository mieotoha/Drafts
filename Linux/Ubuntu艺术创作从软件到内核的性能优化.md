> 这篇文章包含了对文章，音频，直播，视频，图片编辑，乃至3D的创造体验及通用性能优化的内容，虽然后半段对读者技术力要求较高，但其中的代码可以安心的复制和使用

__截止9月28日，我是Blender OpenData中AMD A10-9700 世界第一名，其中同操作系统下classrom领先第二名1555秒__

# 软件级

## 文字创作



## 音频创作



## 图片编辑



## 直播与录屏



## 视频剪辑



## 3D相关



# 内核级

Linux提供了五种内核类型，对于内核类型的选择，可以参考如下的解释：[来源](https://askubuntu.com/questions/126664/why-choose-a-low-latency-kernel-over-a-generic-or-real-time-kernel)

If you do not require low latency for your system then please use the -generic kernel.

> 如果你不要求你的系统相应很快（低延迟），请用通常型内核

If you need a low latency system (e.g. for recording audio) then please use the -preempt kernel as a fist choice. This reduces latency but doesn't sacrifice power saving features. It is available only for 64 bit systems (also called amd64).

> 如果您需要低延迟系统（例如用于录制音频），请首先选择抢占型内核。这可以减少延迟，但不会放弃省电。它仅适用于64位系统（也称为amd64）
>
> 注：抢占型内核是允许内核空间进行进程抢占的实现，后文将会解释什么是「抢占」

If the -preempt kernel does not provide enough low latency for your needs (or you have an 32 bit system) then you should try the -lowlatency kernel.

> 如果抢占型内核不能提供足够低的延迟以满足你的需求（或者你用的是32位系统），则应尝试-lowlatency内核

If the -lowlatency kernel isn't enough then you should try the -rt kernel

> 低延迟型内核还不够就用实时型内核

If the -rt kernel isn't enough stable for you then you should try the -realtime kernel

> 如果实时型内核不够稳定就用稳定实时型内核

也就是：

1. 通常型：generic
2. 抢占型：preempt
3. 低延迟型：lowlatency
4. 实时型：RT
5. 稳定实时型：realtime

更为详尽的[英文文章](https://sevencapitalsins.wordpress.com/2007/08/10/low-latency-kernel-wtf/)

## 通常型

这种内核是各大桌面级Linux发行版的默认内核，貌似有着更省电的能力

## 抢占型

首先，什么是「抢占」（[引用出处](http://linuxperf.com/?p=211)）

> 抢占(Preemption)是指内核强行切换正在CPU上运行的进程，在抢占的过程中并不需要得到进程的配合，在随后的某个时刻被抢占的进程还可以恢复运行。发生抢占的原因主要有：进程的时间片用完了，或者优先级更高的进程来争夺CPU了

## 低延迟型

顾名思义，低延迟，但是相对耗电

## 实时型

> PREEMPT_RT是Linux内核的一个实时补丁。得到Linus的高度评价：
> Controlling a laser with Linux is crazy, but everyone in this room is crazy in his own way. So if you want to use Linux to control an industrial welding laser, I have no problem with your using PREEMPT_RT." -- Linus Torvalds

### Xanmod 内核

首先，什么是[Xanmod 内核](https://xanmod.org/)

**XanMod** is a general-purpose [Linux](https://www.kernel.org/) kernel distribution with custom settings and new features. Built to provide a stable, responsive and smooth desktop experience.

> XanMod是一个通用Linux内核发行版，具有自定义设置和新功能。专为提供稳定、快速响应和流畅的桌面体验而设计

The real-time version is recommended for critical runtime applications such as Linux gaming eSports, streaming, live productions and ultra-low latency enthusiasts.

> 实时版本建议用于关键运行时应用程序，如Linux游戏电子竞技、流媒体、现场制作和超低延迟爱好者
>
> 小声BB：其实对于3D渲染也有一定效果

Supports all recent x86_64 versions of Ubuntu / Debian-based systems.

> 支持所有基于Ubuntu/Debian的最新x86_64系统

> Note: The current proprietary NVIDIA, VirtualBox, VMware Workstation / Player and some other dkms modules builds do not officially support Clang'ed (EDGE) and RT kernels.
>
> 注意：当前专有的NVIDIA、VirtualBox、VMware Workstation/Player和其他一些dkms模块版本不正式支持Clang'ed（EDGE）和RT内核
>
> 人话版：不开源的显卡驱动、虚拟机软件，还有其它内核模块可能不支持这个内核
>
> 小声BB：没事我一直用的集显，驱动什么的根本不怕，就算用不了集显，这个CPU被我强行提升到能勉强能够打过`Intel Core i5-9600K`（并没有），<del>__已经没有什么好怕的了__</del>

### 跑分数据

> 第一组：
>
> 硬件：`AMD A10-9700`
>
> 软件：cyclictest
>
> 操作系统：`Ubuntu 20.04`
>
> 内核：`5.13.19-xanmod1`
>
> 数据获取时间：2021-09-21 16:40:00

状态：低负载(最大优先级)

```bash
mieotoha@mieotoha-A320M:~$ sudo cyclictest -t 4 -p 99
# /dev/cpu_dma_latency set to 0us
policy: fifo: loadavg: 0.77 1.44 1.90 1/890 575862          

T: 0 (575393) P:99 I:1000 C:  24672 Min:      1 Act:    1 Avg:    2 Max:      67
T: 1 (575394) P:99 I:1500 C:  16448 Min:      1 Act:    1 Avg:    2 Max:      68
T: 2 (575395) P:99 I:2000 C:  12336 Min:      1 Act:    2 Avg:    2 Max:      34
T: 3 (575396) P:99 I:2500 C:   9869 Min:      1 Act:    2 Avg:    2 Max:      52
```

状态：高负载(最大优先级)

```bash
mieotoha@mieotoha-A320M:~$ sudo cyclictest -t 4 -p 99
# /dev/cpu_dma_latency set to 0us
policy: fifo: loadavg: 2.11 1.24 1.64 5/707 583649           

T: 0 (582703) P:99 I:1000 C:  24358 Min:      3 Act:    6 Avg:   11 Max:      76
T: 1 (582704) P:99 I:1500 C:  16238 Min:      5 Act:    6 Avg:   13 Max:      82
T: 2 (582705) P:99 I:2000 C:  12179 Min:      4 Act:    7 Avg:   11 Max:      72
T: 3 (582706) P:99 I:2500 C:   9742 Min:      4 Act:    6 Avg:   10 Max:      74
```

状态：低负载(普通优先级)

```bash
mieotoha@mieotoha-A320M:~$ sudo cyclictest -t 4 -p 20
# /dev/cpu_dma_latency set to 0us
policy: fifo: loadavg: 0.74 1.18 1.56 1/681 587837           

T: 0 (587337) P:20 I:1000 C:  24255 Min:      1 Act:    2 Avg:    2 Max:      60
T: 1 (587338) P:20 I:1500 C:  16170 Min:      2 Act:    3 Avg:    3 Max:      72
T: 2 (587339) P:20 I:2000 C:  12127 Min:      1 Act:    2 Avg:    2 Max:      34
T: 3 (587340) P:20 I:2500 C:   9702 Min:      1 Act:    2 Avg:    2 Max:      26
```

状态：高负载(普通优先级)

```bash
mieotoha@mieotoha-A320M:~$ sudo cyclictest -t 4 -p 20
# /dev/cpu_dma_latency set to 0us
policy: fifo: loadavg: 2.30 1.40 1.58 5/722 591073           

T: 0 (590610) P:20 I:1000 C:  24632 Min:      3 Act:    8 Avg:   10 Max:      93
T: 1 (590611) P:20 I:1500 C:  16424 Min:      3 Act:    9 Avg:   11 Max:      88
T: 2 (590612) P:20 I:2000 C:  12318 Min:      3 Act:    5 Avg:    7 Max:      67
T: 3 (590613) P:20 I:2500 C:   9853 Min:      3 Act:    8 Avg:    8 Max:      68
```



> 第二组：
>
> 软件：benchmark-launcher-2.0.5-linux
>
> 操作系统：`Ubuntu 20.04`
>
> 内核：`5.13.19-xanmod1`
>
> 来源：[Blender Open Data](https://opendata.blender.org/)
>
> 数据获取时间： 2021-09-21 16:00 UTC +8:00
>
> 注意：由于参与测试的人数可能较少，测试结果偶然性较大

参考：`Intel i5-9600k`(非本机)

| Device Name                       | Device Type | Operating System | Scene               | Blender Version | Median Render Time | Number of Benchmarks |
| :-------------------------------- | :---------: | :--------------: | :-----------------: | :-------------: | :----------------: | :------------------: |
| Intel Core i5-9600K CPU @ 3.70GHz	| CPU         | Linux            | bmw27               | 2.79            | 381.482            | 1                    |
| Intel Core i5-9600K CPU @ 3.70GHz | CPU         | Linux            | classroom           | 2.79            | 1239.17            | 1                    |
| Intel Core i5-9600K CPU @ 3.70GHz | CPU         | Linux            | fishy_cat           | 2.81            | 471.361            | 1                    |
| Intel Core i5-9600K CPU @ 3.70GHz | CPU         | Linux            | koro                | 2.81            | 610.63             | 1                    |
| Intel Core i5-9600K CPU @ 3.70GHz | CPU         | Linux            | pavillon_barcelona  | 2.9             | 1130.73            | 1                    |
| Intel Core i5-9600K CPU @ 3.70GHz | CPU         | Linux            | victor              | 2.9             | 1747.05            | 1                    |

对比：`AMD A10-9700 RADEON R7`

| Device Name                                    | Device Type | Operating System |       Scene        | Blender Version | Median Render Time | Number of Benchmarks |
| ---------------------------------------------- | :---------: | :--------------: | :----------------: | :-------------: | :----------------: | :------------------: |
| AMD A10-9700 RADEON R7, 10 COMPUTE CORES 4C+6G |     CPU     |      Linux       |       bmw27        |      2.93       |      982.822       |          1           |
| AMD A10-9700 RADEON R7, 10 COMPUTE CORES 4C+6G |     CPU     |      Linux       |     classroom      |      2.93       |      3183.24       |          1           |
| AMD A10-9700 RADEON R7, 10 COMPUTE CORES 4C+6G |     CPU     |      Linux       |     fishy_cat      |      2.93       |      1601.53       |          1           |
| AMD A10-9700 RADEON R7, 10 COMPUTE CORES 4C+6G |     CPU     |      Linux       |        koro        |      2.93       |      1843.55       |          1           |
| AMD A10-9700 RADEON R7, 10 COMPUTE CORES 4C+6G |     CPU     |      Linux       | pavillon_barcelona |      2.93       |      3507.79       |          1           |
| AMD A10-9700 RADEON R7, 10 COMPUTE CORES 4C+6G |     CPU     |      Linux       |       victor       |      2.93       |      6543.95       |          1           |

# 结论

嗯，我说的没错，勉强能够打过`Intel Core i5-9600k`<del>(指只有`Intel Core i5-9600k`性能的1/3)</del>

# 引用

1. [Why choose a low latency kernel over a generic or real-time kernel?](https://askubuntu.com/questions/126664/why-choose-a-low-latency-kernel-over-a-generic-or-real-time-kernel) 2012-04-28 **(English)**
2. [RTwiki](https://rt.wiki.kernel.org/index.php/Main_Page) **(English)**
3. 
4. VMUNIX. [抢占(PREEMPTION)是如何发生的](http://linuxperf.com/?p=211) 2018-02-09 **（中文）**.
5. sevencapitalsins(Luca - sevendays). [LOW-LATENCY KERNEL? WTF?!?!](https://sevencapitalsins.wordpress.com/2007/08/10/low-latency-kernel-wtf/) **(English)**

