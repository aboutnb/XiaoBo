---
title: CentOS安装、配置、自启nginx
tags:
  - Linux
categories: Linux
keywords: Linux
description: CentOS安装、配置、自启nginx
cover: "https://assets.aboutnb.com/blog/nginx.jpg"
comments: true
abbrlink: 8aff900b
sticky:
date:
---

### Nginx 简介

> &emsp;&emsp; Nginx (engine x) 是一个高性能的 HTTP 和反向代理 web 服务器 ，同时也提供了 IMAP/POP3/SMTP 服务。Nginx 是由伊戈尔·赛索耶夫为俄罗斯访问量第二的 Rambler.ru 站点（俄文：Рамблер）开发的，公开版本 1.19.6 发布于 2020 年 12 月 15 日。
> &emsp;&emsp; 其将源代码以类 BSD 许可证的形式发布，因它的稳定性、丰富的功能集、简单的配置文件和低系统资源的消耗而闻名。2022 年 01 月 25 日，nginx 1.21.6 发布。
> &emsp;&emsp; Nginx 是一款轻量级的 Web 服务器/反向代理服务器及电子邮件（IMAP/POP3）代理服务器，在 BSD-like 协议下发行。其特点是占有内存少，并发能力强，事实上 nginx 的并发能力在同类型的网页服务器中表现较好。

### Nginx 下载

> Nginx 官网：[http://nginx.org/en/download.html](http://nginx.org/en/download.html)

### 命令行下载

```bash
    # 进入www目录 根据个人习惯存放位置
    cd /usr/local/www/
    wget http://nginx.org/download/nginx-1.22.0.tar.gz
```

### Nginx 安装前准备

```bash
    # 安装依赖
    yum -y install make zlib zlib-devel gcc-c++ libtool  openssl openssl-devel
```

### 安装 PCRE 库

```bash
    # 可以选择自己安装包放置的路径
    cd /usr/local/www/
    wget http://downloads.sourceforge.net/project/pcre/pcre/8.35/pcre-8.35.tar.gz
    # 解压压缩包
    tar zxvf pcre-8.35.tar.gz
    # 进入解压目录
    cd pcre-8.35/
    ./configure
    # 安装
    make && make install
    # 查看 pcre 版本
    pcre-config --version
```

### Nginx 安装、启动

```bash
    cd /usr/local/www/
    #创建nginx安装目录
    mkdir nginx
    cd /usr/local/www/
    #解压
    tar zxvf nginx-1.22.0.tar.gz
    #进入解压文件夹
    cd nginx-1.22.0
    #简易配置(2选1)
    ./configure --prefix=/usr/local/www/nginx
    #指定配置（2选1）
    ./configure --prefix=/usr/local/www/nginx --with-http_stub_status_module --with-http_ssl_module --with-pcre=/usr/local/www/pcre-8.35
    make && make install
    # 进入nginx目录
    cd /usr/local/www/nginx/sbin/
    # 启动
    ./nginx

```

> Nginx启动成功
  
![启动成功](https://assets.aboutnb.com/blog/1681884253058.jpg)

### nginx.conf检查
    
```bash
    [root@XiaoBo ~]# ./nginx -t
    # 输出以下内容
    nginx: the configuration file /tools/nginx/conf/nginx.conf syntax is ok
    nginx: configuration file /tools/nginx/conf/nginx.conf test is successful
```
### Nginx设置自启
```bash
    # 进入系统服务脚本目录
    cd /usr/lib/systemd/system
    # 创建ngxin服务相关脚本
    touch nginx.service
```

> 编辑nginx.service文件 （根据自己安装目录进行修改）
> 内容如下：

``` bash
    [Unit]
    Description=nginx - web server
    After=network.target remote-fs.target nss-lookup.target

    [Service]
    Type=forking
    PIDFile=/usr/local/www/nginx/logs/nginx.pid
    ExecStartPre=/usr/local/www/nginx/sbin/nginx -t -c /usr/local/www/nginx/conf/nginx.conf
    ExecStart=/usr/local/www/nginx/sbin/nginx -c /usr/local/www/nginx/conf/nginx.conf
    ExecReload=/usr/local/www/nginx/sbin/nginx -s reload
    ExecStop=/usr/local/www/nginx/sbin/nginx -s stop
    ExecQuit=/usr/local/www/nginx/sbin/nginx -s quit
    PrivateTmp=true

    [Install]
    WantedBy=multi-user.target

```

### 重新加载系统服务
    
```bash
    systemctl daemon-reload
```

### 启动服务
    
```bash
    systemctl start nginx.service
```

### 开机启动
    
```bash
    systemctl enable nginx.service
```

### 查看系统服务状态
    
```bash
    systemctl status nginx.service
```


### Nginx 常用命令

```bash
    # 进入nginx目录 
    cd /usr/local/www/nginx/sbin/
    # 启动
    ./nginx
    # 查看进程
    ps -ef | grep nginx
    # 停止
    ./nginx -s stop
    # 重启
    ./nginx -s reopen
    # 强制停止
    ./nginx -s stop
    # 优雅停止 Nginx，在退出前完成已经接受的连接请求 
    ./nginx -s quit 
    # 重载配置文件
    ./nginx -s reload
    # 检查nginx.conf文件正确性
    ./nginx -t   
```
