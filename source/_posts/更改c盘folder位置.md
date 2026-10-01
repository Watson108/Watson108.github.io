---
title: 更改c盘folder位置
date: 2026-10-01 00:00:00
tags:
  - 电脑技巧
  - C盘清理
---

## 更改c盘folder位置

因为c盘又满了，这次重新清理了一些空间出来。尽管有很多应用根本没有在c盘安装，但好像总有一些配置文件是在c盘下面的，于是用了下面的方法。

- 把对应的文件夹复制到目标地址，比如d盘。

- 更改原来的文件夹名字或者直接复制副本。

- 通过管理员模式进入powershell或者cmd，使用以下命令创建链接。

```powershell
 New-Item -ItemType Junction `
-Path 'source path' `
-Target 'target path'
```

注意这里我使用了Junction而不是SymbolicLink，这两者其实都可以，区别主要在于以下:

A junction points to a folder on a local drive. A symbolic link, usually called a symlink, is more flexible: it can point to a file or folder, including a network location.

| Capability | Junction | Symlink |
|---|---|---|
| Points to folders | Yes | Yes |
| Points to individual files | No | Yes |
| Redirects from C: to D: | Yes | Yes |
| Points to a network share | No | Yes |
| Command Prompt creation option | `mklink /J` | `mklink /D` for folders |

使用mklink语法如下
```cmd
mklink /J "source path" "target path"
```

for a simlink, 使用语法如下
```cmd
mklink /D "source path" "target path"
```

- 测试成功后，会发现原来的文件夹有了一个快捷方式的图标，表示它只是一个link。

- 删除或备份原文件夹即可。

**使用记录**：通过这种方式，我把Tencent在c盘roaming中的文件移动到了D盘

```powershell
New-Item -ItemType Junction `
 -Path 'C:\Users\tzy\AppData\Roaming\Tencent' `
 -Target 'D:\ProgramData\Tencent'
```