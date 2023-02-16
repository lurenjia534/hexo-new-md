---
title: WSL命令小记
categories: WSL2
tags:
    - Windows
    - Linux
    - WSL
---

### Windows 10 常用 Wsl2 命令

     wsl --install
更新内核命令

    wsl --update
立即终止所有运行的分发及 WSL 2

    wsl --shutdown
列出已安装的Linux发行版
<!--more-->
    wsl --list
列出所有的可装Linux 列表

    wsl --list --online

### 解决关于WSL的网络问题

打开 Clash 或 V2rayNg 的 允许局域网选项与Http代理(Clash无需选择此项)

查看 Windows 10 任务管理器的网络界面会找到一个由Hy虚拟的网络,查看他的IPV4 地址

Ubuntu子系统可以使用命令查看DNS 地址来获取宿主机的IP 从而设置Proxy

    cat /etc/resolv.conf
在Wsl/Visual Studio Code的终端输入

    export ALL_PROXY="http://IP:port"
此时此代理在本终端生效.
