---
title: 记linux安装C++依赖的问题
catalog: true
comments: true
indexing: true
header-img: ../../../../img/default.jpg
top: false
tocnum: true
date: 2022-01-28 16:30:38
subtitle:
tags:
- linux
categories:
- 环境配置
---
# 背景
回家后换回了游戏本作为开发环境，于是把当时在工作本上遇到的装环境问题(甚至还多出了没见过的问题)都再来一遍。。。

遂做此记录

vscode+wsl2(ubuntu20.04LTS)

## 引入万能头文件#include<bits/stdc++>
在wsl下安装gdb就自动引入了

## c++环境安装
~~~
sudo apt-get install gcc
sudo apt-get install gdb
sudo apt-get install g++
~~~
## clang编译器安装

~~~
sudo apt install clang-11 --install-suggests
~~~
clang12经常编译不通过但是clang11可以，所以就装clang11

工作本上一行命令搞定，游戏本上报错 bruh

~~~
Err:1 http://archive.ubuntu.com/ubuntu focal/universe amd64 fonts-stix all 1.1.1-4
  Connection failed [IP: 91.189.88.142 80]
E: Failed to fetch http://archive.ubuntu.com/ubuntu/pool/universe/f/fonts-stix/fonts-stix_1.1.1-4_all.deb  Connection failed [IP: 91.189.88.142 80]
E: Unable to fetch some archives, maybe run apt-get update or try with --fix-missing?
~~~

