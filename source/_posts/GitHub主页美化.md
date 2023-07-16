

## 1、创建仓库

+ 创建一个仓库，仓库名称和GitHub用户名保持一致
+ 仓库类型为公开，即Public
+ 勾选`Add a README file`,用于显示自定义内容
+ 点击`Create respository`确定创建
  
  ![image](https://github.com/silence1018/Knowledge-summary/assets/20808301/0f7536f5-feca-4452-9025-31504afe216e)


## 2、开始美化

所用仓库：[github-readme-stats][]

阅读该仓库`readme.md`文件，该文件为使用说明文档，默认显示的是英文版，文档全部在该仓库`/docs`目录下，点击顶部`简体中文`直达中文版


改仓库方案主要包含以下模块：

### GitHub Stats Card-状态卡片

   主要显示当前GitHub用户的获得Start数、累计提交数（commit）、拉取请求数（PR）、审查PR数、指出问题数（issue）、参与贡献数、总体评分等。
   
  #### 添加方法
  
   ```html
    [![Anurag's GitHub stats](https://github-readme-stats.vercel.app/api?username=anuraghazra)](https://github.com/anuraghazra/github-readme-stats)
  ```
  上面的代码其实就是`markdown`的图片链接语法`![图片提示词](图片地址)`和普通链接语法`[链接标题](链接地址)`的嵌套，将图片链接作为普通链接的标题，点击图片就会跳到作者的`GitHub`,作者这么写是为了引流，
  所以我们在自己写的时候可以解开嵌套，写法如下：

  ```html
  ![Anurag's GitHub stats](https://github-readme-stats.vercel.app/api?username=anuraghazra)
  ```
  + 将上面一行代码复制粘贴至自己第一步创建仓库的`readme`文件，并将`anuraghazra`替换为自己的GitHub用户名
    
  + 你也可以将其中的链接复制出来，在`readme`文件写一个`img`标签，将链接作为`src`属性值
    
  ```html
    <img align='center'src="https://github-readme-stats.vercel.app/api?username=silence1018&show=reviews&show_icons=true&theme=tokyonight"/> `
  ```

  #### 定制化

  `GitHub Stats Card`使用文档还有各种自定义配置属性，包括字体、图标、显示项目、主题等，具体写法请[参阅文档](https://github.com/anuraghazra/github-readme-stats/blob/master/readme.md#customization)
  
  #### 显示效果
  
  <img  src="https://github.com/silence1018/Knowledge-summary/assets/20808301/00c53b9a-7b6b-44fa-a630-042d2d49e278">

### Top Languages Card-语言卡片

主要显示当前GitHub用户常用语言。注意这里只统计属于自己的非fork非私有仓库的语言使用情况

 #### 添加方法
 
  ```html
    ![Top Langs](https://github-readme-stats.vercel.app/api/top-langs/?username=anuraghazra)
  ```
  
  + 将上面一行代码复制粘贴至自己第一步创建仓库的`readme`文件，并将`anuraghazra`替换为自己的GitHub用户名
    
  + 你也可以将其中的链接复制出来，在`readme`文件写一个`img`标签，将链接作为`src`属性值
    
  ```html
  <img align='center'src="https://github-readme-stats.vercel.app/api/top-langs/?username=anuraghazra"/> `
  ```
  
  #### 定制化

  具体写法请[参阅文档](https://github.com/anuraghazra/github-readme-stats/blob/master/readme.md#exclude-individual-repositories)
  
  #### 显示效果
  
  ![image](https://github.com/silence1018/Knowledge-summary/assets/20808301/c58c94fc-abb0-4bf4-97fd-298ade7510aa)

### GitHub Extra Pins-置顶卡片

最多显示6个当前GitHub用户置顶过(Pin)的项目。

 #### 添加方法
 
  ```html
    ![Readme Card](https://github-readme-stats.vercel.app/api/pin/?username=anuraghazra&repo=github-readme-stats)
  ```
  
  + 将上面一行代码复制粘贴至自己第一步创建仓库的`readme`文件，并将`anuraghazra`替换为自己的GitHub用户名
    
  + 你也可以将其中的链接复制出来，在`readme`文件写一个`img`标签，将链接作为`src`属性值
    
  ```html
  <img align='center'src="https://github-readme-stats.vercel.app/api/pin/?username=anuraghazra&repo=github-readme-stats"/> `
  ```
  
  #### 显示效果
  
  这里没有定制化效果，所以也没有特殊的显示效果，仅仅就是可以自定义显示位置，因为这个`Pins`模块`GitHub`默认就有显示
  
### Wakatime Stats Card-时长统计卡片

这个卡片主要用于配合[Wakatime](https://wakatime.com/)进行编码时长的统计

#### 添加方法
 
  ```html
    ![Harlok's wakatime stats](https://github-readme-stats.vercel.app/api/wakatime?username=ffflabs)
  ```
  
  + 将上面一行代码复制粘贴至自己第一步创建仓库的`readme`文件，并将`ffflabs`替换为自己的GitHub用户名
    
  + 你也可以将其中的链接复制出来，在`readme`文件写一个`img`标签，将链接作为`src`属性值
    
  ```html
  <img align='center'src="https://github-readme-stats.vercel.app/api/wakatime?username=ffflabs"/> 
  ```
#### 显示效果

![image](https://github.com/silence1018/Knowledge-summary/assets/20808301/6ce3d42e-c407-40a3-b200-408f7206ee66)

不过，在代码时长统计这块，我们不使用这个仓库，使用另外一个仓库，下面👇🏻我会有介绍

## 3、Wakatime

### 介绍

`WakaTime`是一个编码追踪分析网站。通过为集成开发环境和文本编辑器安装`WakaTime`插件，分析编码的系统、用户、语言、时间等信息，统计出详细的数据，并以可视化形式在`WakaTime`网站的`dashboard`面板显示。

### 注册登录

[注册登录][wakatime-login],这里建议直接使用`GitHub`账号登录

![image](https://github.com/silence1018/Knowledge-summary/assets/20808301/098e9294-3426-4124-81b8-753980738c84)

### 获取Secret API Key

[获取Secret API Key][wakatime-key]

![image](https://github.com/silence1018/Knowledge-summary/assets/20808301/3556d5ca-c2f1-4740-a35c-655f03d2ef39)

### 编辑器安装WakaTime插件

这里以`VsCode`为例,在左侧拓展商店搜索`Wakatime`并点击安装

![image](https://github.com/silence1018/Knowledge-summary/assets/20808301/ef36e528-9f93-49d2-ab67-42533eae2805)

### WakaTime插件设置Api Key
作用：这一步的作用是将`VsCode`上的`WakaTime`插件和你的`WakaTime`账号绑定起来，这样`WakaTime`就可以获取到你在编辑器的编码信息了

方法： 快捷键`⌘command` + `⇧shift`,出现搜索框，输入关键字`waka`即可，选择`WakaTime: Api Key`,再次出现输入框，全选清除输入框内原有内容，粘贴在`WakaTime`网站复制的`Secret API Key`,最后
  按下回车即可

  ![image](https://github.com/silence1018/Knowledge-summary/assets/20808301/86a17bf6-0761-4bfa-8e3a-68500bb8da9f)

  ![image](https://github.com/silence1018/Knowledge-summary/assets/20808301/4f72f86a-bbcd-41a8-9f24-5e243cfcebac)

## 4、创建一个GitHub个人访问令牌(Personal access tokens)

按照`Settings / DeveloperSettings /Personal access tokens/Tokens`的菜单路径找到创建`token`的地方，点击右上角`Generate new token`按钮。`Note`相当于备注，随便填，尽量用英文；下面的
`Select scopes`表示该`token`的访问权限，勾选`repo`(完全的仓库权限)和`user`(完全的用户信息数据权限)，最后点击最下面的`Generate token`按钮完成创建。

<img width="790" alt="image" src="https://github.com/silence1018/Knowledge-summary/assets/20808301/3ba2e74f-7602-4c59-b0cb-c62eef880eaf">

创建完成后弹出如下界面，点击复制创建的`token`,这个`token`只有这一次可见，切记将其复制到其它地方备用

<img width="787" alt="image" src="https://github.com/silence1018/Knowledge-summary/assets/20808301/791d1287-fcf1-4361-a12e-a69ea3fdf3e5">

## 5、为新建的仓库创建两个秘钥(secrets)

### WAKATIME_API_KEY

作用： 用于获取`WakaTime`的统计数据

回到文章开头我们创建的仓库，进入该仓库，按照`Settings/Secrets and variables/Actions`的菜单路径找到创建secrets的地方，点击右上`New repository secret`按钮，`Name`值填`WAKATIME_API_KEY`,
`secret`填`WakaTime`网站上的`Secret API Key`,最后点击确定

<img width="804" alt="image" src="https://github.com/silence1018/Knowledge-summary/assets/20808301/dd8052bb-ecf0-475f-b1f9-8b21e850de29">


### GH_TOKEN

作用：用于获取用户信息和操作仓库

再次重复上面的步骤创建名为`GH_TOKEN`的`secret`,`Name`值填`GH_TOKEN`,`secret`填我们在第4步创建的`token`的值，最后点击确定

<img width="802" alt="image" src="https://github.com/silence1018/Knowledge-summary/assets/20808301/ee45aea7-8a65-45f1-af63-8700648dd486">

## 6、为新建的仓库创建工作流

作用：定时或手动执行一系列操作，并将我们想要的统计结果添加到`readme`文件

还是文章开头我们创建的仓库，点击`Action`菜单，再次点击`set up a workflow yourself`,打开一个工作流配置文件编辑界面。

接下来轮到我们要用到的第二个仓库[waka-readme-stats][waka-readme-stats]了，我们打开这个仓库，找到[配置文件示例](https://github.com/anmol098/waka-readme-stats#profile-repository)，复制其内容到我们的工作流配置文件编辑界面中，然后点击右上角`Commit Chanages`按钮，然后会在新建的仓库下生成一个`workflows`文件夹，里面有个`main.yml`文件就是刚才的工作流配置文件。

<img width="1512" alt="image" src="https://github.com/silence1018/Knowledge-summary/assets/20808301/473783ae-4e71-46fc-961a-b1047a406300">



如上图所示，这里的`WAKATIME_API_KEY`和`GH_TOKEN`就是我们第5步创建的那两个，有了这个`GH_TOKEN`,这个工作流配置文件才能自动执行。

另外在`waka-readme-stats`仓库的[action.yml](waka-readme-stats)文件中有部分关于上述配置字段的描述,可以看看

配置中的`cron`定时任务cron表达式，感兴趣的可以参考[定时任务cron表达式详解](https://blog.csdn.net/zhongaiyisheng_/article/details/108264914)、[在线Cron表达式生成器](https://cron.qqe2.com/)

## 7、在readme文件中为统计数据放置占位符

```html
<!--START_SECTION:waka-->
<!--END_SECTION:waka-->
```

打开新建仓库的`readme`文件进入编辑模式，将上述代码复制粘贴到你想要展示`WakaTime`统计数据的位置，然后点右上角`Commit Changes`按钮提交修改

## 8、手动执行一次工作流

因为我们的工作流设置的是每天晚上0点自动执行，所以为了看到效果，我们需要先手动执行一次工作流。

再次回到新建仓库的`Actions`面板，点击右侧`Waka Readme`,中间右上角会出现我们刚才创建的`yml`配置文件名，即这个工作流就是我们刚才创建的那个，然后点击右侧`Run workflow`按钮，展开后，再次点击`Run workflow`,手动执行工作流

<img width="1510" alt="image" src="https://github.com/silence1018/Knowledge-summary/assets/20808301/52b03a80-5cf8-426a-a27f-d3e2a0865331">

几秒后就可以看到工作流正在执行，可以点击进去查看执行进度

<img width="1142" alt="image" src="https://github.com/silence1018/Knowledge-summary/assets/20808301/d2aacb31-2619-468c-a2f3-105fa212051b">

<img width="1164" alt="image" src="https://github.com/silence1018/Knowledge-summary/assets/20808301/26d422dd-2a25-451a-9b5c-5dac65f9bb3b">

最后执行完成后，我们回到我们的`GitHub`个人主页的概况页面，也就是`Your profil`里面的`Overview`查看效果

![image](https://github.com/silence1018/Knowledge-summary/assets/20808301/5a381959-bd7f-436b-955a-7c0aee6a2bbd)

---

除了上述美化外，readme还有很多美化方案，下面放一些链接供大家参考

[waka-readme-stats][waka-readme-stats]

[github-readme-stats][github-readme-stats]

[Awesome GitHub Profile README](https://github.com/abhisheknaiidu/awesome-github-profile-readme)

[Github 首页美化教程（一）：打造个性化的GitHub首页](https://zhuanlan.zhihu.com/p/454597068)




[github-readme-stats]: https://github.com/anuraghazra/github-readme-stats "点击直达"
[waka-readme-stats]: https://github.com/anmol098/waka-readme-stats "点击直达"
[wakatime-login]: https://wakatime.com/login "点击直达"
[wakatime-key]: https://wakatime.com/settings/account "点击直达"
