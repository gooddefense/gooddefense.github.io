---
title: hexo博客自定义
date: 2023-03-07 18:12:22
tags:
categories: Hexo
---

## Next主题
Hexo博客支持很多种主题，这里的话只记录Next主题的配置方法
### Next主题的安装和配置
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
### Next各种新鲜玩法
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

### 参考链接
[hexo博客如何写作和更新](https://blog.csdn.net/qq_51513895/article/details/120065812?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522167587559916782425187391%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=167587559916782425187391&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-1-120065812-null-null.142^v73^insert_down1,201^v4^add_ask,239^v1^insert_chatgpt&utm_term=hexo%E6%9B%B4%E6%96%B0%E6%96%87%E7%AB%A0&spm=1018.2226.3001.4187)\
[hexo博客优化和美化](https://blog.csdn.net/nightmare_dimple/article/details/86661502?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522167596487316782425182334%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=167596487316782425182334&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-4-86661502-null-null.142^v73^insert_down1,201^v4^add_ask,239^v1^insert_chatgpt&utm_term=hexo%E4%B8%BB%E9%A2%98&spm=1018.2226.3001.4187)\
[macOS刷新DNS](https://blog.csdn.net/weixin_59197425/article/details/125407632?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522167580152016800211583204%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=167580152016800211583204&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-1-125407632-null-null.142^v73^insert_down1,201^v4^add_ask,239^v1^insert_chatgpt&utm_term=mac%E5%88%B7%E6%96%B0dns&spm=1018.2226.3001.4187)\
[hexo攻略添加分类和标签](https://blog.csdn.net/qq_39181839/article/details/109477607?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522167600792016800184181004%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=167600792016800184181004&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-1-109477607-null-null.142^v73^insert_down1,201^v4^add_ask,239^v1^insert_chatgpt&utm_term=hexo%E5%88%86%E7%B1%BB&spm=1018.2226.3001.4187)\
[hexo美化加强版](http://shenzekun.cn/hexo%E7%9A%84next%E4%B8%BB%E9%A2%98%E4%B8%AA%E6%80%A7%E5%8C%96%E9%85%8D%E7%BD%AE%E6%95%99%E7%A8%8B.html)

## fluid主题
参考文档---[fluid主题用户手册](https://hexo.fluid-dev.com/docs/start/#%E4%B8%BB%E9%A2%98%E7%AE%80%E4%BB%8B)
**具体配置参考用户手册即可**