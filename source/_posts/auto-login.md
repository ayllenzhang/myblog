---
title: SSH auto login with expect
date: 2019-07-07 13:00:35
tags: [Linux, Server]
categories: 探索 / Explore
mathjax: true
---

厌烦了每次 `ssh` 输入用户名与密码，不妨试试这个。

<escape><!-- more --></escape>

## 安装 expect

Manjaro

```bash
sudo pacman -S expect
```

OSX

```bash
brew install expect
```

## 编写脚本

在你期望保存的地方创建脚本（我的是`~/login`），粘贴以下内容

```bash
#!/usr/bin/expect

set timeout 30
spawn ssh <username>@<server IP address>
expect {
    "*yes/no" {send "yes\r";exp_continue} # 分号后不能加空格！
    "*password:" {send "<password>\r"}
}
expect "]*"   # 匹配任意提示信息，可换成 .*
# send "cd arzhang\r" # 进入服务器下的个人文件夹，可省略
# send "nvidia-smi" # 查看服务器 GPU 运行状况，可省略
interact
```

然后将 `<username>`, `<server IP address>` 和 `<password>` 替换为你对应的用户名，服务器 IP 和密码。

保存好后，运行如下指令以使得脚本变为可执行文件：

```bash
chmod +x <filename>
```

其中 `<filename>` 为脚本文件名。

最后，在脚本文件夹目录下使用 `./<filename>` 运行即可。

## 脚本语句解释

### spawn

`spawn` 指令用于根据其后的指令创建一个新的进程，其后的 `expect` 与 `send` 都是与其创建的进程进行交互。

### expect

`expect` 通常用来期待一个指令的相应反馈，正如其名。

`expect` 可以支持多分支语法，如下所示：

```bash
expect {
      "tea" {send "You ordered a cup of tea."; exp_continue}
      "coffee" {send "You ordered a cup of coffee."; exp_continue}
      "coke" {send "Sorry but we don't have coke."}
}
```

当输入 `tea` 或 `coffee` 时，输出对应字符串，同时继续运行此多分支语句；当输入 `coke` 时，输出对应字符串后循环结束。

`expect` 可以支持正则表达式。

### send

顾名思义，`send` 接受一个字符串参数并将其发送到进程。如有其他想在脚本中添加的指令，也可仿照已有 `send` 指令格式添加。

### interact

允许用户和 `spawn` 所创建的进程进行交互，即ssh登录后不会退出。

如需要登录执行指令后自行退出，可将最后一句 `interact` 改为

```bash
expect eof
```

## 不太相关的 Update

`hexo-renderer-marked@1.0.1` 更新后书名号放在行内引用里都不行了，我又不愿意以后都把尖括号换成`&lt; &gt;` 只好为这篇文章换了个renderer。

```bash
npm uninstall hexo-renderer-marked --save
npm install hexo-renderer-markdown-it --save
```

具体配置文件参考 [wiki](https://github.com/hexojs/hexo-renderer-markdown-it/wiki) 。
