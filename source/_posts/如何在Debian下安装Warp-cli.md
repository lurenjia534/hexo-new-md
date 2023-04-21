---
title: How to install warp-cli under debian
categories: Linux
tags:
    - Linux
    - Debian
    - Warp+
---

### 1.工欲善其事，必先利其器(前置环境)

`sudo apt update # 更新源`
`sudo apt install vim curl gnupg lsb-release wget # 安装基本常用apt 包`

### 按照 Cloudflare warp install for linux 安装

**下载公钥并导入**
```curl https://pkg.cloudflareclient.com/pubkey.gpg | sudo gpg --yes --dearmor --output /usr/share/keyrings/cloudflare-warp-archive-keyring.gpg```

**将Warp源导入apt list**
```echo "deb [arch=amd64 signed-by=/usr/share/keyrings/cloudflare-warp-archive-keyring.gpg] https://pkg.cloudflareclient.com/ $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/cloudflare-client.list```

必要时,请务必**参考文档[Cloudflare Warp for Linux wiki](https://developers.cloudflare.com/warp-client/get-started/linux/)**

### 2.欲求成功，先考工具之完善(确定前置环境完成)

**更新源 && 从apt 安装warp**
`sudo apt update`
`sudo apt install cloudflare-warp`
