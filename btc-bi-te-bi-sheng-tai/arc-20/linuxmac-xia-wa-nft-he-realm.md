---
description: 以<atommap>为例，其他同理
---

# Linux/Mac下挖NFT和Realm

## mine atommap

1. 先将atommapzip文件下载下来进行解压

[https://github.com/Atombitworker/Atom-map/tree/main](https://github.com/Atombitworker/Atom-map/tree/main)

2. 进入下方网站索引检查选择的数字是否有效，如果跳出详细信息即代表已经被打。搜"\[number].atommap"

[https://atomicalmarket.com/explorer](https://atomicalmarket.com/explorer)&#x20;

接下来可以开挖了，两种挖取方式



### &#x20;Method1

@SatsXio @atomicalsmarket 这两个第三方生态网站，导入数字对应的文件，使用存放atom资产的地址或者新地址，Bitwork填写 ab编号



### &#x20;Method2:&#x20;

使用cmd, os= Linux/mac

```sh
# 1. 修改svg存放路径及编号及gas；
# 2. gas换算与satsbyte值大概是 1.71：1
# 比如链上当下gas38，那么satsbyte后面的数字写23即可

# 以挖 9069.atommap 为例
yarn cli mint-nft "../Atom-map-main/atommap_svg_final/
9069.atommap.svg" --satsbyte 25 --satsoutput 546 --bitworkc ab9069
```



## mine realm

1. 先进去查重

[https://www.satsx.io/atomicals](https://www.satsx.io/atomicals)

2. 替换 "name"、satsbyte、bitworkc

```
npm run cli mint-realm "kuma" --satsbyte 18 --bitworkc 547b
```
