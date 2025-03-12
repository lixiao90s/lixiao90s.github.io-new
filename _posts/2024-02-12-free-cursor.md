---
title: cursor白嫖
author: 晓
date: 2021-10-8 9:36:00 +0800
categories: [AI]
tags: [cursor,白嫖]
--- 

# Cursor 白嫖策略

## cursor-fake-machine 实现白嫖
这个插件可以改变Cursor的机器码，让它以为你在不同的电脑上登录，从而绕过额度限制。

1. 首先，需要下载`cursor-fake-machine`插件。

2. 下载好之后，打开Cursor，把插件文件直接拖到插件扩展区域就OK了！

3. 安装成功后，你会看到一个提示，告诉你安装完成了。接下来，就是见证奇迹的时刻！

4. 打开Cursor的设置（file->preference->cursor settings），找到“advanced->Manage”，然后进入官网，删除账号。

5. 删除账号后，回到Cursor，退出登录，确保你的账号已经彻底退出了。

6. 在Cursor中，按下快捷键`Ctrl+Shift+P`，然后输入“fake”，你会看到一个“Fake Cursor”的选项，点击它！

## cursor-fake-machine github地址

[cursor-fake-machine](https://github.com/bestK/cursor-fake-machine/releases/)

这个方案使用久了，发现有时候还是不能用，会被提示使用太多次，方案二可以接着白嫖

## 白嫖方案二

方案来自于 [toutiao](https://github.com/yuaotian/go-cursor-help)
1. 参照方案一 去官网删除账号
2. 在powershell 中执行
``` shell
irm https://raw.githubusercontent.com/yuaotian/go-cursor-help/master/scripts/install.ps1 | iex
```
3. 运行命令，等待安装完成，重启cursor