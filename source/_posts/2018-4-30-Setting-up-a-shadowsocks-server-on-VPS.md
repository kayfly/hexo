---
title: 通过VPS搭建VPN
date: 2018-04-30 19:46:49
categories: 计算机
tags: Linux

---
* 一，安装python
``` bash
 apt-get install python-pip3
```
* 二，安装shadowsocks
``` bash
 pip3 install shadowsocks
```
* 三，修改配置文件
``` bash
vi /etc/shadowsocks.json
```
 <!-- more --> 

* 单人连接
``` bash
 { "server":"你的服务器地址", 
  "server_port":设置一个未使用过的端口号, 
  "local_address":"127.0.0.1",
  "local_port":1080,
  "password":"客户端连接的密码",
  "timeout":300,
  "method":"aes-256-cfb",
  "fast_open":false }
```
* 多人连接
``` bash
 { "server":"0.0.0.0", #填入你的IP地址
 "local_address": "127.0.0.1",
 "local_port":1080,
 "port_password": 
{ "8381": "foobar1", #端口号，密码
 "8382": "foobar2",
 "8383": "foobar3",
 "8384": "foobar4" },
 "timeout":300,
 "method":"aes-256-cfb",
 "fast_open": false }
```
* 三，电脑/手机安装shadowsocks
> windows:
https://github.com/shadowsocks/shadowsocks-windows/releases 
Android：
https://github.com/shadowsocks/shadowsocks-android/releases 

* 五，后台启动Shadowsocs
>``` bash
>ssserver -c /etc/shadowsocks.json -d start
>```
```





* 六，shadowsocks2.8.2启动报undefined symbol: EVP_CIPHER_CTX_cleanup错误
> 1，vim编辑：
​``` bash
vim /usr/local/lib/python2.7/dist-packages/shadowsocks/crypto/openssl.py
（具体修改路径自定）
```
2，
将第52行libcrypto.EVP_CIPHER_CTX_cleanup.argtypes = (c_void_p,) 
改为libcrypto.EVP_CIPHER_CTX_reset.argtypes = (c_void_p,)
具体还有第111行，同样修改cleanup 为 reset。

具体错误参考：https://blog.csdn.net/blackfrog_unique/article/details/60320737
