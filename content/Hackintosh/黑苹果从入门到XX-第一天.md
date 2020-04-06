---
title: "黑苹果从入门到?-第一天"
date: 2020-04-06 10:52
tag: uefi,bios,dell dell venue 11 pro 7130,U大师
---

[TOC]

## 参考链接

+ [2020首发黑苹果 10.15.3 安装教程详细图文附资料](https://www.jianshu.com/p/c847b0dcbe11 "2020首发黑苹果 10.15.3 安装教程详细图文附资料")

+ [黑苹果macOS Sierra 10.12 安装教程(venue11 pro测试)](https://www.cnblogs.com/SemiconductorKING/p/6536888.html "黑苹果macOS Sierra 10.12 安装教程(venue11 pro测试)")

+ [【黑果小兵】macOS Mojave 10.14.6 18G87 正式版 with Clover 5050原版镜像[双EFI双平台终极版]](https://blog.daliansky.net/macOS-Mojave-10.14.6-18G87-Release-version-with-Clover-5033-original-image.html "【黑果小兵】macOS Mojave 10.14.6 18G87 正式版 with Clover 5050原版镜像[双EFI双平台终极版]")

+ [小李科技|神舟战神K610-i54210m d1安装黑苹果的经历](https://www.zxm5.com/436.html "小李科技|神舟战神K610-i54210m d1安装黑苹果的经历")

+ [macOS安装教程兼小米Pro安装过程记录](https://blog.daliansky.net/MacOS-installation-tutorial-XiaoMi-Pro-installation-process-records.html "macOS安装教程兼小米Pro安装过程记录")

+ [DELL VENUE 11 PRO系统损坏之后的解决办法](https://www.cnblogs.com/souther/p/4488336.html "DELL VENUE 11 PRO系统损坏之后的解决办法")

## 准备工作

+ 8G U盘 * 1，用来安装PE

+ 8G以上 U盘 * 1，用来安装macOs

+ HUB * 1 ,用来扩展鼠标、键盘和U盘

+ U大师 uefi版或者二合一版本，用来制作PE

+ <del>transmac 10.4，用来写入macOs镜像</del>

+ balenaEtcher 1.5.80，用来写入macOs镜像

+ 黑果小兵 macOS Mojave 10.14.6 18G87 镜像

## PE制作

打开`U大师-->U盘制作-->开始制作`即可

## macOs镜像制作

打开`balenaEtcher-->select image-->select target-->flash`即可

## 重新分配venue分区

venue默认会进原有的win10的启动器，所以首先进PE，将整个硬盘的原有分区全部删除。
> 在已有win10 uefi的情况下进PE,实测需要进venue的bios将boot设置为legacy启动才能进PE

## 安装macOs

直接插上写入macOs镜像的U盘，启动进入安装
> 安装过程出现8苹果花屏，目前的解决办法是发现在我下载到的Clover的config.plist文件中Graphics被注入了id(何为注入id，等以后深入学习后再来看),最后将Graphics的代码改成如下所示后系统安装可正常继续下去。

``` xml
    <key>Graphics</key>
    <dict>
        <key>EDID</key>
        <dict>
            <key>Inject</key>
            <false/>
        </dict>
        <key>Inject</key>
        <dict>
            <key>ATI</key>
            <false/>
            <key>Intel</key>
            <false/>
            <key>NVidia</key>
            <false/>
        </dict>
    </dict>
```

相关安装过程参照黑果小兵blog，此处就不重画轮子了。
