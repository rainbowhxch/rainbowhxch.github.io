---
title: "让吃灰的raspberry Pi变成NAS"
date: 2021-12-25T00:54:24+08:00
tags: ["raspberry pi", "NAS", "openmediavault"]
draft: false
---

## 操作环境
- raspberry pi 4b
- 一个普通的SATA M2固态盘

## NAS选择
本文选择[openmediavault](https://www.openmediavault.org/)，当然也有其他选择，如[TrueNAS](https://www.truenas.com/)等。

## 安装
openmediavault是基于Debian Linux的NAS，但也可以作为一个Service跑在raspberry pi OS上。本文使用这种安装方式，其他安装方式参考[官方文档](https://openmediavault.readthedocs.io/en/5.x/installation/index.html)。

- 第一步：更新&升级包仓库
```bash
sudo apt update
sudo apt upgrade
```
- 第二步：使用官方安装脚本
```bash
wget -O - https://raw.githubusercontent.com/OpenMediaVault-Plugin-Developers/installScript/master/install | sudo bash
```
- 第三步：重启
```bash
sudo reboot
```

## 使用
openmediavault默认跑在80端口，直接浏览器访问raspberry pi的ip地址即可。
默认用户名为`admin`，密码为`openmediavault`。

之后就可以在`Services`中通过配置NFS和Samba(SMB)分别实现Windows与Linux下的文件共享

- 第一步：挂载磁盘

`Storage`->`File Systems`->选中磁盘->`Mount`

- 第二步：创建共享文件夹

`Access Rights Management`->`Shared Folders`->`Add`->一些选项自己斟酌->`Save`

- 第三步：开启SMB/CIFS

`Services`->`SMB/CIFS`->`Setting`->`Enable`->`Save`->`Shares`->`Create`->一些选项自己斟酌->`Save`

- 第四步：开启NFS

`Services`->`NFS`->`Setting`->`Enable`->`Save`->`Shares`->`Add`->一些选项自己斟酌->`Save`

- 第五步：看上边有个黄色条条

点`对勾`使更改的配置生效

-- TODO: Linux/Windows Client 配置 --

P.S. 登录后第一件事**记得改密码**

## Reference
1. [官方文档](https://openmediavault.readthedocs.io/en/5.x/index.html)
2. [一个安装教程](https://pimylifeup.com/raspberry-pi-openmediavault/)
