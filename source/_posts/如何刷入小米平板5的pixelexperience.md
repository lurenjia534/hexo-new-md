---
title: 如何刷入小米平板5的Aosp ROM
categories: ROM
tags:
    - ROM
    - 小米
    - 小米平板5
---

## 先决条件

- 使用MIUI14 的固件或者MIUI 14 ROM
- 将所有应用程序，图片，视频，联系人等备份到云端或外部存储
- 最新的 [platform-tools](https://developer.android.com/tools/releases/platform-tools)
- 解锁引导加载程序和 [Arrow Recovery](https://sourceforge.net/projects/kubersharma001/files/nabu/ArrowOS-Recovery/)
<!--more-->
## 刷入 Arrow Recovery 恢复

确保您已重启进入 Fastboot 模式

### *Windows cmd 用户*

```bash
    fastboot -w # 这将会擦除并恢复设备上的所有数据分区
```

#### **从Windows cmd 刷入 boot.img 和 vendor_boot.img**

```bash
    fastboot flash boot boot.img # 刷入 boot.img
    fastboot flash vendor_boot vendor_boot.img # 刷入 vendor_boot.img
```

### *Powershell 用户*

```bash
    .\fastboot.exe -w #这将会擦除并恢复设备上的所有数据分区
```

#### **从Windows Powershell 刷入 boot.img 和 vendor_boot.img**

```bash
    .\fastboot.exe flash boot boot.img # 刷入 boot.img
    .\fastboot.exe flash vendor_boot vendor_boot.img # 刷入 vendor_boot.img
```

## 重启到 Arrow Recovery 恢复 并确定正确链接到 Recovery

*注意:小米Pad 5的恢复存在面板无法呈现UI的问题，但恢复工作正常.*

Windows cmd 用户

```bash
    fastboot reboot recovery # 告诉您的设备重启到恢复
```

Windows Powershell 用户

```bash
    .\fastboot.exe reboot recovery # 告诉您的设备重启到恢复
```

### 确定链接正常

Windows cmd 用户

```bash
    adb devices # 这应该显示您的设备链接
```

Windows Powershell 用户

```bash
    .\adb.exe devices # 这应该显示您的设备链接
```

## 刷入ROM

现在您已经成功刷入了 Recovery

### 现在重启到 sideload 模式

Windows cmd 用户

```bash
    adb reboot sideload # 这应该重启到sideload
```

Windows Powershell 用户

```bash
    .\adb.exe reboot sideload # 这应该重启到sideload接
```

### sideload ROM

Windows cmd 用户

```bash
    adb sideload romfile.zip # 通过sideload刷入ROM
```

Windows Powershell 用户

```bash
    .\adb.exe sideload romfile.zip # 通过sideload刷入ROM
```

### 清楚数据并重启,然后享受

Windows cmd 用户

```bash
    adb shell # 进入设备的shell模式
    recovery --wipe_data # 在shell模式擦除data
    adb reboot # 重启到系统
```

Windows Powershell 用户

```bash
    .\adb.exe shell # 通过sideload刷入ROM
    recovery --wipe_data # 在shell模式擦除data
    .\adb.exe reboot # 重启到系统
```
