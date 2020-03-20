---
title: "终端配置(Win10)"
date: 2020-03-19 17:36
collection: 美化
---

[TOC]

## 参考资料

+ [Windows 安装和配置 WSL](https://www.jianshu.com/p/3e627ff45ccb "Windows 安装和配置 WSL")

+ [WSL 下的好终端 - wsltty](https://zhuanlan.zhihu.com/p/47743071 "WSL 下的好终端 - wsltty")

+ [babun安装，整合到cmder](https://www.cnblogs.com/hongdada/p/7989236.html "babun安装，整合到cmder")

+ [babun替换cygwin内核（最新的2.6.0或64位cygwin内核）](https://blog.csdn.net/mengyoufengyu/article/details/53142403 "babun替换cygwin内核（最新的2.6.0或64位cygwin内核）")

+ [zsh 启动速度慢的终极解决方案](https://zhuanlan.zhihu.com/p/98450570 "zsh 启动速度慢的终极解决方案")

+ [Cmder + Babun 打造 Windows 好用的终端工具](https://www.cnblogs.com/michael-xiang/p/10466074.html "Cmder + Babun 打造 Windows 好用的终端工具")

+ [Babun 配置 agnoster 主题](https://go2think.com/babun-theme/ "Babun 配置 agnoster 主题")

+ [Windows下最漂亮的Terminal Emulator是什么？](https://www.zhihu.com/question/37181941 "Windows下最漂亮的Terminal Emulator是什么？")

+ [安装ubuntu系统，报错WslRegisterDistribution failed with error: 0x8007019e](https://blog.csdn.net/qq_33033367/article/details/82820983 "安装ubuntu系统，报错WslRegisterDistribution failed with error: 0x8007019e")
## wsltty

Mintty as a terminal for WSL (Windows Subsystem for Linux)

### 与cmder集成 

``` bat
%LOCALAPPDATA%\wsltty\bin\mintty.exe --WSL=Ubuntu-18.04 --configdir=%APPDATA%\wsltty -~
```

![wsltty](../attach/wsltty.png "wsltty")

### 配置文件路径及内容

``` bat
%userprofile%\AppData\Roaming\wsltty\config
```

``` bat
# To use common configuration in %APPDATA%\mintty, simply remove this file
Font=MesloLGS NF
ClicksTargetApp=no
Scrollbar=none
FontWeight=400
FontHeight=12
CursorType=block
  
ForegroundColour=131, 148, 150
BackgroundColour=  0,  43,  54
CursorColour=    220,  50,  47

Black=             7,  54,  66
BoldBlack=         0,  43,  54
Red=             220,  50,  47
BoldRed=         203,  75,  22
Green=           133, 153,   0
BoldGreen=        88, 110, 117
Yellow=          181, 137,   0
BoldYellow=      101, 123, 131
Blue=             38, 139, 210
BoldBlue=        131, 148, 150
Magenta=         211,  54, 130
BoldMagenta=     108, 113, 196
Cyan=             42, 161, 152
BoldCyan=        147, 161, 161
White=           238, 232, 213
BoldWhite=       253, 246, 227
```

[传送门](https://github.com/mintty/wsltty "传送门")

## wsl(Windows Subsystem for Linux)

``` bat
# win+x，选择Windows PowerShell（管理员）输入
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

在普通cmd中启动

``` bat
ubuntu1804
```

## cmder

[传送门](https://cmder.net/ "传送门")

## <del>babun</del>

[传送门](http://babun.github.io/ "传送门")

### <del>替换cygwin为64位</del>

<del>[传送门](https://github.com/babun/babun/wiki/64-bit "传送门" )</del>

<del>终端被[BLODA](https://cygwin.com/acronyms/ "BLODA")影响严重，弃用babun</del>

## zsh

``` bash
sudo apt-get install zsh
```

``` bash
# 将用户的shell设置为/usr/bin/zsh
vim /etc/passwd
```

## powerlevel 10k

[传送门](https://github.com/romkatv/powerlevel10k "传送门")

```bash
vim ~/.zshrc
```

``` bash
# Add zinit ice depth=1; zinit light romkatv/powerlevel10k to ~/.zshrc
zinit ice depth=1; zinit light romkatv/powerlevel10k
```

### 字体安装

+ [MesloLGS NF Regular.ttf](https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Regular.ttf "MesloLGS NF Regular.ttf")

+ [MesloLGS NF Bold.ttf](https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Bold.ttf "MesloLGS NF Bold.ttf")

+ [MesloLGS NF Italic.ttf](https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Italic.ttf "MesloLGS NF Italic.ttf")

+ [MesloLGS NF Bold Italic.ttf](https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Bold%20Italic.ttf "MesloLGS NF Bold Italic.ttf")

## zinit

[传送门](https://github.com/zdharma/zinit "传送门")

``` bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/zdharma/zinit/master/doc/install.sh)"
```

``` bash
vim ~/.zshrc

# 添加如下插件
zplugin light zsh-users/zsh-autosuggestions
zplugin light zdharma/fast-syntax-highlighting
zplugin snippet OMZ::lib/clipboard.zsh
zplugin snippet OMZ::lib/completion.zsh
zplugin snippet OMZ::lib/history.zsh
zplugin snippet OMZ::lib/key-bindings.zsh
zplugin snippet OMZ::lib/git.zsh
```
