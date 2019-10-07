---
title: 科学上网教程(包含谷歌访问助手，shadowsocks,ssh)
date: 2019-08-19 10:50:38
tags: 科学上网
---
# 1.谷歌访问助手：
我最先使用的就是谷歌访问助手
1.下载google chrome
2.下载谷歌访问助手,git@github.com:Emir-Liu/Google-Access-Helper.git
3.打开google chrome,点击三个小点，选择more tools->Extensions,进入了chrome://extensions/（当然也可以直接在地址栏输入，进行访问）
4.点击页面右上角打开Developer mode,点击Load unpacked,选择下载的谷歌访问助手解压包。
5.然后就会有12个小时的免费科学上网时间，永久免费只要按照其要求修改主页就可以了.

优点：
	1。免费不需要自己部署服务器，
	2。操作相对简单一点
缺点：
	2。无法访问Youtube之类网站。

# 2.shadowsocks:
	为了能够访问Youtube我选了这个。

优点：
	1。软件一直更新有保障，可以提issue
	2。可以自由访问网络
缺点：
	1。购买VPS,但是价格还是很便宜的我用的是vultr,主要可以需要的时候部署服务器，不用的时候就销毁了，价格在每个小时0。01USD,大概7分钱左右
	2。操作相对复杂
	3。有时候会出现奇怪的问题
	
## 2.1购买服务器
### 2.1.1购买网站以及要注意的
服务器IP
服务器账户
服务器密码

我这个是在客户端为Ubuntu，服务端为Ubuntu的环境下操作
### 2.1.2连接服务器
```bash
ping 服务器ip //检查是否可以连接
ssh 服务器账户@服务器IP//进行连接 连接后会让你输入服务器密码
```
### 2.2在服务器上搭建shadowsocks
### 2.2.1安装shadowsocks
```bash
apt-get update
apt install python-pip
apt install python-setuptools
pip install shadowsocks
vim shadowsocks.json//自己建立目录在目录下建立配置文件
{
        "server":"0.0.0.0",
        "server_port":服务器端口,
        "password":"密码",
        "method":"aes-256-cfb"//加密方式
}

ssserver -c /目录/shadowsock.json -d start
```
## 2.3在客户端搭建
### 2.3.1安装shadowsocks
```bash
apt-get install shadowsocks

vim shadowsocks.json//自己建立目录在目录下建立配置文件
{
        "server": "服务器IP",
        "server_port": 服务器端口,
        "local_address": "127.0.0.1",
        "local_port": "1080",
        "password": "密码",
        "method": "aes-256-cfb",//加密方式
        "timeout": 300,
        "fast_open": true
}
~
sudo -s//进入root
sslocal -c /目录/shadowsocks.json -d start
exit//退出root
```

# 3.ssh:
最后我觉得上面的方法太麻烦了，我发现一个最简单的方法。
优点：
	1。可以在网上到处浪没限制
	2。操作特别简单
	3。需要服务器，但是不需要配置服务器，
缺点：
	1。也需要一台服务器

服务器的购买和上面的一样

## 3.1 配置客户端
```bash
ssh -D root@66.42.66.21
//root是远程服务器的账户名，
//66.42.66.21时远程服务器的ip
//之后会要求你输入密码，这些根据你自己服务器的配置填写
```
