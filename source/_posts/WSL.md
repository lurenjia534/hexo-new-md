---
title: Windows 10 配置 WSL
categories: WSL
tags:
    - Windwos
    - Linux
    - WSL
---

### 什么是 WSL1?

> 适用于 Linux 的 Windows 子系统 (WSL) 可让开发人员直接在 Windows 上按原样运行 GNU/Linux 环境（包括大多数命令行工具、实用工具和应用程序），且不会产生传统虚拟机或双启动设置开销。

### 什么是WSL2?

>WSL 2 是适用于 Linux 的 Windows 子系统体系结构的一个新版本，它支持适用于 Linux 的 Windows 子系统在 Windows 上运行 ELF64 Linux 二进制文件。 它的主要目标是提高文件系统性能，以及添加完全的系统调用兼容性。
><!--more-->
>这一新的体系结构改变了这些 Linux 二进制文件与Windows 和计算机硬件进行交互的方式，但仍然提供与 WSL 1（当前广泛可用的版本）中相同的用户体验。
>
>单个 Linux 分发版可以在 WSL 1 或 WSL 2 体系结构中运行。 每个分发版可随时升级或降级，并且你可以并行运行 WSL 1 和 WSL 2 分发版。 WSL 2 使用全新的体系结构，该体系结构受益于运行真正的 Linux 内核。

### WSL可以做什么

- 在 Microsoft Store 中选择你偏好的 GNU/Linux 分发版。
- 运行常用的命令行软件工具（例如 grep、sed、awk）或其他 ELF-64 二进制-文 件。
- 运行 Bash shell 脚本和 GNU/Linux 命令行应用程序，包括：
- 工具：vim、emacs、tmux
- 语言：NodeJS、Javascript、Python、Ruby、C/C++、C# 与 F#、Rust、Go等
- 服务：SSHD、MySQL、Apache、lighttpd、MongoDB、PostgreSQL。
- 使用自己的 GNU/Linux 分发包管理器安装其他软件。
- 使用类似于 Unix 的命令行 shell 调用 Windows 应用程序。
- 在 Windows 上调用 GNU/Linux 应用程序。

### Windows 10提供了一键安装命令 如无法一键安装，请参考下面的手动安装命令

自动安装命令

    wsl --install
然后重启并更新内核

    wsl --update
调整默认的非稳定Ubuntu为稳定20.04LTS版本

    wsl --install -d Ubuntu-20.04

### 手动安装必要条件

- 必须运行 Windows 10 版本 2004 及更高版本（内部版本 19041 及更高版本）或 Windows 11
- Windows 控制面板 - 程序和功能 - 启用或关闭Windows功能 - 适用于Linux的Windows子系统
- Windows 控制面板 - 程序和功能 - 启用或关闭Windows功能 - Hyper-V

### 手动安装流程

首先,列出所有的可安装Linux发行版

    wsl --list --online
以下是所有的可安装Linux发行版

    NAME            FRIENDLY NAME
    Ubuntu          Ubuntu
    Debian          Debian GNU/Linux
    kali-linux      Kali Linux Rolling
    openSUSE-42     openSUSE Leap 42
    SLES-12         SUSE Linux Enterprise Server v12
    Ubuntu-16.04    Ubuntu 16.04 LTS
    Ubuntu-18.04    Ubuntu 18.04 LTS
    Ubuntu-20.04    Ubuntu 20.04 LTS
安装指定的Linux发行版

    wsl --install --distribution <Distribution Name>
以 Ubuntu20.04LTS 为例子

    wsl --install --distribution Ubuntu-20.04
等待安装完成

查看正在运行WSL版本

    wsl -l -v
由于默认版本为WSL1

      NAME            STATE           VERSION
    * Ubuntu-20.04    Running         1
设置默认WSL版本的命令

    wsl --set-default-version <Version>
切换WSL版本命令

    wsl --set-version <distribution name> <versionNumber>
从WSL1切换WSL2切换时可能要求下载并安装更新

下载的更新的文件名应该是

    wsl_update_x64.msi
切换完成以后更新WSL

     wsl --update
下载更新完毕以后会要去关闭WSL

    wsl --shutdown
到此为止,手动安装流程结束

### 在 Visual Studio Code 使用 WSL2进行开发

安装 [Visual Studio Code](https://code.visualstudio.com/)

安装 [Remote - WSL](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl)

打开 [Windows Terminal](https://docs.microsoft.com/zh-cn/windows/terminal/) 的 [PowerShell](https://docs.microsoft.com/zh-cn/powershell/) 输入

    code .
此时会调起 Visual Studio Code 并链接你的 Ubuntu20.04LTS

### 解决关于WSL的网络问题

打开 Clash 或 V2rayNg 的 允许局域网选项与Http代理(Clash无需选择此项)

查看 Windows 10 任务管理器的网络界面会找到一个由Hy虚拟的网络,查看他的IPV4 地址

Ubuntu子系统可以使用命令查看DNS 地址来获取宿主机的IP 从而设置Proxy

    cat /etc/resolv.conf
在Wsl/Visual Studio Code的终端输入

    export ALL_PROXY="http://IP:port"
此时此代理在本终端生效

### 在 Wsl 上安装nvm并安装Node LTS版本

安装Curl

    sudo apt-get install curl
关闭 Windows Terminal 并重新打开，验证安装 nvm

    command -v nvm 
使用 nvm 安装 Nodejs 稳定LTS版本

    nvm install --lts
验证Nodejs版本

    node -v
验证Npm包管理器版本

    npm -v

### 参考资料与文献

>[Microsoft WSL文档](https://docs.microsoft.com/zh-cn/windows/wsl/about)
