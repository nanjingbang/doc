

layout: postname
title: 'Android组件化和插件化开发'
date: 2016-06-30 15:22:49
categories: 插件化
tags: [组件化,插件化,android]
keywords: "我是大黑，Android组件化和插件化开发"
---


# Android组件化和插件化开发
### 什么是组件化和插件化？

<!-- more -->

![组件化和插件化](https://raw.githubusercontent.com/halibobo/BlogImage/master/blog/module/module_plug.png)

**组件化开发**就是将一个app分成多个模块，每个模块都是一个组件（Module），开发的过程中我们可以让这些组件相互依赖或者单独调试部分组件等，但是最终发布的时候是将这些组件合并统一成一个apk，这就是组件化开发。
**插件化开发**和组件化开发略有不用，插件化开发时将整个app拆分成很多模块，这些模块包括一个宿主和多个插件，每个模块都是一个apk（组件化的每个模块是个lib），最终打包的时候将宿主apk和插件apk分开或者联合打包。


----------


## 组件化
#### 概述
android工程的组件一般分为两种，lib组件和application组件
**application组件**是指该组件本身就可以运行并打包成apk
**lib组件**是指该组件属于app的一部分，可以供其它组件使用但是本身不能打包成apk

#### 为什么要有组件化？
加入一个app工程只有一个组件，随着app业务的壮大模块越来越多，代码量超10万是很正常的，这个时候我们会遇到以下问题
-  稍微改动一个模块的一点代码都要编译整个工程，耗时耗力
-  公共资源、业务、模块混在一起耦合度太高 
-  不方便测试

#### 组件化正确的姿势
既然选择使用组件化，那么如何正确的使用它呢？这里给出一种解决方案，如果你有更好的方案，欢迎交流。
我们创建了一个app工程project，默认里面有一个app组件，这个app组件是可以直接运行的。
**怎么划分组件呢？**
- 1.新建一个lib组件，new Module--->Andorid Library，取名BaseUtilLib，我们将所有的公共的工具类、网络分装等类放在其中
- 2.新建一个lib组件，BaseReslLib，我们将所有的公共资源、drawable、String等类放在其中
- 3.将app按照自己的规则划分成多个模块，比如按业务按地区等都可以
- 4.逐一开发某个模块，比如Test模块，新建一个TestApp组件，TestApp组件引用[1][2]步骤的BaseUtilLib和BaseReslLib，在TestApp组件里添加并引用TestLib组件。在TestLib的activity中写代码写业务逻辑，TestApp只负责跳转和测试
- 5.将工程中的所有类似TestLib组件（不是TestApp组件）引入到工程的app中
看着有点乱，整理出一张图
![组件化开发](https://raw.githubusercontent.com/halibobo/BlogImage/master/blog/module/module.png)

这样的好处有

> 每个模块可以独立开发编译运行
> 开发单个模块时可以共享资源和工具类
> 可以针对单个模块测试


[demo地址：https://github.com/halibobo/ModuleBuild](https://github.com/halibobo/ModuleBuild)


----------
## 插件化
#### 为什么有插件化？
有了组件化，为什么还要用插件化呢？插件化开发总的来说有以下几点好处（不同插件框架不一样）：
- 宿主和插件分开编译
- 并发开发
- 动态更新插件
- 按需下载模块
- 方法数或变量数爆棚
 

#### 处境
开放出来的插件化开发框架比较多，他们各自都有自己的优势和和不足，实现的原理也有差别下面列

#### 开源的插件化框架
- [Qihoo360/DroidPlugin](https://github.com/Qihoo360/DroidPlugin)
- [CtripMobile/DynamicAPK](https://github.com/CtripMobile/DynamicAPK)
- [mmin18/AndroidDynamicLoader](https://github.com/mmin18/AndroidDynamicLoader)
- [singwhatiwanna/dynamic-load-apk](https://github.com/singwhatiwanna/dynamic-load-apk)
- [houkx/android-pluginmgr](https://github.com/houkx/android-pluginmgr)
- [bunnyblue/ACDD](https://github.com/bunnyblue/ACDD)
- [wequick/Small](https://github.com/wequick/Small)
- ......

目前开源的这几个框架有宿主和插件分离的也有融合在一起的，每个框架的详细介绍和demo在github里都可以查看到。插件化demo运行起来比较简单，但是真正将它用到实际项目中还是要考虑很多小细节的，目前我也正处于研究阶段。

**欢迎大家多交流**
