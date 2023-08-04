---
title: PicGo图床搭建
date: 2023-04-24 17:09:15
tags:
categories: 编程语言及工具笔记
---

# 三分钟搭建PicGo图床
参考链接：[跳转至Bilibili](https://www.bilibili.com/video/BV1Ui4y1x7Cq/?spm_id_from=333.337.search-card.all.click)

原本是打算使用Gitee作为图床仓库的，但是gitee对图床仓库做了限制，最后还是选择Github作为仓库。

当然，除了Github，也可以选择其他的方式做图床仓库。（建议百度）**（已修改，详情见细下文）**


 ## Github
 ***建议科学上网，否则网速真的很慢***
1. 登录Github账号，点击右上角的+号
![截图](https://raw.githubusercontent.com/gooddefense/picture_bed/main/%E6%88%AA%E5%B1%8F2023-04-24%2019.47.25.png)
2. 在加号的下拉列表中，选择**New repository**--创建新仓库
![创建新仓库](https://raw.githubusercontent.com/gooddefense/picture_bed/main/%E6%88%AA%E5%B1%8F2023-04-24%2019.51.30.png)
3. 进入创建新仓库列表，输入新仓库的名字，剩下的按照下图配置即可，点击Create repository
![配置新仓库](https://raw.githubusercontent.com/gooddefense/picture_bed/main/%E6%88%AA%E5%B1%8F2023-04-24%2019.53.48.png)

***做完以上步骤，先下载PicGo，获取密钥可以在下载PicGo之后进行***

 ## PicGo
 ***还是建议科学上网，下载速度会快很多***

 建议直接去官方下载链接下载，根据自己电脑的系统选择对应的安装包：[官方下载链接 ](https://github.com/Molunerfinn/PicGo/releases)

### 下载时碰到的问题和解决办法
在使用macbook安装PicGo时，安装完成后点击启动台的PicGo图标后，显示文件损坏，无法打开。
报错信息：
```
PicGo已损坏，无法打开。 您应该将它移到废纸篓。
```

**解决办法：**
在终端输入命令（注意最后有一个空格）：
```shell
sudo xattr -r -d com.apple.quarantine 
```
***先不要按回车！(重要的事情说三遍)***
打开 “访达”（Finder）进入 “应用程序” 目录，找到软件图标，将图标拖到刚才的终端窗口里面，会得到如下结果：
```shell
sudo xattr -r -d com.apple.quarantine /Applications/WebStrom.app
```
回到终端窗口按回车，输入系统密码回车即可正常使用

### 设置PicGo
 下载完成之后，进入界面，选择图床设置->Github
 ![图床设置](https://raw.githubusercontent.com/gooddefense/picture_bed/main/%E6%88%AA%E5%B1%8F2023-04-24%2020.03.57.png)

 设定仓库按照上图所示填写：**用户名/仓库名**
 分支名填main或者master都可以
 token：从Github上获取

 ***这里如何获取token？***
 1. 点击用户头像，点击下拉列表的Settings-设置选项
 ![xx](https://raw.githubusercontent.com/gooddefense/picture_bed/main/%E6%88%AA%E5%B1%8F2023-04-24%2020.07.30.png) 
 2. 点击左边列表的Developer settings
 ![](https://raw.githubusercontent.com/gooddefense/picture_bed/main/%E6%88%AA%E5%B1%8F2023-04-24%2020.09.16.png)
 3. 点击Personal access tokens->Tokens(classic)
 ![](https://raw.githubusercontent.com/gooddefense/picture_bed/main/%E6%88%AA%E5%B1%8F2023-04-24%2020.11.19.png)
 4. 点击Generate new token
 ![](https://raw.githubusercontent.com/gooddefense/picture_bed/main/%E6%88%AA%E5%B1%8F2023-04-24%2020.13.19.png)
 5. 输入Note，Select scopes选择repo即可,点击Generate token,即可生成token
 ![](https://raw.githubusercontent.com/gooddefense/picture_bed/main/%E6%88%AA%E5%B1%8F2023-04-24%2020.15.26.png)
 6. 将生成的token复制粘贴到PicGo上，点击确认，即可开始使用图床


### 测试结果
**Github仓库截图：**
![Github仓库截图](https://raw.githubusercontent.com/gooddefense/picture_bed/main/%E6%88%AA%E5%B1%8F2023-04-24%2020.19.01.png)

**markdown截图：**
![](https://raw.githubusercontent.com/gooddefense/picture_bed/main/%E6%88%AA%E5%B1%8F2023-04-24%2020.20.26.png)

***这样子，一个使用方便的图床就搭建好了！***

## 别的方式