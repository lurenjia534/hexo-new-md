---
title: Android 玩机记录
categories: Android
tags:
    - Android
    - 谷歌
    - 技巧
---

## Android设备的小技巧

### [Android Magisk 面具](https://github.com/topjohnwu/Magisk)

> Android的神器
>
> Magisk是一套开放源代码的Android（5.0以上版本）自定义工具套组，内置了Magisk Manager（图形化管理界面）、Root、启动脚本、SElinux补丁和启动时认证/dm-verity/强制加密移除功能。Magisk同时提供了在无需修改系统文件的情况下更改/system或/vendor分区内容的接口，利用与Xposed类似的模块<!--more-->系统，开发者可以对系统进行修改或对所安装的软件功能进行修改等。
>
>除此之外，Magisk可以对其他验证系统完整性的应用程序进行隐藏（称为Magisk Hide），使得用户可在获取Root权限的情况下使用如向导宝可梦GO[1]、Fate/Grand Order[2]一类的应用程序或开启支付宝、微信的指纹支付功能[3]。
>
> [Github地址](https://github.com/topjohnwu/Magisk)
>
> [面具中文网](https://magiskcn.com/)

### [ReVanced](https://revanced.io/) # 注意:Vanced 失去了但是我们仍然拥有ReVanced

>YouTube Vanced已经死了，我们将永远珍惜它为平台上所有用户创造的简单性。尽管如此，我们不能坐等它的复兴，因为许多其他合适的替代品正在提供类似的功能，甚至可能提供更好的用户体验。最期待的Vanced替代品之一是YouTube ReVanced APK，官方替代品。虽然此应用程序仍处于初始阶段，但它提供了基本的YouTube Vanced功能和令人印象深刻的补丁，旨在维护Vanced的遗产。这篇文章将引导您完成您需要了解的有关YouTube复仇应用程序的所有信息。

>主要特点：
具有黑色主题的选项，以减少眼睛和电池疲劳。
阻止所有视频广告，并允许您在后台或画中画中播放视频（仅适用于Android 8.0及更高版本）
滑动控件允许您控制亮度和音量，就像在其他视频播放器应用程序（如VLC或MX播放器）（具有可配置的填充）中一样。
新的自动重复功能允许您欣赏tiktoks /vines等视频，或者只是继续循环播放歌曲。
不喜欢新的评论区或迷你游戏？这些也可以切换到与旧版本非常相似的平板电脑版本（尽管略有错误）。
>
>定制：
允许您覆盖编解码器选项，例如为旧设备或VP9强制H264，这也允许您强制HDR播放或关闭60fps（如果您更喜欢电影体验）。（这些功能的自定义设备配置可以在我们的discord或XDA上找到）
强制将默认视频分辨率设置为您想要的较高或最低，甚至覆盖屏幕分辨率，以便在任何设备上进行清晰的4k播放，并且还允许您将默认播放速度更改为0.25x到2x之间的任何位置（假设您的设备足够强大）
允许您切换家庭广告，大多数UI广告，商品广告，社区帖子，电影追加销售，紧凑的横幅信息（例如covid信息），完全删除评论，紧凑的电影，电影架删除等等！
>
>赞助商块
具有跳过烦人的赞助商细分（Youtuber在视频中间宣传服务或产品）的功能
它还支持跳过其他类别，例如介绍，outros和订阅提醒。
使用此处找到的 API。您可以找到有关其工作原理的更多信息
还允许您向API提交自己的细分，并为更广泛的社区做出贡献
完全控制是自动跳过细分类别还是显示用于跳过的按钮，或者只是根本不跳过它。
根据播放时间线中的类别，以特定颜色突出显示片段。
> [Github地址](https://github.com/YTVanced/VancedManager)
>
> [官网地址](https://vancedapp.com/)

### [LSPosed框架](https://github.com/LSPosed/LSPosed)

>Android 上目前最棒的XP框架依赖于 [Riru 25 +/ Zygisk](https://github.com/RikkaApps/Riru/releases) 和 [Magisk 面具](https://github.com/topjohnwu/Magisk)
>
>所有的现代化模块都应该迁移到 Zygisk！
>
>目前支持:安卓 8.1 ~ 14 DP1
>
>[TG群](https://t.me/LSPosed/145)
>
>[Github地址](https://github.com/LSPosed/LSPosed)

### [应用列表隐藏/Shamiko](https://github.com/LSPosed/LSPosed.github.io/releases)

>解决银行APP不能用就靠这个
>
>虽然“检测安装的应用是不正确的做法”，而且很蠢，但是并不是所有的插件类应用都提供了随机包名支持。这就意味着检测到安装了 root 类应用（如 Fake Location、存储重定向）与检测到了 root 本身区别不大。（会使用检测手段的 app 可不会认为你是在“我就蹭蹭不进去”）
与此同时，部分“不安分”的 app 会使用各种漏洞绕过系统权限来获取你的应用列表，从而对你建立用户画像（如陈叔叔将安装了 V2Ray 的用户分为一类），或是类似于某某校园某某乐跑的软件会要求你卸载作弊软件。
该模块提供了一些检测方式用于测试您是否成功地隐藏了某些特定的包名，如 Magisk/Edxposed Manager；同时可作为 Xposed 模块用于隐藏应用列表或特定应用，保护隐私。
>
> [Github地址](https://github.com/LSPosed/LSPosed.github.io/releases)
>

### [VipER4Android Fx](https://github.com/vipersaudio/viper4android_fx)

> 依赖于 [Magisk 面具](https://github.com/topjohnwu/Magisk)
>
> Android大名鼎鼎的音效软件，使用他来让你的耳朵怀孕吧
>
>[Github地址](https://github.com/vipersaudio/viper4android_fx)
