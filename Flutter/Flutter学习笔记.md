---
title: Flutter学习笔记
date: 2021-03-7T11:59:30.000+08:00
tags: 
- Flutter
---

## 环境配置

> 由于我个人只有`Ubuntu 20.10`的环境(`OS X`的环境不可用),所以这里只进行`Linux`环境下的`Flutter`安装与环境配置

### SDK

> 我使用的是`VSCode`,而不是已经在我电脑里面的`Android Studio`或`IDEA`

__[中文官网](https://flutter.cn/docs/get-started/install/linux)有安装教程__

推荐使用`Snap`安装`Flutter`，但这并不是最佳做法

```sh
sudo snap install flutter --classic
```

> 当`IDE`需要`Flutter SDK`路径时,可以使用以下命令
>
> ```sh
> flutter sdk-path
> ```

### 环境变量

Linux下

编辑于`etc/profile`最后一行

```sh
export FLUTTER_STORAGE_BASE_URL="https://mirrors.tuna.tsinghua.edu.cn/flutter"
export PUB_HOSTED_URL="https://mirrors.tuna.tsinghua.edu.cn/dart-pub"
```

运行`source /etc/profile`来加载更改

### IDE

__`VSCode`需要安装三个插件,其中`Flutter`插件安装时会自动安装`Dart`插件,后两个可选__

[![6KEZxH.png](https://s3.ax1x.com/2021/03/07/6KEZxH.png)](https://imgtu.com/i/6KEZxH)

[![6KAR58.png](https://s3.ax1x.com/2021/03/07/6KAR58.png)](https://imgtu.com/i/6KAR58)

[![6KGlG9.png](https://s3.ax1x.com/2021/03/07/6KGlG9.png)](https://imgtu.com/i/6KGlG9)

这样就设置完成了，接下来是对各平台的支持

__[使用`Flutter`创建`Ubuntu`桌面应用程序](https://cn.ubuntu.com/blog/canonical-enables-linux-desktop-app-support-with-flutter-2)__

```bash
flutter config --enable-linux-desktop
```

__使用`Flutter`创建`Windows`桌面应用程序__

```bash
flutter config --enable-windows-desktop
```

__使用`Flutter`创建`MacOS`桌面应用程序__

```bash
flutter config --enable-macos-desktop
```

最后是提前下载所需的平台特殊开发二进制文件

```bash
flutter precache
```

## 创建项目

__[中文官网]([中文官网](https://flutter.cn/docs/get-started/install/linux)有安装教程)有教程__

> __注：我安装了`IDEA`快捷键映射,可能会与你们``VSCode`的实际情况有差别__

按下`Alt`键，或通过`Ctrl + Shift + A`直接打开`命令面板`

在`查看(view) -> 命令面板(Command Palette)`输入`Flutter`

[![6KmiOH.png](https://s3.ax1x.com/2021/03/07/6KmiOH.png)](https://imgtu.com/i/6KmiOH)

选择第一个`New Application Project`

第一次会对`Flutter`进行初始化,运气不好就只能重装`Flutter SDK`了

__弹出这个窗口时就可以选择项目的主目录了__

[![6KnB28.png](https://s3.ax1x.com/2021/03/07/6KnB28.png)](https://imgtu.com/i/6KnB28)

> `Umbrella`是我个人的一个学习项目,里面是对于语言或框架的主流路线的学习代码

创建完成后,会有弹窗提示你是否要参与谷歌的调查问卷,这里不强制要求

> __注：当你在 `VSCode`中点击`No Devices`的时候，你也许看不到`Start iOS Simulator`选项,如果你使用`OS X`你可能得运行以下命令才能启动模拟器__
>
> ```sh
> open -a simulator
> ```

通过同样方式创建`Flutter`项目或在已有项目下

```bash
flutter create .
```

## 文件目录

>  像`android`和`ios`之类的目录应该不用我说了

### lib

> 这个文件夹是用来存放`Flutter`的工程文件的，其中`main.dart`是项目的入口(最初且必须的)文件

[![6dle5d.png](https://s3.ax1x.com/2021/03/13/6dle5d.png)](https://imgtu.com/i/6dle5d)

### test

> 测试文件夹，用于存放测试文件，很重要的

[![6d1MFJ.png](https://s3.ax1x.com/2021/03/13/6d1MFJ.png)](https://imgtu.com/i/6d1MFJ)

### 配置文件(pubspec.yaml)

> 声明第三方库依赖

[![6d18Qx.png](https://s3.ax1x.com/2021/03/13/6d18Qx.png)](https://imgtu.com/i/6d18Qx)

## 第一次运行

> 我使用了真机来运行项目，你们可以看到`CAM AL00`的选项(Android Studio)

在`main.dart`的编辑窗口下按下`F5`进行`debug`

[![6d1wYd.png](https://s3.ax1x.com/2021/03/13/6d1wYd.png)](https://imgtu.com/i/6d1wYd)

事 后

[![6d8VVU.png](https://s3.ax1x.com/2021/03/13/6d8VVU.png)](https://imgtu.com/i/6d8VVU)

亦或是在`Android Studio`下选择使用`web`/`Pixle 3a`并按下`Shift + F10`启动

[![6d8JaD.png](https://s3.ax1x.com/2021/03/13/6d8JaD.png)](https://imgtu.com/i/6d8JaD)

[![6d8Mx1.png](https://s3.ax1x.com/2021/03/13/6d8Mx1.png)](https://imgtu.com/i/6d8Mx1)

`Google`真香

## Coding from scratch

### 先从理解示例开始

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        // This is the theme of your application.
        //
        // Try running your application with "flutter run". You'll see the
        // application has a blue toolbar. Then, without quitting the app, try
        // changing the primarySwatch below to Colors.green and then invoke
        // "hot reload" (press "r" in the console where you ran "flutter run",
        // or simply save your changes to "hot reload" in a Flutter IDE).
        // Notice that the counter didn't reset back to zero; the application
        // is not restarted.
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
}

class MyHomePage extends StatefulWidget {
  MyHomePage({Key key, this.title}) : super(key: key);

  // This widget is the home page of your application. It is stateful, meaning
  // that it has a State object (defined below) that contains fields that affect
  // how it looks.

  // This class is the configuration for the state. It holds the values (in this
  // case the title) provided by the parent (in this case the App widget) and
  // used by the build method of the State. Fields in a Widget subclass are
  // always marked "final".

  final String title;

  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  int _counter = 0;

  void _incrementCounter() {
    setState(() {
      // This call to setState tells the Flutter framework that something has
      // changed in this State, which causes it to rerun the build method below
      // so that the display can reflect the updated values. If we changed
      // _counter without calling setState(), then the build method would not be
      // called again, and so nothing would appear to happen.
      _counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    // This method is rerun every time setState is called, for instance as done
    // by the _incrementCounter method above.
    //
    // The Flutter framework has been optimized to make rerunning build methods
    // fast, so that you can just rebuild anything that needs updating rather
    // than having to individually change instances of widgets.
    return Scaffold(
      appBar: AppBar(
        // Here we take the value from the MyHomePage object that was created by
        // the App.build method, and use it to set our appbar title.
        title: Text(widget.title),
      ),
      body: Center(
        // Center is a layout widget. It takes a single child and positions it
        // in the middle of the parent.
        child: Column(
          // Column is also a layout widget. It takes a list of children and
          // arranges them vertically. By default, it sizes itself to fit its
          // children horizontally, and tries to be as tall as its parent.
          //
          // Invoke "debug painting" (press "p" in the console, choose the
          // "Toggle Debug Paint" action from the Flutter Inspector in Android
          // Studio, or the "Toggle Debug Paint" command in Visual Studio Code)
          // to see the wireframe for each widget.
          //
          // Column has various properties to control how it sizes itself and
          // how it positions its children. Here we use mainAxisAlignment to
          // center the children vertically; the main axis here is the vertical
          // axis because Columns are vertical (the cross axis would be
          // horizontal).
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text(
              'You have pushed the button this many times:',
            ),
            Text(
              '$_counter',
              style: Theme.of(context).textTheme.headline4,
            ),
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _incrementCounter,
        tooltip: 'Increment',
        child: Icon(Icons.add),
      ), // This trailing comma makes auto-formatting nicer for build methods.
    );
  }
}

```

首先看到第一行

```dart
import 'package:flutter/material.dart';
```

这是使用`Flutter`进行开发的必要语句，它的意思是"导入`Flutter`包"

因为`dart`本质是一个语言，而`Flutter`是使用`dart`语言的UI工具包

接下来是这个方法

```dart
void main() {
  runApp(MyApp());
}
```

`void`是指不返回值

这是个`main`(入口)方法

就像要打开神奇的洞穴要大喊"芝麻开门"一样，要使用`Flutter`这是必须的

同时它可以写成

```dart
void main()=>runApp(MyApp());
```

而其中的`MyApp`，也就是下面的

```dart
class MyApp extends StatelessWidget {
// 此处省略
}
```

这是创建了一个`类(class)`叫做`MyApp`，它通过`extends`关键字`继承`了`StatelessWidget`这个类

让我们回到这句话

```dart
runApp(MyApp());
```

其中`runApp`是一个`方法`，它`实例化`了`MyApp`这个`类`，实例化可以写上`new`关键字，但也可以省略

```dart
runApp(new MyApp());
```

__那么为什么不直接写成`void main()=>runApp(StatelessWidget());`呢？__

首先，为了未来维护代码，你不应该把它写成一行，而且写成一行并不会带来可见的性能提升

其次，你通常会写很多元素，这会导致它非常大，为了易读性(代码是给人看的)，你应该创建一个类(自定义组件)，并在里面按照编码规范进行开发

__需要注意的是__

方法首字母小写，下一个单词首字母大写，也就是[驼峰命名法](https://baike.baidu.com/item/%E9%AA%86%E9%A9%BC%E5%91%BD%E5%90%8D%E6%B3%95)，而类则全部单词的首字母大写

__那么`StatelessWidget`是什么呢？__

它`Flutter`提供的一个组件(类)，是`无状态组件`，它的状态不可变，而且它是一个`抽象类`，它有一个`抽象方法`叫`build`

而`StatefulWidget`是之后会提到的`有状态组件`，它的状态可能在`widget生命周期`改变

__那么这个叫做"build"的抽象方法是干嘛用的？__

首先，抽象方法是“只有名字没有具体功能”的方法

它要求每个继承它的类都要强制实现这个方法

__那么让我们回到示例中的代码__

```dart
@override
Widget build(BuildContext context) {
  return MaterialApp(
    title: 'Flutter Demo',
    theme: ThemeData(
      // This is the theme of your application.
      //
      // Try running your application with "flutter run". You'll see the
      // application has a blue toolbar. Then, without quitting the app, try
      // changing the primarySwatch below to Colors.green and then invoke
      // "hot reload" (press "r" in the console where you ran "flutter run",
      // or simply save your changes to "hot reload" in a Flutter IDE).
      // Notice that the counter didn't reset back to zero; the application
      // is not restarted.
      primarySwatch: Colors.blue,
    ),
    home: MyHomePage(title: 'Flutter Demo Home Page'),
  );
}
```

`Widget`是一个组件(类)

而这个`bulid`方法就是返回`Widget`这个组件的(子类)方法，所以要在关键字`return`后面返回一个组件

而示例中的组件就是`MaterialApp`，有一定`Android`开发经验(没有经验的同学也看过来)的同学一定联想到了`material design`↖(^ω^)↗

没错，这就是基于`material design`的`Flutter`组件

__让我们稍微深入一下__

长按`Ctrl`键(注：我开启了IDEA快捷键映射)，点击`MaterialApp`

变成了现在这样：

[![cnJgr4.png](https://z3.ax1x.com/2021/04/03/cnJgr4.png)](https://imgtu.com/i/cnJgr4)

我们看到`title`这一项

[![cnJ2qJ.png](https://z3.ax1x.com/2021/04/03/cnJ2qJ.png)](https://imgtu.com/i/cnJ2qJ)

这是用于设置标题的`参数`

__那么再让我们回到示例中的代码__

看到这一段

```dart
theme: ThemeData(
        // This is the theme of your application.
        //
        // Try running your application with "flutter run". You'll see the
        // application has a blue toolbar. Then, without quitting the app, try
        // changing the primarySwatch below to Colors.green and then invoke
        // "hot reload" (press "r" in the console where you ran "flutter run",
        // or simply save your changes to "hot reload" in a Flutter IDE).
        // Notice that the counter didn't reset back to zero; the application
        // is not restarted.
        primarySwatch: Colors.blue,
      )
```

__首先__

它设置了`MaterialApp`的另一个属性，叫`theme`，就是这个代码块里的第一行第一个单词

而这个属性是一个叫`ThemeData`的类，它用于描述UI样式

__接下来看到注释__

它的大意是

> 这是应用程序的主题。试着用“flatter run”运行你的应用程序。您将看到应用程序有一个蓝色工具栏。然后，在不退出应用程序的情况下，尝试将下面的主色样更改为`Colors.green`，然后调用“hot reload”（在控制台中按“r”运行“flatter run”，或者在flatter IDE中将更改保存为“hot reload”）。请注意，计数器没有重置回零；应用程序没有重新启动

同时也向我们展示了一次热加载的强大......

上面这段注释`speak in English`就是

__原本它是蓝的，把`blue`改成`green`，再来一次`hot reload`，它就变绿了__

修改的就是倒数第二行

```dart
primarySwatch: Colors.blue
```

变成

```dart
primarySwatch: Colors.green
```

__让我们看一下`Colors`源码__

[![cntDjU.png](https://z3.ax1x.com/2021/04/03/cntDjU.png)](https://imgtu.com/i/cntDjU)

发现了这样一行代码

```dart
static const Color black = Color(0xFF000000);
```

`static`表示“静态的”，用于实现类级别的`变量`或`函数`

`const`表示“常数”，搭配`static`设置`常量`

这段代码的意思是：

一个叫`black`的`Color`类等于一个具有参数`0xFF000000`的`Color`类

而这个`0xFF000000`是`16进制`的代码

当然，其中内设了很多基于`material design`的颜色，而`green`和`blue`就是其中的参数

同时，你可以通过使用以下代码改成天依色

```dart
Color.fromARGB(255, 102, 204, 255)
```

但是它不能在这里用……

__那么下一行__

```dart
home: MyHomePage(title: 'Flutter Demo Home Page')
```

那么属性`home`对应的就是`MyHomePage`这个自定义类

跳到第30行的代码块~

```dart
class MyHomePage extends StatefulWidget {
  MyHomePage({Key key, this.title}) : super(key: key);

  // This widget is the home page of your application. It is stateful, meaning
  // that it has a State object (defined below) that contains fields that affect
  // how it looks.

  // This class is the configuration for the state. It holds the values (in this
  // case the title) provided by the parent (in this case the App widget) and
  // used by the build method of the State. Fields in a Widget subclass are
  // always marked "final".

  final String title;

  @override
  _MyHomePageState createState() => _MyHomePageState();
}
```

它继承的是一个`StatefulWidget`类

而这是它的一个基本结构

首先`StatefulWidget`是一个抽象类，它具有一个抽象方法`createState()`，也就是这一行代码

```dart
_MyHomePageState createState() => _MyHomePageState();
```

这个抽象方法是必须要实现的，因此要调用我们自定义的`MyHomePageState`，也就是这一段代码

```dart
class _MyHomePageState extends State<MyHomePage> {
// 此处省略部分代码
  @override
  Widget build(BuildContext context) {
    // 此处省略部分代码
  }
}
```

__那这个`_`是什么意思呢？__

它表示方法是私有的

`_MyHomePageState`这个类还需要继承`State`类，并且要实现里面的`build`方法

__终于〒▽〒，终于可以开始写内容了__

```dart
class _MyHomePageState extends State<MyHomePage> {
  int _counter = 0;

  void _incrementCounter() {
    setState(() {
      _counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text(
              'You have pushed the button this many times:',
            ),
            Text(
              '$_counter',
              style: Theme.of(context).textTheme.headline4,
            ),
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _incrementCounter,
        tooltip: 'Increment',
        child: Icon(Icons.add),
      ),
    );
  }
}
```

> 注：删除了注释

我们看到`build`方法下的`return`关键字后的代码

```dart
return Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      body: Center(
        // 此处省略部分代码
    );
```

__什么是`Scaffold`?__

> [官方文档](https://api.flutter-io.cn/flutter/material/Scaffold-class.html)

简单来说，Scaffold(脚手架)就是一个提供 Material Design 设计中基本布局的 widget

让我们再稍微深入一下

[![gcTk3F.png](https://z3.ax1x.com/2021/05/16/gcTk3F.png)](https://imgtu.com/i/gcTk3F)

其中第一个就是`AppBar`，也就是下图那个在最上方的那一条蓝色的条框

[![gcHiy4.png](https://z3.ax1x.com/2021/05/16/gcHiy4.png)](https://imgtu.com/i/gcHiy4)

> 没错这确实是Gtk程序

接下来我们再看看`AppBar`的源码

[![gcHr0s.png](https://z3.ax1x.com/2021/05/16/gcHr0s.png)](https://imgtu.com/i/gcHr0s)

这里我们只看它的`title`属性，其它的属性我们之后再学，然后让我们回到示例

```dart
appBar: AppBar(
        // Here we take the value from the MyHomePage object that was created by
        // the App.build method, and use it to set our appbar title.
        title: Text(widget.title),
      ),
```

没错就是设置一个标题而已😜

让我们继续，看到body部分

```dart
body: Center(
        // Center是一个布局小部件，它需要一个child，并将其放置在父组件的中心
        child: Column(
          // Column也是一个布局小部件。它会获取子对象列表并垂直排列它们。默认情况下，它会调整自身大小使其水平适应其子对象，并尝试与父对象一样高
          //
          //调用“debug painting”（在控制台中按“p”，在Android Studio中从flatter Inspector中选择“Toggle debug Paint”操作，VSCode中选择“Toggle debug Paint”命令）以查看每个小部件的线框
          //
          // Column有各种属性来控制它如何调整自身大小以及如何定位子组件。在这里，我们使用主轴对齐来垂直地使子对象居中；这里的主轴是垂直轴，因为Column是垂直的（横轴是水平的）
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text(
              'You have pushed the button this many times:',
            ),
            Text(
              '$_counter',
              style: Theme.of(context).textTheme.headline4,
            ),
          ],
        ),
      ),
```



---

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/88x31.png" /></a><br />本作品采用<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/">知识共享署名-非商业性使用-禁止演绎 4.0 国际许可协议</a>进行许可。