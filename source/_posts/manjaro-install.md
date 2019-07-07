---
title: Manjaro 装机二三事
date: 2019-06-24 13:31:08
tags: [manjaro, linux, 装机]
categories: 探索 / Explore
---

作为当前 [DistroWatch](https://distrowatch.com/) 上排名第二的 Linux 发行版，基于 ArchLinux 的 Manjaro 在共享前者的 AUR 仓库，Wiki 及社区的同时，大大简化了 ArchLinux 的上手难度。他提供丰富的图形化界面选择，自动安装驱动，且拥有专用的软件仓库，是 Linux 初学者及进阶使用者的不二选择。

网上已经有很多的 Manjaro 装机报告了，我在此加以总结，并补充上我自己遇上的一些 bug 以及解决方案。

<!-- more -->

# Manjaro 的安装

### 镜像下载

- 下载地址：https://manjaro.org/download/
- 选择 Official（官方发行）目录下或 Community（社区发行）目录下的发行版均可
- 推荐初学者使用 GNOME 或 Deepin（简单易用），进阶使用者使用 KDE （美观）

### 启动盘制作工具

- macOS 推荐使用 [Etcher](https://www.balena.io/etcher/)

- Windows 推荐使用 [Rufus](https://rufus.ie/)

这两个都是一键配置，不像 UltraISO 有很多参数需要调。

### 安装过程

注意：双系统安装需要提前分区，请参考[这个网页](<https://blog.csdn.net/lj402159806/article/details/80218360>)。

一个小 Trick 是：如果你有双硬盘，建议将 `~/Downloads` 挂在机械硬盘上，然后利用 `ln -s` 建立软连接。例如，将 `Documents` 文件夹放在 `~/Downloads` 下，但通过 `ln -s` 连接到主文件夹中。这样，`Documents` 就不会占用固态硬盘的空间，而我们仍可以通过 `~/Documents` 直接访问该文件夹。

装机过程请参考[这个网页](https://zzycreate.github.io/2018/11/03/Manjaro的尝试/)。（很有缘，博客作者和我用的同一套 Hexo 主题，只是我调了颜色）

# Manjaro 系统配置

### 替换国内源

系统配置的第一步当然是配置软件源

在终端输入

```bash
sudo nano /etc/pacman.d/mirrorlist
```

在该文件顶端添加

```json
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinux/$repo/os/$arch
```

然后 `Ctrl+O` 写入，`Ctrl+X` 退出。

再次在终端输入

```bash
 sudo nano /etc/pacman.conf
```

在文件末端加上

```json
[archlinuxcn]
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch
```

同理保存退出

终端输入如下指令更新软件源：

```bash
sudo pacman -Syy && sudo pacman -S archlinuxcn-keyring
```

### 安装 `yay` 并配置

安装方式：终端输入如下代码

```bash
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
```

同样，将软件源修改为清华源提速：

```bash
yay --aururl "https://aur.tuna.tsinghua.edu.cn" --save
```

### 安装输入法

~~此处采用`fcitx + sogoupinyin` 的安装方案~~  

`sogoupinyin`实在是 bug 太多了，换用`fcitx + googlepinyin` 的安装方案

```bash
sudo pacman -S fcitx-im fcitx-configtool
sudo pacman -S fcitx-gtk2 fcitx-gtk3 fcitx-qt4 fcitx-qt5 
# 注：按照本次装机经验，GNOME下用到的是 fcitx-qt4
sudo pacman -S fcitx-googlepinyin fcitx-cloudpinyin
```

编辑 ~/.xprofile 和 /etc/profile，加入（两个文件都要加入）

```json
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=@im=fcitx
```

### 安装 Git 并配置 ssh

```bash
sudo pacman -S git
git config --global user.name <your_name>
git config --global user.email <your_email>
cd ~/.ssh
ssh-keygen -t rsa -C "<your_email>" # 然后回车两次，如果不需要 passphrase 的话
eval "$(ssh-agent -s)" # 后台启动 ssh-agent
ssh-add ~/.ssh/id-rsa
sudo pacman -S xclip
xclip -sel clip < ~/.ssh/id_rsa.pub # 此行指令将公钥复制到剪切板，粘贴到 Github 上添加即可
```



### 其他软件安装

#### 安装 Chrome 及 node.js

```bash
sudo pacman -S google-chrome nodejs npm
```

#### 安装截图软件 `deepin-screenshot`

```sh
sudo pacman -S deepin-screenshot
```

#### 安装 VSCode

```bash
sudo pacman -S visual-studio-code-bin
```

#### 安装 QQ，TIM 和 WeChat

```bash
sudo pacman -S deepin.com.qq.office
sudo pacman -S deepin.com.qq.im
sudo pacman -S electronic-wechat-git
```

#### 安装 福昕阅读器，网易云，smplayer，goldendict

```bash
yay -S foxitreader netease-cloud-music smplayer goldendict 
```

注意 `yay` 不要加 `sudo`

goldendict 需要手动添加词典，[下载地址](<https://github.com/skywind3000/ECDICT/wiki>)

##### （选装）Typora：一款轻便好用的 markdown 编辑器，支持所见即所得（我用这个写的博客）

```bash
yay -s typora
```

#### 安装字体

```bash
# 文泉驿
yay -S wqy-microhei-lite
yay -S wqy-bitmapfont 
yay -S wqy-zenhei
# Adobe 系列
yay -S adobe-source-han-sans-cn-fonts 
yay -S adobe-source-han-serif-cn-fonts 
yay -S noto-fonts-cjk
```

#### 安装 SS / SSR

##### SS 安装

```bash
sudo pacman -S shadowsocks-qt5
```

##### SSR 安装

```html
# GFW 导致直接 yay -S electron-ssr 会失效
# 请直接到此处下载 pacman 包
https://github.com/qingshuisiyuan/electron-ssr-backup/releases
# 如果 SSR 安装异常请先安装 gconf
```

### 其他配置

#### 配置快捷键

设置-设备-键盘-下划到最下方点击 `+` 号新建快捷键，自行设定即可，命令为要打开的软件名

#### 文件夹默认打开方式出错解决方法（例如默认文件夹打开方式变为VSCode）

设置-应用-移除相应误开软件的文件打开方式绑定