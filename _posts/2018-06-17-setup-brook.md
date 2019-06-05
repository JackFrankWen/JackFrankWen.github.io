---
title: 在google icloud 搭建brook
categories:
  - Server
tags:
  - vpn
---

### 搭建步骤

I.申请安装一个vps服务器
II.部署VPS服务器 
III.安装客户端   


### 第一步

申请一个vps服务器

### 第二步
1.登录ssh　远程服务器

```
ssh root@ip
```
2.安装谷歌BBR加速

BBR 是一个由谷歌社区开发的 TCP拥塞控制技术，目前处于开发初期，但是前景很棒，大家可以持续关注，同时BBR是集成与Linux最新版本的内核中的。
需要了解查看https://github.com/google/bbr

方案一
蓝底窗口按TAB键选NO
选择重启 Y
这里会断开连接，大家可以关掉窗口再重新打开或几秒钟后在界面随便按几个字母 便会提示重新连接。

```
sudo -i
wget -N --no-check-certificate https://raw.githubusercontent.com/FunctionClub/YankeeBBR/master/bbr.sh && bash bbr.sh install
sudo -i
bash bbr.sh start
```


方案二 TCP-BBR加速方案 无需重启

```
sudo -i
wget --no-check-certificate https://github.com/iyuco/scripts/raw/master/bbr.sh
chmod +x bbr.sh
./bbr.sh
```
３.搭建brook服务端

```

wget -N --no-check-certificate https://softs.fun/Bash/brook.sh && chmod +x brook.sh && bash brook.sh
如果失效用这个
wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubi/doubi/master/brook.sh && chmod +x brook.sh && bash brook.sh
```
再出现这个界面以后需要输入 reboot 重启服务器。BBR 和 RBOOK 就全启动啦 回车后 关掉窗口即可
### 第三步
ubuntu
```
install brook
sudo snap install brook
brook client -l 127.0.0.1:1080 -i 127.0.0.1 -s server_address:port -p password
```

window
下载地址

```
https://github.com/txthinking/brook
```