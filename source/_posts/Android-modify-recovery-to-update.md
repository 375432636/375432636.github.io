---
title: 安卓修改Recovery，获得刷机权限
date: 2019-04-10 13:52:15
tags:
categories: Android
---

# 1. Recovery.img 准备

## 1.1 获得Recovery

从其他开发者或者原版机器中得到

## 1.2 环境部署

- adb apt-get install abootimg

## 1.3 解包

- 解压出所有的Recovery

```bash
root@Ubuntu:/ 
abootimg -x recovery.img 
```

- 解压出initrd.img

```bash
root@Ubuntu:/ 
abootimg-unpack-initrd initrd.img
```

## 1.4 修改信息

- 找到对应recovery文件，文件位置为 ramdisk/sbin/recovery

- 使用IDApro对recovery文件进行反编译，[参考教程](http://www.oneplusbbs.com/thread-860851-1.html)

- 找到后使用IDApro或者Sublime进行修改

## 1.5 打包

- 修改ramdisk/, bootimg.cfg, zImage权限

```bash
root@Ubuntu:/ 
chmod 700 -R ramdisk/ bootimg.cfg zImage
```

- 打包ramdisk

```bash
root@Ubuntu:/ 
abootimg-pack-initrd new_initrd.img ramdisk/
chmod 700 -R new_initrd.img
```

- 打包recovery

```bash
root@Ubuntu:/ 
abootimg --create new_recovery.img -f bootimg.cfg -k zImage -r new_initrd.img
```

## 1.6 刷入recovery

将recovery拷贝到U盘，插入机顶盒，通过USB或TTL连接

```bash
root@Hi3798MV300:/ 
dd if=/mnt/sda/sda1/oldinitrd_recovery.img of=/dev/block/mmcblk0p3
```

# 2. 制作刷机包

## 2.1 部署加密工具获得

```bash
root@Ubuntu:/ 
git clone https://github.com/supersu097/apk_rom_signature_check_sign.git
./dersa -m
```

## 2.2 获得刷机包

从本机中提取或者和其他的

## 2.3 签名

```bash
root@Ubuntu:/ 
./dersa  -s ./certkey/releasekey update.zip
```

## 2.4 刷机

拷贝到U盘上，插入机顶盒，进入recovery刷机


