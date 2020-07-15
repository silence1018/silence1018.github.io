---

title: 如何备份Hexo

date: 2020-07-15 17:14:30

tags:

---

​	使用`Hexo`和`gitHub`搭建完自己的博客后，突然想到一个问题，就是`Hexo`是装在自己电脑上的，它的配置文件、博客源文件都是存在电脑上的，而远程`gitHub`仓库里面的文件是`.deploy_git`文件夹下的文件，我猜应该是执行`hexo g`、`hexo d`命令后生成的`html`文件以及相关文件，并不是吧本机`Hexo`目录下的所有文件都上传到`gitHub`，这么一来，如果某一天，你换了电脑，或者重装系统，那整个博客目录都没了，包括`hexo`的配置文件和博客源文件，主要是博客源文件文件没了，就很尴尬，除非你把`source\_posts`目录下的所有`.md`文件都备份下来，然后再自己安装`hexo`、配置环境、连接`gitHub`,最后再把你备份的所有`.md`格式的博客源文件复制到`source\_posts`目录下，然后再`hexo g`、`hexo d`部署到`gitHub`,但是这样总觉得有点。。。。
<!--more-->
​	其实我刚开始有个思路，就是在`gitHub`再建一个仓库`Hexo`，专门用于存放本机博客相关的所有源文件，每次写完博客部署到`gitHub`后，再把所有文件`push`到`Hexo`仓库，不过在看了知乎一个提问下的某个评论后，茅塞顿开，大概思路就是，给放博客那个仓库再新建一个分支，就叫`hexo`,名字随意，开心就好，专门用于存放源文件，而默认的`master`分支则用于存放编译之后的文件，下面开始操作！！！


### 新建分支hexo

登陆你的`gitHub`,找到你的博客的仓库，新建一个分支，名字随意，我取名为`hexo`,因为我的博客已经搭建好了，所以新建分支后，`hexo`分支和默认的主分支`master`分支里面的内容一样，都是编译后的文件

### 替换hexo分支内的文件

如上所说，此时，`hexo`分支内的文件还是编译后，而我们要做的就是将`hexo`分支内的文件替换为源文件:

+ 将远程的整个博客仓库`clone`到本地,得到一个名为`liaijie.github.io`的文件夹，里面就是编译好的文件

+ 在`liaijie.github.io`根目录下，打开`git bash`命令面板，默认为`master`分支，执行`git branch hexo`，切换到`hexo`分支

+ 此时打开文件管理器，将`liaijie.github.io`文件夹下，除`.git`之外的所有文件都删除，将本机上所有`Hexo`源文件除`.deploy_git`外全部复制过来

+ 最后将本地的更改提交，`push`到远程`gitHub`,依次执行`git add .`、`git commit -m '备份hexo源文件01'`、`git push origin hexo`

  ***注：***如果`theme`文件夹中有`.git`文件，那么应该把主题文件中的`.git`文件夹删掉，因为git不能嵌套上传

### 博客部署+源文件提交

  上面操作完毕后，就可以删除本机原来的博客文件夹，以后写博客就在这个`liaijie.github.io`文件夹下操作

+ 新建博客`hexo new '博客测试'`  

+ 编写博客

+ 生成`HTML`页面:`hexo g`  

+ 署到`gitHub`:`hexo d`  

+ 切换到`hexo`分支：`git branch hexo`

+ 源文件提交：`git add .`、`git commit -m '备份hexo源文件02'`、`git push origin hexo`                                                                                         

### 改进

从上面可以看到，我们每次打开`git bash`面板后，默认是`master`分支，需要手动切换到`hexo`分支，所以我们索性直接把`hexo`设置为默认分支，这样就不用每次手动切换分支了，博客写完后可以直接`hexo d`、`git add .`、`git commit -m '备份hexo源文件0X'`、`git push origin hexo`,不用怕出错，只要是在源文件下执行的`hexo d`就不会出错，`hexo`内部应该是在这里只将编译后的`html`及 相关文件执行了`git push origin master`

### 新机部署

如果你换了新电脑，别怕：

+ 下载安装`hexo`和部署插件

+ `SSH Keys`生成生成并添加到`gitHub`

+ 跳过`hexo init`初始化

+ 将远程`gtiHub`的`hexo`分支下的源文件复制到本机

+ `npm install`安装依赖

+ 写博客、部署博客、提交源文件

  ***注意:`npm`安装的`hexo`和`hexo`分支下的配置文件可能会有问题，因为`hexo`分支下的配置文件是原版本的`hexo`的配置文件，而你下载的`hexo`可能是最新版本，所以配置可能会不同，你可以安装指定版本的`hexo`***
