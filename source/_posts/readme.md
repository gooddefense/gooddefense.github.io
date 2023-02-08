---
title: 个人博客搭建教程及避坑指南
date: 2023-02-09 01:06:46
tags: 
---
# 搭建一个个人博客
## 写在前面
    今天闲着没事干，玩了一下当下很火的CharGPT。CharGPT是一个智能聊天机器人程序，我体验了一下，基本上我问的问题，CharGPT都可以很准确的给到我答案，它也可以处理一下有难度的工作，比如写文章，写代码，处理文档等等。在这期间，我问了它一个问题，就是如何搭建个人博客，它给出的答案是用框架来搭建。我之前对这些框架的了解比较少，对这一类框架也比较好奇。为了满足自己的好奇心，我决定试一试这些博客框架。
[参考链接](https://blog.csdn.net/weixin_41160054/article/details/89531921?ops_request_misc=&request_id=&biz_id=102&utm_term=mac%E4%BD%BF%E7%94%A8hexo%E2%80%94%E2%80%94script&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-0-89531921.142^v73^insert_down1,201^v4^add_ask,239^v1^insert_chatgpt&spm=1018.2226.3001.4187)
## Hexo搭建
    我最后选择用hexo来搭建我的个人博客，至于为什么不用wordPress或者其他的，我只能说hexo打的字少，其他的字多我懒得打。

### 创建Github仓库
- 登录GitHub账号，如果没有的话就先注册一个
- 登录成功之后，进入到个人主页，点击Repositories,这一个页面就是仓库；点击右上角的New按钮可以进入创建仓库界面，自行填写相关参数就可以了

### 安装nvm(避坑)
    这里需要注意，先安装好nvm，再去安装nodejs
#### 原因
- nodejs如果使用官网提供的安装包安装的话，在安装hexo-cli时可能会出现报错
![引用自csdn](https://img-blog.csdnimg.cn/20190430205745353.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MTE2MDA1NA==,size_16,color_FFFFFF,t_70)
导致出现以上问题的原因是因为，我们没有权限将hexo写入到.npm-global里面

#### 开始安装
- 开始之前先确认node和npm都已经卸载完成
- 从github上获取nvm最新下载命令进行下载
[nvm github网址](https://github.com/nvm-sh/nvm)
```
    这里会碰到一个问题，在终端输入nvm最新的下载命令后，会提示报错信息。
    解决方案如下：
    1. 进入该网址： https://www.ipaddress.com/ 
    2. 查询拒绝访问的网址的IP地址，拉到最下面，复制下来
    3. 终端输入：sudo vim /etc/hosts
    4. 在文件最后输入：（IP地址）（网址）
    5. 保存文件后，重新执行最新下载命令即可
    6. 重新执行下载命令，可能会有连接超时的问题，多执行几次或者等网络好一点的时候再执行就可以解决
    7. 成功下载完成之后，终端可能会提示需要配置环境变量，这个时候只需要按照提示进行配置即可。
    8. 输入：nvm -v查看版本号，有显示说明安装成功
```
![](https://img-blog.csdnimg.cn/0db881b72f69436f9cab7390c608a152.png)
 

### 安装nodejs
- 在nvm安装完成的基础上，执行命令：
```
    nvm install node
```
等待完成即可
### 安装git
- 执行以下代码：
```
    npm install -g hexo-cli
    hexo init blog
```

### 