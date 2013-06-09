---
layout: post
title: "树莓派Raspbian系统初始配置"
category: OS
tags: [Raspbian, 树莓派]
---

树莓派已上手有一段时间了，现在来记录分享一下Raspbian的初始配置工作。

首次启动将出现系统初始配置的界面，这个界面在也可以在之后的终端窗口中通过sudo raspi-config激活。先来看一下各配置项的含义：

expand_rootfs – 将根分区扩展到整张SD卡，因为整个Image才400多兆，但是现在的SD卡基本都是几个G的，除非SD卡有其他用途，一般建议选择这项，这样可以有足够多的空间来安装各种程序。
overscan – 可以扩充或者缩小屏幕的设置，除非一启动就发现显示的内容能刚好填满整个电视的画面。
configure_keyboard  - 这个很重要，前面的屏幕选默认值：Generic 105-key (Intl) PC，但在Keyboard layout:时，显示出来的都是English（UK）的，要选择Other，然后在里面选择English（US），否则会出现键盘的一些符号不对或者对调，比如引号”和@符号对调，#号变成英镑符号等等。之后的两个屏幕都选择默认值就可以了，到了：Use Control+Alt+Backspace to terminate the X server? 时，选择Yes，表示用这个可以终止X Server，当整个X-Window死掉的时候可以用。
change_pass – 默认的用户名是pi，密码是raspberry，一般登录时不需要输入，但是用ssh远程连接时要用到这个用户名和密码，这里可以更改密码。

change_locale – 更改语言设置。在Locales to be generated: 中，选择en_US.UTF-8和zh_CN.UTF-8。在Default locale for the system environment:中，选择en_US.UTF-8（等启动完机器，装完中文字体，再改回zh_CN.UTF-8，否则第一次启动会出现方块）。
change_timezone – 更改时区，这个很重要，因为树莓派没有内部时钟，是通过网络获取的时间，如果设错时区，那么时间就不正确了，选择Asia – Shanghai，没错是Shanghai，木有Beijing，这是Unix的传统。缩写是CST，不知道是China Shanghai Time还是China Standard Time。
memory_split – 按照网上的说法，这个功能有Bug，会导致/boot/start.elf损坏使系统无法启动，所以不要使用这个功能。可以通过拷贝/boot/下的arm128_start.elf、arm192_start.elf、arm224_start.elf覆盖start.elf来实现显存和内存的划分。为了能播放高清1080p的视频，至少要分配64M显存给GPU。所以arm224就不能播放1080p高清视频。
ssh – 是否激活sshd服务，应该选择激活，这是当界面死掉后唯一进入机器的通道（如果Kernel没死的话），可以找另外一部机器，用putty或者其他ssh的工具连接到这部机器上，用pi这个用户登录，至少可以实现安全重启。
boot_behaviour – 设置启动时启动图形界面，正常肯定是Yes。
先说说我碰到过的问题，刚开始还以为系统刷了后可以直接用，忽略配置就startx进入图形界面用了，知道浏览中文网站时全是框框才开始找教程折腾。记得第一次进系统后还执行了更新系统命令，然后把SD看撑爆了，O(∩_∩)O~

仔细看过“攻略”后总结了一下配置步骤：

先配置列表中想要配置的项，值得注意的是 change_locale 项先不要改成zh-cn的，expand_rootfs项最好选择它，不然装软件或更新系统的时候碰到空间不足的问题，配置change_locale时是用空格键选择的，我之前都不知道而搞了好久。
执行  sudo apt-get install ttf-wqy-zenhei  命令安装文泉驿的开源中文字体，执行  sudo apt-get install scim-pinyin  安装拼音输入法。
重启后执行  sudo raspi-config  重新激活配置页面配置好change_locale信息。
修改源，我查了一下国内有两个源，大连那个学校的稍慢与清华大学的，当然我用的是南方电信网络，自己ping过后再选择速度快的。清华大学的源：http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/  把地址替换掉/etc/apt/sources.list里面原始的地址即可，记得保留后面那串字符。其他源地址在这里。
到这里基本就可以使用了，我看到网上有人觉得安装谷歌浏览器挺稀罕的，其实使用通过apt-get安装chromium即可，跟在Ubuntu中用命令装是一样的，不过用起来反应有点慢，还不如原生自带的轻量级浏览器Midori 好用，反正我是这么觉得的，呵呵