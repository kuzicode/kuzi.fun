---
description: 系统环境：Linux Ubuntu 22.04
---

# 20240911：Linux跑CAT Protocol

### 一. 环境部署

```shell
sudo apt update && apt upgrade -y
sudo apt install docker.io -y

VERSION=$(curl --silent https://api.github.com/repos/docker/compose/releases/latest | grep -Po '"tag_name": "\K.*\d')
DESTINATION=/usr/local/bin/docker-compose

sudo curl -L https://github.com/docker/compose/releases/download/${VERSION}/docker-compose-$(uname -s)-$(uname -m) -o $DESTINATION
sudo chmod 755 $DESTINATION

sudo apt install npm -y
sudo npm install n -g
sudo n stable
sudo npm i -g yarn
```

### 二. 拉取代码并编译

```shell
git clone https://github.com/CATProtocol/cat-token-box
cd cat-token-box
sudo yarn install && sudo yarn build
```

### 三. 用 Docker 来运行

1. Run Fractal Node

```shell
cd $HOME/cat-token-box/packages/tracker/
sudo chmod 777 docker/data
sudo chmod 777 docker/pgdata
sudo docker-compose up -d
```

2. Run CAT Protocol Local Index

```shell
cd $HOME/cat-token-box/
sudo docker build -t tracker:latest .
sudo docker run -d --name tracker --add-host="host.docker.internal:host-gateway" -e DATABASE_HOST="host.docker.internal" -e RPC_HOST="host.docker.internal" -p 3000:3000 tracker:latest
```

### 四. Update 配置文件

```shell
cd $HOME/cat-token-box/packages/cli/
vim config.json

# 更新 `Config.json` 配置 (修改 username 和 password 且和 tracker/.env 的一样):
{
  "network": "fractal-mainnet",
  "tracker": "http://127.0.0.1:3000",
  "dataDir": ".",
  "maxFeeRate": 30,
  "rpc": {
      "url": "http://127.0.0.1:8332",
      "username": "bitcoin",
      "password": "opcatAwesome"
  }
}
```

### 五. Run cli cmd

```shell
# Wallet的创建、地址查看
sudo yarn cli wallet create
sudo yarn cli wallet address

# 这一步要先等节点同步完成才能看到效果
# 给地址转入 $FB，单次Mint
# 看链上 gas 并对应 `--fee-rate` 后的数值： https://explorer.unisat.io/fractal-mainnet/block
sudo yarn cli mint -i 45ee725c2c5993b3e4d308842d87e973bf1951f5f7a804b21e4dd964ecd12d6b_0 5 --fee-rate 100

# 查看到账情况
sudo yarn cli wallet balances
```

循环脚本：指定gas，30秒mint一次。

```sh
cd $HOME/cat-token-box/packages/cli/
vim auto-run.sh
```

编辑内容并保存退出：

```shell
#!/bin/bash

command="sudo yarn cli mint -i 45ee725c2c5993b3e4d308842d87e973bf1951f5f7a804b21e4dd964ecd12d6b_0 5 --fee-rate 100"

while true; do
    $command

    if [ $? -ne 0 ]; then
        echo "Run fail, EXIT."
        exit 1
    fi

    sleep 30
done
```

给脚本添加运行权限并跑起来：

```sh
chmod +x auto-run.sh
./auto-run.sh

# 放后台跑
nohup ./auto-run.sh > run.log 2>&1 &
# 查看日志
tail -f -n 100 run.log
```



