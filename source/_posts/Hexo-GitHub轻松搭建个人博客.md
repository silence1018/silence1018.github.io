---
title: Hexo+GitHub轻松搭建个人博客
date: 2020-05-03 15:21:55
tags:
---
>本教程是在已经安装`Node`、`Git`、`npm`，并注册`Github`账号的前提下进行的，如果以上条件不具备，请查看相关博客文章

>Hexo是一个简单、快速、强大的基于 Github Pages 的博客发布工具，支持Markdown格式，有众多优秀插件和主题。


<!--more-->

### 配置Github
#### 创建仓库
创建一个仓库，用于存放博客文章，注意下面截图中的红色部分必须是你的用户名，不是昵称--`用户名.github.io`

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200502135646848.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjIwNTEwMQ==,size_16,color_FFFFFF,t_70)

#### 生成SSK Keys(已经配置过的略过)

执行CMD命令`ssh-keygen -t rsa -C "注释文字（可以为邮箱或者名字）"`

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200502142651400.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjIwNTEwMQ==,size_16,color_FFFFFF,t_70)

#### 将本地生成的`SSH`秘钥添加到`GitHub`

秘钥文件的地址上面的截图中有，默认在`C:用户/用户名/.ssh`目录下，的`id_rsa.pub`文件中，用记事本打开该文件，全选复制里面的内容

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200502143143716.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjIwNTEwMQ==,size_16,color_FFFFFF,t_70)

点击你的`Github`头像，选择`Settings`,然后选择`SSH and GPG keys`,最后点击右侧的`New SSH key`,输入标题，粘贴秘钥，点击确定

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200502143430190.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjIwNTEwMQ==,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200502143623127.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjIwNTEwMQ==,size_16,color_FFFFFF,t_70)

#### 验证SSH  Keys是否配置成功
执行CMD命令`ssh -T git@github.com`  如下所示则为成功

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200502144518435.png)

#### 完善`github`个人信息
执行以下`CMD`命令,用于`Github`操作统计，可以不是`github`的用户名和邮箱

`$ git config --global user.name "wuyalan"`   输入用户名

`$ git config --global user.email  "alan.wyl@foxmail.com"`  输入邮箱

### Hexo安装及配置

[Hexo官网](http://hexo.io)

[Hexo github地址](https://github.com/hexojs/hexo)

#### 全局安装Hexo

`npm install -g hexo-cli`   

#### 安装部署插件
+ 新建一个文件夹，用于存放`hexo`,我这里创建一个`MyBlog`文件夹
+ 执行`CMD`命令`npm init`生成一个`package.json`文件
+ 执行`CMD`命令` npm install hexo-deployer-git --save`安装部署插件
+ 执行`CMD`命令`npm install`  安装依赖

#### 初始化Hexio
执行`CMD`命令`hexo init`，会生成以下文件

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200502150015191.png)
 

<!-- + 创建hexo文件夹,以后文章都写在这里面，在文件夹下执行`hexo init`

>此时，基本的`Hexo`其实已经安装完毕了，并自动生成了一篇示例文章，执行以下命令就可以在本地进行浏览器预览

`hexo g` 生成网页，每次进行相应改动都要hexo g 生成一下
`hexo s`  启动一个本地服务器，实现本地预览，默认端口4000
>执行以上命令之后，hexo就会在public文件夹生成相关html文件，在浏览器地址栏输入`localhost:4000 `,即可预示例文章

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200502135239916.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjIwNTEwMQ==,size_16,color_FFFFFF,t_70) -->



#### 写一篇博客
在`MyBlog`目录下执行`hexo new 'my-first-blog'`

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200502151406626.png)

会在`MyBlog\source\_posts`下生成一个`my-first-blog.md`文件

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200502151544796.png)

 打开`my-first-blog.md`文件编辑博客

```
---
title: postName #文章页面上的显示名称，一般是中文
date: 2013-12-02 15:30:16 #文章生成时间，一般不改，当然也可以任意修改
categories: 默认分类 #分类
tags: [tag1,tag2,tag3] #文章标签，可空，多标签请用格式，注意:后面有个空格
description: 附加一段文章摘要，字数最好在140字以内，会出现在meta的description里面
---

以下是正文
文章，1984年6月26日出生于陕西省西安市，中国内地男演员、导演。2006年毕业于中央戏剧学院表演系。
2004年参演电视剧《与青春有关的日子》，开始在影视圈崭露头角 [1]  。2005年拍摄古装剧《锦衣卫》。2007年主演赵宝刚导演的青春剧《奋斗》； [2]  同年，主演首部电影《走着瞧》。2008年主演滕华涛执导的电视剧《蜗居》，饰演80后城市青年小贝。 [1]  [3]  2009年，在电影《海洋天堂》中扮演自闭症患者王大福；同年参演抗战题材的电视剧《雪豹》 [4]  。2011年，主演的电视剧《裸婚时代》在各大卫视播出； [5]  2011年-2012年连续2年获得北京大学生电影节 [6-7]  最受大学生欢迎男演员奖。2012年，凭借电影《失恋33天》获得第31届大众电影百花奖最佳男主角奖； [8]  同年成立自己经营的北京君竹影视文化有限公司，并导演第一部影视作品《小爸爸》。2013年2月，主演的电影《西游·降魔篇》在全国上映。 [9] 
2014年3月28日，主演的中韩合资文艺爱情片《我在路上最爱你》在全国上映。2014年12月18日，在姜文执导的动作喜剧片《一步之遥》中扮演武七一角。 [10]  2016年，主演电视剧《少帅》，饰演张学良 [11]  ；主演电视剧《剃刀边缘》 [12]  。7月15日导演的电影《陆垚知马俐》上映。 [13] 
演艺事业外，文章也参与公益慈善事业，2010年成立大福自闭症关爱基金。
2017年9月16日，凭借《陆垚知马俐》获得第31届中国电影金鸡奖导演处女作奖 [14]  。
2019年7月28日，文章通过微博宣布，与妻子马伊琍离婚 [15] 
```
#### 生成HTML页面
每次修改博客后，都要先生成`html`页面，然后才能本地预览或者部署，执行`CMD`命令`hexo g`生成`html`页面

#### 本地预览
在`MyBlog`目录下执行命令`hexo s`,打开浏览器，地址栏输入`http://localhost:4000`即可本地预览
```node
F:\个人\MyBlog>hexo s
INFO  Start processing
INFO  Hexo is running at http://localhost:4000 . Press Ctrl+C to stop.
```

#### 部署到GitHub
在`MyBlog`目录下执行命令`hexo d` 

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200502150210757.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjIwNTEwMQ==,size_16,color_FFFFFF,t_70)

#### 查看效果
打开浏览器，在地址栏输入`github用户名.github.io`

#### Hexo常用命令
[Hexo常用命令](https://hexo.io/zh-cn/docs/commands)


#### 修改网站语言
>打开站点配置文件，`_config.yml`
```yml
# Site
title: Hexo
subtitle: ''
description: ''
keywords:
author: Selience
language: zh-CN
timezone: ''
```
我这里将语言改为了中文，有些教程说改成`zh-Hans`，但是我改了之后变成了阿拉伯文，最后发现，这里设置的语言，要在你当前使用主题文件夹下的`languages`文件夹下才行
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020050220580896.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjIwNTEwMQ==,size_16,color_FFFFFF,t_70)

#### 网站底部添加字数统计和阅读统计
+ 安装插件

`npm install hexo-symbols-count-time --save`
+ 修改站点配置

就是你最开始新建的那个目录下的`_config.yml`，打开统计开关
```js
symbols_count_time:
  symbols: true                # 文章字数统计
  time: true                   # 文章阅读时长
  total_symbols: true          # 站点总字数统计
  total_time: true             # 站点总阅读时长
  exclude_codeblock: false     # 排除代码字数统计
```
+ 修改主题配置文件

`themes`文件夹下每个文件夹就是一个主题，打开主题文件夹内的`_config.yml`，找到`symbols_count_time`选项，没有的话就新建
```yml
# Post wordcount display settings
# Dependencies: https://github.com/theme-next/hexo-symbols-count-time
symbols_count_time:
  separated_meta: true     # 是否另起一行（true的话不和发表时间等同一行）
  item_text_post: true     # 首页文章统计数量前是否显示文字描述（本文字数、阅读时长）
  item_text_total: true   # 页面底部统计数量前是否显示文字描述（站点总字数、站点阅读时长）
  awl: 4                   # Average Word Length
  wpm: 275                 # Words Per Minute（每分钟阅读词数）
  suffix: mins.
```
+ 修改文字描述

就是例如`首页`、`标签`、`本文字数`、`阅读时长`、`发表于`等这些文字，如果要修改，就打开当前主题文件夹下的`themes`文件夹，打开当前所使用的语言的配置文件，进行修改

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200502210202857.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjIwNTEwMQ==,size_16,color_FFFFFF,t_70)

+ 顶部效果

![!\[在这里插入图片描述\](https://img-blog.csdnimg.cn/20200502205040160.png](https://img-blog.csdnimg.cn/20200502205132785.png)

+ 底部效果

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200502205054630.png)

#### 添加网站访问量、访客量、文章阅读量
我用的`next`主题版本为`7.8.0`，内部已经集成了了`busuanzi`,只需要在主题配置啊文件中开启就可以，打开主题配置文件`_config.yml`,查找`busuanzi_count`选项，没有的就新建
```yml
# Show Views / Visitors of the website / page with busuanzi.
# Get more information on http://ibruce.info/2015/04/04/busuanzi
busuanzi_count:
  enable: true #开启busuanzi统计
  total_visitors: true #总访客数
  total_visitors_icon: fa fa-user
  total_views: true #总访问量
  total_views_icon: fa fa-eye
  post_views: true #文章浏览量
  post_views_icon: fa fa-eye
```

效果如下

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200504165734720.png)

#### 改变菜单位置
`首页`、`归档`这两个默认菜单显示位置在最上面，想让其显示在侧边，还是打开主题配置文件`_config.yml`,找到`_config.yml`(解构)属性，里面有四种选择自己喜欢的即可！
```yml
# Schemes
# scheme: Muse
# scheme: Mist
# scheme: Pisces
scheme: Gemini
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200504195048694.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjIwNTEwMQ==,size_16,color_FFFFFF,t_70)


[参考文章1---详细教程](https://zhuanlan.zhihu.com/p/80142778?from_voters_page=true)

[参考文章2---详细教程](https://www.cnblogs.com/liuxianan/p/build-blog-website-by-hexo-github.html)

[参考文章3---美化整理](https://www.jianshu.com/p/ec2e6c8a1d89)

[参考文章3---每篇文章阅读量统计](https://bjtu-hxs.github.io/2018/06/12/leancloud-config/)