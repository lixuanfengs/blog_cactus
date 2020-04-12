---
title: frp搭建内网穿
date: 2020-04-12 15:42:28
tags: frp
categories: frp
toc: true
author: cactus
---

​	内网穿透技术众多，比如花生壳内网穿透、Ngrok、Frp 都是现在主流的内网穿透技术。
但我个人认为 Frp 是目前最好用配置最简单的。

<!-- more -->

- 花生壳
  配置简单方便，比较傻瓜化。但要收费。虽然也有免费版，但由于免费版的流量限制，基本上没有什么实际作用。
- Ngrok
  发布时间相对较长，对象较为成熟的一种内网穿透技术。但由于功能的强大。配置较为繁琐。
- Frp
  配置简单。并且适用于各大主流平台设备。

## 准备工作

* 需要一台有公网ip的云服务器（腾讯云、阿里云等）
* 在腾讯云或者是阿里云购买一个域名

由于 [frp官网]( https://github.com/fatedier/frp/blob/master/README_zh.md ) 说明文档比较详细，我这里就不在详细介绍了。

## 配置 frp 服务器

登录自己买的云服务器，在 https://github.com/fatedier/frp/releases 页面下载自己服务器对应版本 的 frp

```shell
wget https://github.com/fatedier/frp/releases/download/v0.32.1/frp_0.32.1_linux_amd64.tar.gz
```

使用 tar 指令解压 tar.gz 文件

```shell
tar -zxvf frp_0.32.1_linux_amd64.tar.gz
```

进入 frp 目录

```sehll
cd frp_0.32.1_linux_amd64
```

删除不必要的客户端文件

```shell
rm -f frpc frpc_full.ini frpc.ini
```

> 版本不同可能稍有差异。
>
> **frpc** 为客户端文件
>
> **frpc** 为客户端文件

配置服务器端文件

```
vim frps.ini
```

> **frps.ini** 为服务器配置文件

编辑配置文件

```shell
[common]
bind_port = 7000
vhost_http_port = 8080
dashboard_port = 7500
dashboard_user = 用户名
dashboard_pwd = 密码
max_pool_count = 5
authentication_timeout = 900

subdomain_host = www.wbqcactus.xyz

[ssh]
listen_port = 6000
auth_token = 和客服端 token 对应
```

> 简单解释：
>
> **[common]必填的**
>
> `bind_port` Frp 服务端口（可自定义）
> `vhost_http_port` http 访问端口（可自定义）
> `dashboard_port` dashboard 界面端口
> `dashboard_user` 登录 dashboard 用户名
> `dashboard_pwd` 登录 dashboard 密码
> `max_pool_count` 最大连接池数量
> `authentication_timeout` 超时验证时间
> `subdomain_host` 自定义二级域名
>
> **[ssh]**
>
> `listen_port` ssh 访问端口
> `auth_token` 用户身份认证
>
> **详细配置**
>
> [点击官方](https://github.com/fatedier/frp/blob/master/README_zh.md)

保存上面配置的文件，启动 frp 服务器

```shell
./frps -c ./frps.ini
```

> 用root用户启动

## 客户端配置

客户端就是需要映射到外网的设备，比如说：windows、Mac、linux等。

下载 frp ,删除服务端文件（和服务端配置基本相似）

```shell
wget https://github.com/fatedier/frp/releases/download/v0.32.1/frp_0.32.1_linux_amd64.tar.gz
tar -zxvf frp_0.32.1_linux_amd64.tar.gz
cd frp_0.32.1_linux_amd64
rm -f frps frps_full.ini frps.ini
```

编辑 frpc.ini 文件（客户端配置文件）

```shell
vim frpc.ini
```

编辑配置文件如下

```shell
[common]
server_addr = ip
server_port = 7000
auth_token = 和服务器端对应
pool_count = 1

[ssh]
type = tcp
local_ip = 局域网ip
local_port = 22
remote_port = 6000

[nas]
type = http
local_port = 5000
subdomain = nas

[web]
type = http
local_port = 80
subdomain = web
```

> 简单解释：
>
> **[common]必填的**
>
> `server_addr` 服务器端公网
> `server_port` frp 服务端口，和服务器端 `bind_port` 一致
> `auth_token` 和前面服务器端 `[ssh] auth_token` 一致
> `pool_count` 连接池数量
>
> 
>
> **[ssh]**
>
> `type` 服务类型（tcp、http、https、udp）
> `local_ip` NAS 本地局域网内网 ip
> `local_port` NAS 开启 ssh 服务端口号，默认 22
> `remote_port` 服务器端 ssh 端口，和服务器端 `[ssh] listen_port` 配置一致
>
> 
>
> **[web]web 服务，没有可以不用设置**
>
> `type = http` 类型为 http
> `local_port = 80` NAS web 服务端口
> `subdomain = web` 二级域名 web.lekee.cc
> **使用自定义二级域名的时候，域名 www.wbqcactus.xyz 要解析到服务器 IP**
>
> **详细配置**
>
> [点击官方](https://github.com/fatedier/frp/blob/master/README_zh.md)

保存，运行。

```shell
./frpc -c ./frpc.ini
```

此时在服务端会看到"start proxy sucess"字样，即连接成功。

### 测试运行

```shell
ssh -p 6000 user@服务器ip
```

## 后台运行

后台运行服务的方法有很多，这里只说一种可以在服务器端（Linux）和客户端都可以用的 `nohup指令`

```shell
nohup ./frps -c ./frps.ini &
```

## 客户端

```shell
nohup ./frpc -c ./frpc.ini &
```