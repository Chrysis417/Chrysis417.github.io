---
title: wsl2下的gitproxy设置
catalog: true
comments: true
indexing: true
header-img: ../../../../img/default.jpg
top: false
date: 2022-01-19 15:19:08
subtitle:
tags:
- wsl2
- git
- windows
categories:
- 环境配置
---
# Contents
众所周知，由于github服务器架设在国外，大陆用户访问以及使用git操作较为困难。本文提供windows下linux子系统wsl2的git proxy设置方法，加速使用代理访问github

萌新时期一个git clone能复制半年确实非常劝退


首先在powershell下使用命令
~~~
wsl -l -v
~~~
查看当前wsl版本。本文适用于wsl2。

由于wsl2一些实现上的原因，在开机的时候会随机分配一个ip地址，所以在wsl2上配置git proxy不能使用以下命令，而要将其中的本机地址127.0.0.1设置为wsl2的ip地址
~~~
git config --global https.proxy http://127.0.0.1:1080
git config --global https.proxy https://127.0.0.1:1080
~~~


在wsl2中使用命令
~~~
cat /etc/resolv.conf |grep "nameserver" |cut -f 2 -d " "
~~~
可以查询到当前wsl2的ip地址。所以可以使用如下脚本文件设置gitproxy

set_proxy.sh
~~~
host_ip=$(cat /etc/resolv.conf |grep "nameserver" |cut -f 2 -d " ")
http_port="10809"
git config --global http.proxy "http://$host_ip:$http_port"
git config --global https.proxy "http://$host_ip:$http_port"
~~~
运行.sh文件的时候host_ip后面会多一个空格，而在命令行中直接执行就不会，原因不明。留个坑以后填

其中http_port根据自己的梯子来设置，我的http port是10809，有的可能是1080

如果失效，尝试使用export引入环境变量

set_proxy1.sh
~~~
host_ip=$(cat /etc/resolv.conf |grep "nameserver" |cut -f 2 -d " ")
http_port="10809"
export http_proxy="http://$host_ip:$http_port"
export https_proxy="http://$host_ip:$http_port"
~~~

完成后可以在wsl2中输入
~~~
curl google.com
~~~
测试有没有连上
# 其他注意事项
如果设置后仍然没有生效，检查以下设置
> 梯子开没开
> &nbsp;
> 注意打开梯子的允许局域网连接
> &nbsp;
> (如果是win10)系统搜索“允许应用通过windows防火墙”,给梯子以及相关应用的局域网(专用网络)访问权限。当然最前面那个勾也打上

# 总结与反思
问技术问题一定要把运行环境以及自己所做过的操作写出来。
