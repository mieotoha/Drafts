1. 安装

    1. 如何安装Julia
        1. Windows下安装
        2. Linux/OS X下安装

    2. 一个合适的IDE
        1. VSCode
        2. Atom
        3. IDEA
        4. REPL/Jupyter
    
2. 可以参考的好教程
    1. 视频推荐
    2. 文章推荐

3. 如何快速构建一个项目
    1. 误区
    2. 用`Pkg`的大佬
    3. `PkgTemplates.jl`真好

4. 你看那CI/CD
    1. Travis CI
    2. Codecov

5. 从写一个卷积函数开始

## 安装

### 如何安装Julia

#### Windows下安装

> __方法一__:[去官网](https://julialang.org)

__截至2021-02-16,最新稳定版是v1.5.3__<del>但是我们明显不会用它,1.6.0-rc1多香啊</del>

[![yckFUK.png](https://img-blog.csdnimg.cn/img_convert/ed817ccdfd8463fee14e0735726b680f.png)](https://imgchr.com/i/yckFUK)

__点击那个最大的绿色的东西__

[![yckpuR.png](https://img-blog.csdnimg.cn/img_convert/64cc0e8af52f9bb4864d549be1d672e3.png)](https://imgchr.com/i/yckpuR)

__可以看到Julia有很多操作系统的预编译结果__

[![yck9D1.png](https://img-blog.csdnimg.cn/img_convert/9a4344c95cbdea814d271ab22234c5dd.png)](https://imgchr.com/i/yck9D1)

__稍微往下滑,选择`Windows`一行的第一个(如果你是64位操作系统)__

下载安装,很方便了

> 方法二:去不了官网去[中国科学技术大学的Julia镜像站](https://mirrors.ustc.edu.cn/julia-releases/bin/)

[![ycFxgJ.png](https://img-blog.csdnimg.cn/img_convert/ad5e27396cfcd925228f3d7638531023.png)](https://imgchr.com/i/ycFxgJ)

__进入`winnt`选择x64(如果你是64位操作系统)1.6,下载倒数第三个,看清楚咯~__

[![ycFzv9.png](https://img-blog.csdnimg.cn/img_convert/3c6bb422865e291a30dda397780c6902.png)](https://imgchr.com/i/ycFzv9)
#### Linux/OS X下安装

> 方法一:我爱`jill`!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

> 注: 
>
> 1. Ubuntu 20.10(以及20.04)亲测需要使用`python3-pip`而不是简单的使用`pip`安装
> 2. -i 参数用于设置镜像站的使用

```shell
sudo pip3 install jill -i https://mirrors.aliyun.com/pypi/simple
sudo jill install 1.6.0-rc1
```

__看起来大概是这样的__

[![yckiE6.png](https://img-blog.csdnimg.cn/img_convert/6c563920742d31daf2cbd3054d8204d4.png)](https://imgchr.com/i/yckiE6)
> 方法二:自行解压并设置

这个真的没什么心情讲......

### 一个合适的IDE

#### VSCode

> 国内大家的最爱

请到[这里](https://code.visualstudio.com/Download)来~

[![ycA0OA.png](https://img-blog.csdnimg.cn/img_convert/23667384a2859a23b38cf7bbdf15a97a.png)](https://imgchr.com/i/ycA0OA)

__进入VSCode,看向左边,点击这个__

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210216101721797.png#pic_center)

__看到这里~,当然你也可以先安装中文插件__

![在这里插入图片描述](https://img-blog.csdnimg.cn/2021021610174767.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0NzQ0OTYx,size_16,color_FFFFFF,t_70#pic_center)

__在输入框里面输入`Julia`__

[![yckECD.png](https://img-blog.csdnimg.cn/img_convert/43255a4a89c9337aa0c30ab76655721a.png)](https://imgchr.com/i/yckECD)

__还有一个很好用的插件叫`Code Runner`__

[![6KAR58.png](https://s3.ax1x.com/2021/03/07/6KAR58.png)](https://imgtu.com/i/6KAR58)

__安装后记得重启IDE(如果同时安装了中文插件)__

#### Atom

> 一看就知道肯定是GitHub钦定的IDE

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210216121538554.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0NzQ0OTYx,size_16,color_FFFFFF,t_70#pic_center)

__它会自动根据你的操作系统给你选择下载安装__

> 那些高级黑魔法自己找,反正探究原子是少不了黑魔法的,否则就好好等吧

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210216121601439.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0NzQ0OTYx,size_16,color_FFFFFF,t_70#pic_center)

__来,一起看到最右边的第四个`Install a Package`~__

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210216121635573.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0NzQ0OTYx,size_16,color_FFFFFF,t_70#pic_center)

__点击`Open Installer`,然后在中间的输入框里面输入`Juno`,最后把所有属于`JunoLab`的插件全部下载掉__

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210216121652423.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0NzQ0OTYx,size_16,color_FFFFFF,t_70#pic_center)

__这样就可以了~__

#### IDEA

> 像我这种从Java转过来的同学可喜欢了

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210216121710786.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0NzQ0OTYx,size_16,color_FFFFFF,t_70#pic_center)

__安装过程不说太多,这里我只提供Ubuntu用户的小贴士(我就是偏心怎么了,你打我亚哦吼吼w)__

```shell
sudo mv idea-IC-203.7148.57/ /opt
```

切换到`opt/idea-IC-203.7148.57/bin`下

```shell
./idea.sh
```

__注意不要`sudo`__

一路下去就可以了

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210216121728629.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0NzQ0OTYx,size_16,color_FFFFFF,t_70#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210216121742386.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0NzQ0OTYx,size_16,color_FFFFFF,t_70#pic_center)

__开发用的IDE到此结束!__

#### REPL/Jupyter

![REPL](https://img-blog.csdnimg.cn/20210225203447309.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0NzQ0OTYx,size_16,color_FFFFFF,t_70#pic_center)

__简单粗暴__

![IJulia](https://img-blog.csdnimg.cn/20210225203601829.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0NzQ0OTYx,size_16,color_FFFFFF,t_70#pic_center)

```shell
pkg> add IJulia
```

第一次安装会自动添加Julia内核

__注意:使用`IJulia`之前请确保你已经安装了`Jupyter`__

## 可以参考的好教程

### 你不喜欢天天看文档?

[BiliBili | MIT《计算思维导论》2020秋季 18.S191 Introduction to Computational Thinking](https://www.bilibili.com/video/BV12V411m7zU)

> 注：B站上的字幕并不完整，如果英语能力不错，那么同学你可以用黑魔法去Youtube

[Youtube | Computational Thinking | MIT 18.S191 Fall 2020](https://youtu.be/vxjRWtWoD_w)

> 注：字幕良心

### 你不喜欢天天看视频?

[Think Julia: How to Think Like a Computer Scientist](https://benlauwens.github.io/ThinkJulia.jl/latest/book.html)

[Julia中文文档](https://docs.juliacn.com/latest/)

[Julia官方文档](https://docs.julialang.org/en/v1/)

[Julia中文社区](https://discourse.juliacn.com/)

[Julia官方社区](https://discourse.julialang.org/)

## 如何快速构建一个项目

### 误区

用`VSCode`新建文件夹和文件

事实上一个正常的Julia项目必须要有一个`Project.toml`文件，但是这个文件并不是简简单单的“新建”就可以了的

一个标准的`Project.toml`文件应该有以下内容

> [文档](https://docs.juliacn.com/latest/stdlib/Pkg/#%E8%AF%8D%E6%B1%87%E8%A1%A8)有写

- 项目的名称
- UUID（针对包）
- 作者
- 许可证
- 它所依赖的包和库的名称及 UUID

但如果你只打算把它当做脚本的话

用Python啊！

### 用`Pkg`的大佬

> 同样，[文档](https://docs.juliacn.com/latest/stdlib/Pkg/#Creating-your-own-packages)有写

在`pkg`模式下使用`generate`命令创建

示例：

```julia
(@v1.6) pkg> generate Umbrella    # 注：这里的Umbrella可以替换成你的项目名称
```

这样，一个简简单单的Julia项目就创建成功了

### `PkgTemplates.jl`真好

首先你要在Julia REPL下添加这个包

```julia
(@v1.6) pkg> add PkgTemplates
```

在使用前你需要进行以下设置

- `user.name`: git下你的名字
- `user.email`: git下你的电子邮箱
- `github.user`: GitHub上你的名称

> GitHub有对应文档
>
> [设置用户名](https://docs.github.com/cn/github/getting-started-with-github/setting-your-username-in-git)
>
> [设置电子邮箱](https://docs.github.com/cn/github/setting-up-and-managing-your-github-user-account/setting-your-commit-email-address)

示例：

```bash
git config --global user.name "Monica"
git config --global user.emali "monica@cuievhuwiex.com"
git config --global github.user "hentaidesu"
```

接下来开始使用`PkgTemplates.jl`

```julia
using PkgTemplates

tpl = Template(;
    dir="~/code",
    plugins=[
        Git(; manifest=true, ssh=true),
        Codecov(),
        TravisCI(; x86=true),
        Documenter{TravisCI}(),
    ],
)

tpl("Umbrella")

```

以上

## 问题集中营

> 与政治或历史无关

__将会按首字母顺序将问题排序并尽可能解决__

### 如何安装Jupyter

```shell
sudo apt install python3-pip
sudo pip3 install jupyterlab -i https://mirrors.aliyun.com/pypi/simple
```

以上

### 为什么VSCode下看不了Julia相关包的源码?

__注意:我个人使用了IDEA快捷键映射__

首先,我已经证实在1.5.3版本下VSCode无法查看源码,我个人使用的是1.6.0-rc1版本,可以按下`Ctrl`键并点击鼠标左键查看源码

__解决方案:截至今日(2021-2-25),我最佳的解决方案是更新至`Julia v1.6.0-rc1`,相关教程或文章请参见[CSDN上的文章](https://blog.csdn.net/qq_44744961/article/details/113753975)或[知乎上的文章](https://zhuanlan.zhihu.com/p/352953152)__

***

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/88x31.png" /></a><br />本作品采用<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/">知识共享署名-非商业性使用-禁止演绎 4.0 国际许可协议</a>进行许可。