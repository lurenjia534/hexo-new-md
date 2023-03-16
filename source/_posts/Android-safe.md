---
title: Android 安全入门
categories: Andoird
tags:
  - BootLoader
  - Tee
  - StrongBox
  - SafetyNet
  - Play Integrity API
---

## 前言:Android 经常被人诟病不够安全,但是作为现代化系统有义务防止设备被数字取证.

### so...What is BootLoader?

> 引导加载程序是供应商专有的映像，负责在设备上启动内核。引导加载程序保护设备状态，并负责初始化可信执行环境 (TEE)并绑定其信任根。在将执行转移到内核之前，引导加载程序还会验证 boot 分区和 recovery 分区的完整性。

简而言之 BootLoader 会校验设备的 Kernel、Boot、Recovery 分区,来保证设备的完整性. 在这里我们不对 BL 的工作原理进行深度刨析,因为这偏离了本文的主要论点.

<!--more-->

### 为什么要解锁 BootLoader

> 虽然Android BootLoader可以保护设备不被篡改和提供更高的安全性，但其本身由于固有的校验机制而变得封闭。Android一直以来都是开源和自由的操作系统，因此一些用户可能会由于各种原因解锁BootLoader。但是，现在的代工厂商和[设备制造商](https://zh.wikipedia.org/zh-hk/%E4%BB%A3%E5%B7%A5%E7%94%9F%E4%BA%A7)为了保护自身利益和生态系统，会限制用户解锁BootLoader

### 什么是 Tee

> 可为 Android 提供可信执行环境 (TEE),在固有的 Android 安全硬件中实现,目的是抵御远程攻击.
> Google 提供了 [Trusty Tee](https://source.android.com/docs/security/features/trusty?hl=zh-cn#:~:text=Trusty%20is%20a%20secure%20Operating,run%20parallel%20to%20each%20other.)
> 其他 TEE 操作系统历来都是由第三方供应商以二进制 blob 的形式提供，或由内部开发。 对系统芯片 (SoC) 供应商和 OEM 来说，开发内部 TEE 系统或从第三方获取 TEE 许可的成本可能很高。 资金成本加上不可靠的第三方系统会导致 Android 生态系统不稳定。我们将 Trusty 作为一种可靠且免费的开源替代方案提供给合作伙伴，用于替代其可信执行环境。Trusty 可提供通过封闭源代码系统无法实现的透明性。

> Android 支持各种 TEE 实现，因此您并非只能使用 Trusty。每一种 TEE OS 都会通过一种独特的方式部署可信应用。对试图确保应用能够在所有 Android 设备上正常运行的可信应用开发者来说，这种不统一性可能是一个问题。 使用 Trusty 作为标准，可以帮助应用开发者轻松地创建和部署应用，而不用考虑有多个 TEE 系统的不统一性。借助 Trusty TEE，开发者和合作伙伴能够实现透明化、进行协作、检查代码并轻松地进行调试。可信应用的开发者可以集中利用各种常见的工具和 API，以降低引入安全漏洞的风险。 这些开发者可以确信自己能够开发应用并让此应用在多个设备上重复使用，而不需要进一步进行开发。

简而言之,为 Android App 提供受信任的执行环境而防止恶意的远程攻击,任何解锁 Bl 后损坏 TEE 和 DRM 等级的行为都是愚蠢的 OEM/ODM 的极端操作.

### 什么是 StrongBox

整个互联网关于 StrongBox 的任何消息都非常浅薄,我在这里以我自己的理解来讲,Android StrongBox 是下一代 Tee,他在设备专有安全硬件实现,抵御远程攻击和针对设备模块的硬件攻击(遂成,数字取证),StrongBox 似乎比我们想的安全,这里是[案例](https://twitter.com/EricLiu_USA/status/1599084759929745409)。
Android StrongBox 是基于 Trusted Execution Environment（TEE）的一种特定实现。
Android StrongBox 使用了 TEE 作为安全硬件模块，以提供可信的密钥存储和处理功能。在使用 StrongBox 时，密钥和加密数据都将被存储在安全硬件模块中，只有 TEE 才能够访问这些数据，以保证其安全性和保密性。应用程序可以通过 Keymaster API 使用 StrongBox 提供的安全硬件功能，来保护其敏感数据和加密密钥。

由于 StrongBox 基于 TEE 实现，因此它可以利用 TEE 提供的各种安全保护措施，例如内存保护、代码签名和加密，来保护设备上的敏感数据。这使得 StrongBox 成为 Android 设备上最安全的密钥保护解决方案之一。

### 什么是 SafetyNet

SafetyNet是一个由Google提供的安全服务，旨在帮助Android应用程序保护其用户免受安全威胁和恶意行为的攻击。SafetyNet可以检测设备是否已被Root、是否存在恶意软件、是否存在模拟器等等，从而帮助应用程序确认设备的安全性。

SafetyNet提供了两个主要的API：SafetyNet Attestation API和SafetyNet Verify Apps API。其中，SafetyNet Attestation API允许应用程序检查设备是否具有基于硬件的安全保护措施，并可以使用这些信息来评估设备的安全性。SafetyNet Verify Apps API允许应用程序检测设备上是否存在恶意软件，从而保护用户的隐私和安全。

SafetyNet通过使用多种技术来保证其可靠性和安全性。例如，SafetyNet可以检测设备的根状态、是否存在模拟器、是否有未受信任的应用程序或服务等等。此外，SafetyNet还可以使用硬件密钥保护（如TEE）来保护其API的安全性，以防止恶意应用程序攻击SafetyNet API。

...未完待续