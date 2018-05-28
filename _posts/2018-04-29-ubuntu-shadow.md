---
title: ubuntu 使用shadowsocks
categories:
  - Ubuntu
tags:
  - Linux
---

### ubuntu 使用shadowsocks

方法1 
用PIP安装很简单，



```
sudo apt-get update
sudo apt-get install python-pip
sudo apt-get install python-setuptools m2crypto

```
接着安装shadowsocks

```
pip install shadowsocks
```

```
sudo apt install shadowsocks
```

安装好后，在本地我们要用到sslocal ，终端输入sslocal --help 可以查看帮助，像这样
通过帮助提示我们知道各个参数怎么配置，比如 sslocal -c 后面加上我们的json配置文件，或者像下面这样直接命令参数写上运行。
比如

```
sslocal -s 11.22.33.44 -p 50003 -k "123456" -l 1080 -t 600 -m aes-256-cfb

```

确定上面的配置文件没有问题，然后我们就可以在终端输入 sslocal -c /home/mudao/shadowsocks.json 回车运行。如果没有问题的话，下面会是这样…
```

{
    "server":"11.22.33.44",
    "server_port":50003,
    "local_port":1080,
    "password":"123456",
    "timeout":600,
    "method":"aes-256-cfb"
}

server  你服务端的IP
servier_port  你服务端的端口
local_port  本地端口，一般默认1080
passwd  ss服务端设置的密码
timeout  超时设置 和服务端一样
method  加密方法 和服务端一样
```
确定上面的配置文件没有问题，然后我们就可以在终端输入 sslocal -c /home/mudao/shadowsocks.json 回车运行。…

方法2
```

sudo add-apt-repository ppa:hzwhuang/ss-qt5
sudo apt-get update
sudo apt-get install shadowsocks-qt5
```

设置代理
安装插件
我们需要给chrome安装SwitchyOmega插件，但是没有代理之前是不能从谷歌商店安装这个插件的，但是我们可以从Github上直接下载最新版 https://github.com/FelisCatus/SwitchyOmega/releases/ （这个是chrome的）然后浏览器地址打开chrome://extensions/，将下载的插件托进去安装。