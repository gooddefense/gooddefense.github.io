---
title: 个人博客搭建教程及避坑指南
date: 2023-02-09 01:06:46
tags: 
categories: Hexo
---
# 搭建一个个人博客
```
    本文记录用hexo搭建个人博客的过程和避坑指南，会持续更新和完善
```

## 写在前面
### 提示
搭建环境：macOS\
md文件编辑器；vs code\
如何使用markdown语言编写博客：[markdown教程](https://www.runoob.com/markdown/md-table.html)\
博客GitHub地址：[点击跳转](https://github.com/gooddefense/gooddefense.github.io)


### 作者想说 
今天闲着没事干，玩了一下当下很火的CharGPT。CharGPT是一个智能聊天机器人程序，我体验了一下，基本上我问的问题，CharGPT都可以很准确的给到我答案，它也可以处理一下有难度的工作，比如写文章，写代码，处理文档等等。在这期间，我问了它一个问题，就是如何搭建个人博客，它给出的答案是用框架来搭建。我之前对这些框架的了解比较少，对这一类框架也比较好奇。为了满足自己的好奇心，我决定试一试这些博客框架。

[参考链接](https://blog.csdn.net/weixin_41160054/article/details/89531921?ops_request_misc=&request_id=&biz_id=102&utm_term=mac%E4%BD%BF%E7%94%A8hexo%E2%80%94%E2%80%94script&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-0-89531921.142^v73^insert_down1,201^v4^add_ask,239^v1^insert_chatgpt&spm=1018.2226.3001.4187)

## 可能会用到的一些异常解决办法(持续更新)
**提示：这里只记录作者在碰到此类问题时的解决办法，若以下方法没有解决问题，请自行查阅网上相关资料**
### 输入指令后长时间没有响应
碰到以下情况：
- 输入指令
```
    git push
    git pull
```
- 出现长时间无法登陆GitHub

**解决办法：**

刷新DNS缓存：
在终端输入以下指令
```
    sudo killall -HUP mDNSResponder
```



## 搭建过程
```
我最后选择用hexo来搭建我的个人博客，至于为什么不用wordPress或者其他的，我只能说hexo打的字少，其他的字多我懒得打。
```

### 创建Github仓库
- 登录GitHub账号，如果没有的话就先注册一个
- 登录成功之后，进入到个人主页，点击Repositories,这一个页面就是仓库；点击右上角的New按钮可以进入创建仓库界面，自行填写相关参数就可以了

### 配置SSH keys
1. 打开终端，输入命令
```
    cd ~/.ssh    #进入电脑下的ssh文件
```
2. 生成新的SSH keys
```
    ssh-keygen -t rsa -C "你的邮箱地址"
```
执行此条命令后，最后出现类似长方形的字符画即表示成功。
3. 将SSH keys添加进Github
- 打开刚刚生成的文件.ssh/id_rsa.pub(可以用VSCode打开查看)
- 复制所有内容
- 进入Github->点击头像栏的settings->选择SSH and GPG keys->点击New SSH Key->将内容复制进key->点击add SSH Key
4. 进行测试，输入以下指令：
```
ssh -T git@GitHub.com #全部复制，无需更改
```
接下来会出现
```
The authenticity of host 'GitHub.com (207.97.227.239)' can't be established.
RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
Are you sure you want to continue connecting (yes/no)?<输入yes>
Hi 你的用户名! You've successfully authenticated, but GitHub does not provide shell access.
```
出现以上提示，则证明添加SSH Keys成功
5. 测试Github Pages是否创建成功，输入以下命令：
```
echo "# 你的用户名.github.io" >> README.md
git init    
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/你的用户名/你的用户名.github.io.git
git push -u origin master
```
之后在浏览器中输入 【你的名字】.github.io ，如果成功出现页面，并且页面上是你刚输入的地址，那么github pages配置成功。


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
### 安装hexo
- 执行以下代码：
```
    npm install -g hexo-cli
    hexo init blog
    cd blog
    npm install
```
- 测试hexo是否可以运行
```
    cd blog
    hexo s
```
在浏览器上输入**http://localhost:4000/**，如果显示网页，则证明成功
当然，现在这个页面只能在本地进行浏览，所以我们现在需要将hexo通过Github Pages部署到Github服务器
### 部署hexo到Github服务器上
1. 安装hexo-deployer-git
```
npm install hexo-deployer-git --save
```
2. 修改_config.yml (路径：/blog/_config.yml)
```
deploy:
  type: git
  repo: <repository url> #你的 【你的名字】.github.io  这一项目的git地址#
  branch: master 
  message: [message] #可不填写#
```
3. 执行命令将hexo部署到服务器上
```
    hexo clean
    hexo g
    hexo d
```
- 如果执行命令后出现错误，就重复执行下列语句
```
    npm install hexo-deployer-git --save
```
执行完毕后，应该就可以在**你的名字.github.io**看到你的网页了

### 更新博客文章
1. 创建新文章
```
    hexo new "新文章"
```
2. 编写文章
这里推荐使用vscode，typora也行，但是typora需要付费
3. 更新main分支
```
    hexo clean #可忽略
    hexo generate #使刚刚完成写作的文章生成网站静态文件到默认设置的 public 文件夹
    hexo s #启动本地服务器
    hexo d #一键部署
```
4. 更新hexo分支
```
    git add -A （此命令用来添加所有文件到暂存区）
    git commit -m "新增博客文章"  （此命令用来提交，双引号内可自定义内容，双引号前有空格）
    git push origin hexo （此命令用来推送hexo分支到Github）
    # 此条命令有时候会上传失败，可以使用下面这个命令
    # git push origin HEAD:hexo
```

### 自定义你的hexo博客（持续更新）
Hexo博客支持很多种主题，这里的话只记录Next主题的配置方法
#### Next主题的安装和配置
1. 在博客主目录下执行
```
    git clone https://github.com/theme-next/hexo-theme-next themes/next
```
2. 配置_config.yml文件
```
    theme:next
```
3. Next主题有几种风格：Muse、Mist、Pisces、Gemini，同样可以通过配置_config.yml来实现主题的切换
- **注意：这里的_config.yml文件路径是在:/blog/themes/next/_config.yml**
```
    override：false #表示是否将主题置为默认样式
cache:
	enable:true #表示添加缓存功能，这样浏览器后续打开我们的博客网站会更快
menu: #设置博客各个页面的相对路径，默认根路径是blog/source
  home: / || home
  about: /about/ || user
  tags: /tags/ || tags
  categories: /categories/ || th
  archives: /archives/ || archive
  #schedule: /schedule/ || calendar #日历
  #sitemap: /sitemap.xml || sitemap #站点地图，供搜索引擎爬取
  #commonweal: /404/ || heartbeat # 腾讯公益404

# Enable/Disable menu icons / item badges.
menu_settings:
  icons: true # 是否显示各个页面的图标
  badges: true # 是否显示分类/标签/归档页的内容量
# Schemes
scheme: Gemini
```
#### Next各种新鲜玩法
目前本博客还没有加入很多的插件，这里只记录本站加入的插件的办法
1. 在每篇文章末尾统一添加“本文结束”标记\
**实现效果图:**
![](https://blogdata-1258545379.cos.ap-shanghai.myqcloud.com/20190124/1548274181405.png)
**实现方法：**
1. 在路径 \themes\next\layout\_macro 中新建 passage-end-tag.swig 文件,并添加以下内容：
```
    <div>
        {% if not is_index %}
            <div style="text-align:center;color: #ccc;font-size:14px;">-------------本文结束<i class="fa fa-paw"></i>感谢您的阅读-------------</div>
        {% endif %}
    </div>
```
2. 接着打开路径\themes\next\layout\_macro\post.swig文件，在post-body 之后， post-footer 之前添加如下代码（post-footer之前两个大括号）
```
      {%- if not is_index %}
        {{ partial('_macro/passage-end-tag.swig') }}
      {%- endif %}
```
3. 打开初始路径下的主题配置文件_config.yml,在末尾添加以下代码：
```
    # 文章末尾添加“本文结束”标记
    passage_end_tag:
        enabled: true
```
完成后即可显示对应标记

## 参考链接
[hexo博客如何写作和更新](https://blog.csdn.net/qq_51513895/article/details/120065812?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522167587559916782425187391%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=167587559916782425187391&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-1-120065812-null-null.142^v73^insert_down1,201^v4^add_ask,239^v1^insert_chatgpt&utm_term=hexo%E6%9B%B4%E6%96%B0%E6%96%87%E7%AB%A0&spm=1018.2226.3001.4187)\
[hexo博客优化和美化](https://blog.csdn.net/nightmare_dimple/article/details/86661502?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522167596487316782425182334%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=167596487316782425182334&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-4-86661502-null-null.142^v73^insert_down1,201^v4^add_ask,239^v1^insert_chatgpt&utm_term=hexo%E4%B8%BB%E9%A2%98&spm=1018.2226.3001.4187)\
[macOS刷新DNS](https://blog.csdn.net/weixin_59197425/article/details/125407632?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522167580152016800211583204%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=167580152016800211583204&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-1-125407632-null-null.142^v73^insert_down1,201^v4^add_ask,239^v1^insert_chatgpt&utm_term=mac%E5%88%B7%E6%96%B0dns&spm=1018.2226.3001.4187)\
[hexo攻略添加分类和标签](https://blog.csdn.net/qq_39181839/article/details/109477607?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522167600792016800184181004%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=167600792016800184181004&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-1-109477607-null-null.142^v73^insert_down1,201^v4^add_ask,239^v1^insert_chatgpt&utm_term=hexo%E5%88%86%E7%B1%BB&spm=1018.2226.3001.4187)\
[hexo美化加强版](http://shenzekun.cn/hexo%E7%9A%84next%E4%B8%BB%E9%A2%98%E4%B8%AA%E6%80%A7%E5%8C%96%E9%85%8D%E7%BD%AE%E6%95%99%E7%A8%8B.html)