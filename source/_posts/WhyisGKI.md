---
title: 什么是 GKI
categories: Android
tags:
    - Android
    - Kernel
    - GKI
---

## 直入主题: 什么是 GKI

GKI是 **通用内核映像** (Android common kernels)

### 它是的存在目的是什么？

GKI的存在目的是解决Android的碎片化,应商通过修改内核源代码并添加设备驱动程序，添加了对 SoC 和外围设备的支持。但是这些修改内容可能很多，以至于设备上运行的代码中有多达 50% 是树外代码（并非来自上游 Linux 和 AOSP 通用内核）。
设备内核由以下部分组成：

- 上游：来自 kernel.org 的 Linux 内核
- AOSP：AOSP 通用内核的其他 Android 专用补丁程序
- 供应商：供应商提供的 SoC 和外围设备支持以及优化补丁程序
- 原始设备制造商 (OEM)/设备：其他设备驱动程序和自定义项

Google的通用内核映像是解决Android碎片化问题的下一步

Google一直在努力减少Android的碎片化，因为有大量的OEM厂商希望定制他们的设备。这导致Android OS在各种设备上的更新速度缓慢。Google的项目如Project Treble和Project Mainline旨在简化更新。但是，尤其是在OEM使用的Linux内核周围，碎片化仍然存在。Google的解决方案是通用内核映像（GKI）。GKI的目标是隔离SoC供应商和OEM的定制，允许Google直接向用户推送内核更新。启动Android 12并运行Linux内核5.10.43或更高版本的设备将必须遵循与GKI相关的某些指导方针。Google Pixel 6系列是首款配备GKI的手机。Google的最终目标是到2023年减少Android设备上树外代码的“技术债务”。

### 核心目的

GKI（Generic Kernel Image，通用内核映像）的核心目的是将所有的OEM和SoC供应商的定制代码从核心内核中隔离出来，并将它们移到可加载的模块中，这些模块通常被称为"vendor modules"（供应商模块）。这样做的好处是，Google可以直接推送内核更新给终端用户，而不需要等待OEM或SoC供应商进行修改或定制。这大大简化了更新过程，提高了Android设备的安全性，并有助于减少Android的碎片化问题。

最终Android内核将会实现通用化,如X86一样通用而无需做出向后移植等更改。
GKI的目标就是实现Android内核的通用化，这与x86架构的通用内核思路相似。通过这种方式，设备制造商（OEM）和SoC供应商的特定定制和驱动程序被隔离在可加载的模块中，而不是直接集成到核心内核中。

这意味着，理论上，如果一个设备出厂时使用的是5.10版本的内核，未来当6.x版本的内核发布时，用户或制造商可以直接更新到这个新版本的内核，而不需要进行大量的定制工作。这大大简化了更新过程，使Android设备能够更快速、更容易地接收到内核更新，同时也提高了设备的安全性和性能。

### 技术原理

模块化设计：GKI采用了模块化的设计，将SoC供应商和OEM的定制代码从核心内核中隔离出来，并将它们移到可加载的模块中。这些模块被称为"vendor modules"（供应商模块）。

Kernel Module Interface (KMI)：KMI是GKI的关键组件，它定义了核心内核与供应商模块之间的稳定接口。这意味着，只要这些接口保持稳定，供应商模块就可以与新版本的核心内核无缝协作。

Android Common Kernel (ACK)：Google会从主线Linux内核分支出一个“Android Common Kernel”（ACK），并在其中添加一些Android特定的补丁。SoC供应商（如Qualcomm、MediaTek和Samsung）会从ACK分支出针对其特定SoC的内核，并可能添加一些额外的补丁。GKI的目标是使这些供应商的补丁尽可能地被隔离在供应商模块中，而不是直接集成到核心内核中。

更新机制：Google正在努力通过Play Store提供GKI更新，这意味着未来内核更新可以像应用程序更新一样直接通过Play Store进行。

规范和指导方针：为了确保设备制造商遵循GKI的原则，Google为Android 12和更高版本的设备制定了一系列规范和指导方针。

减少树外代码：GKI的另一个目标是减少所谓的"out-of-tree"代码，即那些不在主线Linux或AOSP通用内核中的代码。这样做可以简化合并上游更改的过程，并提高设备的安全性。

简单总结来说: GKI和Vendor 会以 KMI(内核模块接口)通讯实现解决碎片化的问题，在此项目完全实施的情况下,此时GKI内核将会通用化，所有的SOC与OEM代码将在Vendor,此时碎片化问题将解决。

Project Treble的作用：Project Treble是Google为解决Android碎片化问题而推出的一个项目。它通过将OS框架与供应商实现（如HALs和设备特定的Linux内核分支）分离，使得Android OEM更容易在最新的AOSP框架上重建其OS。

Project Mainline的目标：Project Mainline旨在简化Android组件的更新过程。Google通过Google Play远程推送关键OS组件的更新，无需等待OEM应用补丁。

### 其他内核相关

...等待补充,未完待续