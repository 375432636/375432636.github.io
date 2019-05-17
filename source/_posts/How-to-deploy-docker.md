---
title: How to deploy docker
date: 2019-05-17 15:02:53
tags:
---

## 1. Background

One of our projects, we need develop on windows, and deploy in other docker. So we need install docker on our develop enviroment.

## 2. Insetall

### 2.1 Download 

The releases page is  https://github.com/boot2docker/windows-installer/releases

### 2.2 Install by GUI

## 3. Enviroment setting

### 3.1 Pull image

```
docker pull mysql
```

### 3.2 Start run a mysql container

```
docker run --name ly-mysql -e MYSQL_ROOT_PASSWORD=123456 -p 3306:3306 -d mysql
```

- name：给新创建的容器命名，此处命名为ly-mysql
- e：配置信息，此处配置mysql的root用户的登陆密码
- p：端口映射，此处映射主机3306端口到容器pwc-mysql的3306端口
- d：成功启动容器后输出容器的完整ID.
最后一个mysql指的是mysql镜像名字

### 3.3 Examine IP of docker and host

```
docker inspect --format '{{ .NetworkSettings.IPAddress }}' <container-ID> 
docker-machine ip
```


