---
title: Android 编译
categories: Android
tags:
    - Pixel
    - 谷歌
    - 编译
---

### 记录一次针对于 Redmi K40/Poco F3/Mi 11x的编译

### 1.准备阶段

> 24G的RAM的机器
>
>熟悉Linux sever操作系统 如Ubuntu Debian 等,尽量使用Lts系 系统
>
>足够的硬盘空间 推荐300G+
>
>全局且质量极高的科学上网
>
>至少不低于四核心的主流CPU
<!--more-->
### 2.源码拉取阶段

 更新源

    sudo apt update

安装 Git

    sudo apt install git

执行初始化环境脚本

    cd ~/ # 切换用户根目录
    git clone https://github.com/akhilnarang/scripts # 拉取环境脚本
    cd scripts # 切换到脚本文件夹
    ./setup/android_build_env.sh # 执行脚本

以像素体验为例子

    mkdir -p ~/bin # 创建文件夹存放 repo
    mkdir -p ~/android/pe # 创建文件夹存放源码

安装Curl

    curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo #下载repo 并存放于~/bin
    chmod a+x ~/bin/repo # 更改文件权限使其可执行

配置Git的用户名与邮箱 下载配额

    git config --global user.email "you@example.com" # 邮箱
    git config --global user.name "Your Name" # 用户名

初始化像素体验仓库

    cd ~/android/pe # 进入文件夹
    repo init -u https://github.com/PixelExperience/manifest -b branch_name # 设置分支仓库 branch_name 一般设置为 twelve (截止于2022/03/27最新)

拉取源码

    repo sync -c -j$(nproc --all) --force-sync --no-clone-bundle --no-tags

切换到源码目录

    cd ~/android/pe # 切换源码目录
    source build/envsetup.sh # 执行预编译环境脚本
    lunch aosp_$device-userdebug # 拉取设备依赖 $ 一般指你的设备型号

以Redmi K40/Poco F3/Mi 11x为例子

    ============================================
    PLATFORM_VERSION_CODENAME=REL
    PLATFORM_VERSION=12 # 构建 Android 版本
    CUSTOM_VERSION=PixelExperience_Plus_alioth-12.1-20220327-1405-UNOFFICIAL # 自定义构建版本 
    TARGET_PRODUCT=aosp_alioth # 构建设备的代号
    TARGET_BUILD_VARIANT=userdebug # 用户调试
    TARGET_BUILD_TYPE=release # 发布版本
    TARGET_ARCH=arm64
    TARGET_ARCH_VARIANT=armv8-a
    TARGET_CPU_VARIANT=generic
    TARGET_2ND_ARCH=arm
    TARGET_2ND_ARCH_VARIANT=armv8-a  
    TARGET_2ND_CPU_VARIANT=generic 
    HOST_ARCH=x86_64 
    HOST_2ND_ARCH=x86
    HOST_OS=linux
    HOST_OS_EXTRA=Linux-5.13.0-1017-azure-x86_64-Ubuntu-20.04.4-LTS # 构建此 Android 所用系统
    HOST_CROSS_OS=windows
    HOST_CROSS_ARCH=x86
    HOST_CROSS_2ND_ARCH=x86_64
    HOST_BUILD_TYPE=release
    BUILD_ID=SP2A.220305.013.A3 # Android Build号
    OUT_DIR=out # 输出目录
    PRODUCT_SOONG_NAMESPACES=hardware/google/interfaces hardware/google/pixel device/xiaomi/sm8250-common hardware/xiaomi hardware/qcom-caf/wlan vendor/qcom/opensource/usb/etc vendor/xiaomi/sm8250-common device/xiaomi/alioth vendor/xiaomi/alioth hardware/qcom-caf/sm8250 vendor/qcom/opensource/commonsys/display vendor/qcom/opensource/commonsys-intf/display vendor/qcom/opensource/display vendor/qcom/opensource/data-ipa-cfg-mgr vendor/qcom/opensource/dataservices packages/apps/Bluetooth hardware/nxp hardware/qcom-caf/common/fwk-detect
    ============================================

### 3.编译阶段

构建开始

    croot # 设置编译根目录
    mka bacon -j$(nproc --all) # 使用make全核编译

### 4.构建完成后的ROM位置

跳转到编译文件位置

    cd $OUT

### 5.清理阶段

清理依赖文件与ROM rec包(如果有)

    make clean

## 结束与额外补充

### 更新源码与二次编译

    repo sync # 此命令会检查源码更新与设备树更新

切换到**源码**目录后

    source build/envsetup.sh
构建

    croot # 更改 root 目录
    mka bacon -j$(nproc --all) # 使用make全核编译

清理缓存

    make clean

参考资料与文献
>[像素体验WiKi](https://wiki.pixelexperience.org/)
>
>[Android Build号](https://source.android.com/setup/start/build-numbers?hl=zh-cn)
