---
description: 如果不用现有的工具而喜欢自己折腾，可以学着配置。
---

# Linux/Mac配置环境和启动挖币

## Install and Run by cmd

```sh
# install env
mkdir atomicals && cd atomicals
git clone git@github.com:atomicals/atomicals-js.git
cd atomicals-js && npm install
npm run build
npm install -g yarnl
yarn install

# init wallet
yarn cli wallet-init
```

## Mine Token

```sh
# Mint Token, atom 为例
yarn cli mint-dft [token] [--satsbyte]
yarn cli mint-dft atom

# 查余额
npm run cli balances --all
# 查总量
npm run cli location atom

# 转移atom
npm run cli transfer-ft atom
```

### 2023.12 补充：CMD的环境配置与示例文档

linux/mac的参考我写的示例： [https://mirror.xyz/9110.eth/XjPO4LrdMXhy5tBUeQZueB95pHaTAdS2uFIfVeTo-DQ](https://mirror.xyz/9110.eth/XjPO4LrdMXhy5tBUeQZueB95pHaTAdS2uFIfVeTo-DQ)[ ](https://mirror.xyz/2066.eth/XjPO4LrdMXhy5tBUeQZueB95pHaTAdS2uFIfVeTo-DQ)

windows的参考E哥 @sslisen 的教程： [https://mirror.xyz/cyberscavenger.eth/rayhn9RT1VMUMo4Iios3g0A6G6AtZ-EXfQ8F\_kj8HhQ](https://mirror.xyz/cyberscavenger.eth/rayhn9RT1VMUMo4Iios3g0A6G6AtZ-EXfQ8F\_kj8HhQ)



###
