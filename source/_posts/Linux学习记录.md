---
title: Linux学习记录
date: 2021-03-08 22:54:11
index_img: https://resource.liangzai.online/resource/Linux.png
categories:
  - 计算机学习
tags:
  - Linux
---

## Linux基础知识
<!-- more -->
1. linux系统组成：内核、Shell、文件管理系统和应用程序。
    >内核：运行程序和管理磁盘和打印机等硬件设备的核心
    >Shell：是系统的用户界面，提供了用户与内核进行交互操作的一种接口，接受用户输入的命令并把它送入到内核中去执行。
    >文件系统：是文件存放在磁盘等存储设备上的组织方法
    >应用程序：程序集

2. linux发行版本
   * RedHat
   * Fedora（由Redhat发展而来）
   * Debian
   * Ubuntu（基于Debian）
   * Slackware
   * OpenSUSE

## Shell的基本运用

### Shell

1. Shell简介

    Shell是Linux的一个特殊程序，是内核与用户的接口，是命令语言、命令解释器及程序设计语言的统称。是一个命令语言解释器，拥有自己的Shell命令集，也能被系统中其他应用程序调用。

2. Shell终端

* Shell命令提示符

    ```bash
    [root@localhost ~]#   超级用户的命令提示符
    [name@localhost ~]$   普通用户name的命令提示符
    ```

    @之前的为已登陆的用户名，以后的为计算机的主机名，默认为localhost，其次为当前目录名。（~表示用户主目录）

* Shell命令格式

  命令名 [选项] [参数]

  * 命令名是描述该命令功能的英语单词或缩写；
  * 选项是执行该命令的限定参数或者功能参数,通常以'-'开头，当有多个选项时，可以只使用一个该符号。部分选项以'--'开头，这些选项通常是一个单词，还有少数命令的选项不需要'-'符号；
  * 参数是执行该命令所必须的对象，如文件、目录；
  * 在Shell中一行中可以键入多行命令，用';'分隔。在一行命令后加'\'表示另起一行继续输入。使用Tab键可以自动补全。
