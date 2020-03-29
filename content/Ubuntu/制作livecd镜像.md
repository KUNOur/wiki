---
title: "制作LiveCD镜像"
date: 2020-03-20 23:21
tag: LiveCD
---

[TOC]

## 参考链接

+ [定制自己的ubuntu 镜像文件 （remastersys, respin, USB live CD)](https://www.cnblogs.com/sunshore/p/8823109.html "定制自己的ubuntu 镜像文件 （remastersys, respin, USB live CD)")

+ [如何制作ubuntu系统镜像](https://zhuanlan.zhihu.com/p/90022299 "如何制作ubuntu系统镜像")

+ [Systemback](https://launchpad.net/systemback "Systemback")

+ [解决systemback 无法生成超过4G的iso的问题](http://community.bwbot.org/topic/194/%E8%A7%A3%E5%86%B3systemback-%E6%97%A0%E6%B3%95%E7%94%9F%E6%88%90%E8%B6%85%E8%BF%874g%E7%9A%84iso%E7%9A%84%E9%97%AE%E9%A2%98 "解决systemback 无法生成超过4G的iso的问题")

+ [使用Systemback在Ubuntu18.04备份系统](https://blog.csdn.net/rechardchen123/article/details/90649208 "使用Systemback在Ubuntu18.04备份系统")

+ [10种linux下磁盘快照方式恢复系统](https://www.cnblogs.com/linuxprobe/p/5399144.html "10种linux下磁盘快照方式恢复系统")

+ [Ubuntu 使用 systemback 制作自定义系统镜像和系统备份](https://blog.csdn.net/ustccw/article/details/84310572 "Ubuntu 使用 systemback 制作自定义系统镜像和系统备份")

+ [Systemback – Restore Ubuntu Desktop and Server To Previous State](https://www.ostechnix.com/systemback-restore-ubuntu-desktop-and-server-to-previous-state/ "Systemback – Restore Ubuntu Desktop and Server To Previous State")

+ [使用 Systemback 制作个性化 Ubuntu 系统镜像](https://wiki.tianbot.com/doku.php?id=ubuntu:systemback "使用 Systemback 制作个性化 Ubuntu 系统镜像")

+ <del>[搬：ubuntu系统备份还原(迁移)到另外一台电脑上](https://blog.csdn.net/hunter___/article/details/89020194 "搬：ubuntu系统备份还原(迁移)到另外一台电脑上")</del>

## Ubuntu 16.04

``` bash
sudo add-apt-repository ppa:nemh/systemback
sudo apt-get update
sudo apt-get install systemback
```

## Ubuntu 18.04

``` bash
sudo add-apt-repository ppa:nemh/systemback
sudo add-apt-repository --remove ppa:nemh/systemback
sudo add-apt-repository "deb http://ppa.launchpad.net/nemh/systemback/ubuntu xenial main"
sudo apt-get update
sudo apt-get install systemback
```

## 使用Live system create

![systemback-1](../attach/systemback-1.jpg "systemback-1")

![systemback-2](../attach/systemback-2.jpg "systemback-2")

![systemback-3](../attach/systemback-3.jpg "systemback-3")

## 镜像大于4G无法直接通过systemback导出

### 解压 .sblive 文件

``` bash
mkdir sblive
tar -xf /home/systemback_live_2016-04-27.sblive -C sblive
```

### 命名 syslinux 至 isolinux

``` bash
mv sblive/syslinux/syslinux.cfg sblive/syslinux/isolinux.cfg
mv sblive/syslinux sblive/isolinux
```

### 安装 cdtools

``` bash
# aria2c -s 10 https://nchc.dl.sourceforge.net/project/cdrtools/alpha/cdrtools-3.02a07.tar.gz
wget https://nchc.dl.sourceforge.net/project/cdrtools/alpha/cdrtools-3.02a07.tar.gz
tar -xzvf cdrtools-3.02a07.tar.gz
cd cdrtools-3.02
make
sudo make install
```

### 生成 ISO 文件

``` bash
/opt/schily/bin/mkisofs -iso-level 3 -r -V sblive -cache-inodes -J -l -b isolinux/isolinux.bin -no-emul-boot -boot-load-size 4 -boot-info-table -c isolinux/boot.cat -o sblive.iso sblive
```
