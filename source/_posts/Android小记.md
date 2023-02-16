---
title: Android 小记
categories: Android
tags:
    - Pixel
    - 谷歌
    - 编译
---

### 各系统的Adb与fastboot工具下载地址

[Google Adb For Fastboot Download](https://developer.android.com/studio/releases/platform-tools)

### Adb常用命令

查看USB调试打开下的Adb链接设备
<!--more-->
    adb devices
重启系统或重启到Rec和Fastboot

    adb reboot 
    adb reboot recovery
    adb reboot fastboot

### Fastboot常用刷写命令

fastboot刷写recovery命令

针对于非A/B分区设备刷些recovery,一般此类设备为老设备

    fastboot flash recovery recovery.img
针对于较为新的A/B分区设备

    fastboot flash boot recovery.img
fastboot 刷写Boot.img. 一般用于Magisk boot修补获取Root

    fastboot flash boot boot.img
查看fastboot链接设备

    fastboot devices
fastboot 重启或重启到Rec Fastboot

    fastboot reboot
    fastboot reboot recovery
