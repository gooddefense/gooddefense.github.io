---
title: Maven
date: 2023-11-24 11:27:09
tags:
categories: 后端
---

# Maven

## Maven简介
Maven是一个项目管理工具。它可以帮助程序员构建工程，管理jar包，编译代码，完成测试，项目打包等等。

**maven的作用**
- 一键构建
    构建的过程：编译-测试-运行-打包-安装-部署等
- 依赖管理
    maven工程中不直接将jar包导入到工程中，而是有一个专门存放jar包的仓库，仓库中的每个jar包都有自己的坐标。maven工程中只要配置jar包坐标即可，运行项目需要使用jar包时，根据坐标即可从maven仓库中拿到jar包即可运行。


## 下载和配置Maven

### 下载
**[maven下载链接](https://maven.apache.org/download.cgi)**

**文件名后缀为bin.tar.gz**

### 配置maven_home环境变量
这里只写了mac的实例(windows的自行搜索)：
```Makefile
    
```


