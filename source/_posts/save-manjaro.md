---
title: 拯救 manjaro
date: 2019-07-16 17:27:07
tags: [Manjaro, ArchLinux]
categories: 探索 / Explore
---

在昨晚的一次 `update` 并重启以后，`manjaro` 忽然黑屏，而我旁边只有一台手机。吓得本 Newbie 当场就在 Manjaro Forum 的 [Newbie Corner](https://forum.manjaro.org/c/newbies) 发了个[帖子](https://forum.manjaro.org/t/18-04-gnome-black-screen-with-only-underscore-after-update-no-tty/94876)。然而发完回应者寥寥（就一个），所提的解决方法也无济于事，于是只好抱着小手机想办法。

情况是这样的，在显示完系统选择界面，进入 Loading 环节时，屏幕上依次列出了四行信息

```text
Loading Linux 5.0-rt-x86_64 ...
Loading initial ramdisk ...
mount: /sys/firmware/efi/efivars: unknown filesystem # 注：本报错此前就有
Starting version 242.32-3-arch
```

然后屏幕就定格在了黑屏，乌漆抹黑，只有左上角有一个凝固的下划线。我本来以为是更新后的初始化，结果吃了个饭回来发现还是这样，当时就惊了。更严重的是，甚至无法通过 `Ctrl+Alt+Fx` 进入 `tty` 。强制关机吧。按下关机键这个下划线还闪了两下，调皮。

玩笑归玩笑，事情还是要解决。第一个问题是如何进去。如果当时我有 MacBook Pro 在旁边的话有个很方便的解决办法，那就是 [chroot](https://forum.manjaro.org/t/how-to-save-your-manjaro-installation-when-it-breaks/75) ，具体实现方法是制作一个 `Manjaro` 启动盘，在启动盘系统加载好后把原硬盘中的分区mount到系统，再用`chroot`偷天换月，然后你就可以在这个临时系统里对原系统做调整了。

但是没有，怎么办呢？我首先参考了[这个网页](https://www.ostechnix.com/restore-broken-arch-linux-previous-working-state/)，通过在 `grub` 文件中 `linux` 为首的一行行末插入

```bash
init=/bin/bash
```

从而混入了系统。

但这还远远没完，进来之后发现系统仅挂在了 `/` 一个挂载点，同时网络也无法链接，测试证明网卡也未加载。在多次试验后，我写了这么一个脚本，在每次进系统后自动完成一系列配置操作。

```bash
#!/bin/sh

# 挂载各分区
# lsblk -f # 显示分区情况
mount /dev/sdb3 /boot
mount /dev/sdb2 /boot/efi
mount /dev/sdb5 /home
mount /dev/sda1 /home/Downloads

# 配置网卡
# lspci -v | grep Ethernet -8 # 寻找网卡模块名称，Ethernet 下 Kernal Module 后面的就是了
modprobe e1000e # 这里我的 Module 是 e1000e
ip link # 查看网卡名，其中不带 LOOPBACK 的那个是对的
ip link set eth0 up # 启用网卡
dhcpcd eth0 # 自动分配地址，如果失败要先 killall dhcpcd
# ping www.baidu.com -c 5 # 这个界面不加 -c 居然 Ctrl+C 停不了，第一次配完又被迫重启了...
```

如此这般，看似简单，其实查了 N 个网页才查清楚上面一系列操作怎么完成。有人要说了，为什么要联网呢？因为是更新完出了错，首先要做的肯定是回滚更新。

```bash
cat /var/log/pacman.log | grep "2019-07-15" | grep -iE 'installed|upgraded|removed'
```

这样就能具体看到今天 `pacman` 安装、升级、移除的包。通过 `grep` 的小技巧可以轻松回滚。

回滚完了以后系统依然无法进入，怀疑是更新导致了系统关键文件错误。由于在一开始的界面是可以更换 `Linux` 内核尝试启动的，而我尝试过后并没有效果，所以最初就排除了内核错误。而实验室的核显电脑自然也不会是因为显卡黑屏（尽管如此我还是尝试了重装驱动，无效）。所以最后能做的只有一点点翻看系统日志了。

```bash
journalctl -x -b -1 | grep -iE 'fail|error|unable'
# -x for more information, -b -1 for the last boot
```

然后翻到这么两行

```log
Jul 15 22:53:25 manjaro /usr/lib/gdm-x-session[540]: /usr/lib/Xorg: error while loading shared libraries: libnettle.so.6: cannot open shared object file: No such file or directory
Jul 15 22:53:25 manjaro /usr/lib/gdm-x-session[540]: Unable to run X server
```

这其实就很明显了。`X server` 是 Gnome 等一堆桌面环境的基础，没运行起来肯定进不了图形界面，于是搜索解决办法。解决方案非常简单，重装 `nettle` 包就行了。重装后执行

```bash
exec /sbin/init
```

轻松进入图形界面，收工。

