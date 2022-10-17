---
title: Linux下配置Clash科学上网、开机自启
date: 2020-01-22
tags:
- 科学上网
- clash
- Linux
- CentOs
categories: 
- 网络
- OpenSource
thumbnail: "cover.png" 
url: "clash"
---



Clash是一款基于规则的网络代理软件，可以自动根据域名、IP 所属地理位置、IP CIDR、端口等规则将数据包分流到不同节点。

通过在Linux服务器上配置Clash，可以解决服务器无法访问国外网站、拉取资源速度慢、推送项目失败等问题。

<!--more-->



## 项目目的

服务器低延迟访问国外网站，可正常拉取资源、推送项目等



## 配置步骤

#### 下载、解压安装包，并生成配置文件

下载对应系统、CPU架构的最新安装包，Linux CentOs 7一般选择clash_linux_amd64命名的最新安装包即可：

[Release](https://github.com/Dreamacro/clash/releases/)

由于服务器还未配置科学上网，无法通过以下方式直接将安装包下载到服务器

```
wget -O https://github.com/Dreamacro/clash/releases/download/v1.10.6/clash-linux-amd64-v3-v1.10.6.gz
```

因此，选择另一种方式：

1. 在本机直接下载服务器所需的clash安装包到`/Users/用户名/Downloads/`目录下

2. 通过scp命令将安装包远程复制到服务器`/usr/local/bin/`目录下 

   ```
   scp /Users/用户名/Downloads/clash-linux-amd64-v3-v1.10.6.gz 服务器用户名@服务器ip地址: /usr/local/bin/ 
   ```

3. 解压安装包到`/usr/local/bin/` 目录下，并删除安装包

   `````
   gzip -dc clash-linux-amd64-v3-v1.10.6.gz > /usr/local/bin/clash
   chmod +x /usr/local/bin/clash
   rm -f clash-linux-amd64-v3-v1.10.6.gz
   `````

4. 进入`/usr/local/bin/`目录并启动clash

   ```
   /.clash
   ```

   clash启动后会自动在`~/.config/clash`目录下生成配置文件

   ``````
   ls -la ~/.config/clash
   
   > -rw-r--r-- 1 root root   16 May 13 	23:11 config.yaml
   
   > -rw-r--r-- 1 root root 2548019 May 13 23:13 Country.mmdb
   ``````

5. 将`~/.config/clash`目录移动到`/etc`目录下

   ```
   sudo mv ~/.config/clash /etc
   ```

   

#### 配置代理

1. 导入订阅链接，**订阅链接前后要加英文双引号**

   ```
   wget -O /etc/clash/config.yaml "你的订阅链接"
   ```

2. 设置系统代理，创建配置文件`/etc/profile.d/proxy.sh`并写入以下内容：

   ```
   export http_proxy="127.0.0.1:7890"
   export https_proxy="127.0.0.1:7890"
   export no_proxy="localhost, 127.0.0.1"
   ```

3. 重载`/etc/profile`配置

   ```
   source /etc/profile
   ```

   

#### 配置开机自启

1. 创建`system`脚本并打开，文件路径为`/etc/systemd/system/clash.service`

```
touch /etc/systemd/system/clash.service
nano /etc/systemd/system/clash.service
```

2. 在`system`脚本中写入如下内容：

```
[Unit]
Description=clash daemon

[Service]
Type=simple
User=root
ExecStart=/usr/local/bin/clash -d /etc/clash/
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

3. 重载`systemctl daemon`

   ```
   systemctl daemon-reload
   ```

4. 启动clash并设为开机自启

   ```
   systemctl start clash
   systemctl enable clash
   ```

5. 测试clash配置是否成功

   ```
   [root@VM-20-8-centos ~]# curl google.com
   
   <HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
   <TITLE>301 Moved</TITLE></HEAD><BODY>
   <H1>301 Moved</H1>
   The document has moved
   <A HREF="http://www.google.com/">here</A>.
   </BODY></HTML>
   ```



#### 代理管理

- 如需关闭代理，可使用

  ```
  systemctl stop clash
  ```

- 如需查看clash日志，可使用

  ```
  journalctl -e -u clash
  ```

  
