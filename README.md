# 个人博客部署教程

### 一、在 github 创建博客项目仓库

#### 1、创建仓库

首先打开 github，点击 New repository，创建一个新仓库，仓库名必须要遵守格式：账户名.github.io，注意：用户名必须正确

#### 2、 设置域名

打开建好的仓库，点击右上角 settings 按钮，打开的页面向下拉到 GitHub Pages 选项，你会看到有个网址， 该地址就是你的博客默认地址，你也可以购买域名，将其换成你自己的地址。

### 二、在你的本地部署 Hexo 环境

Tip：Hexo 的官网：https://hexo.io/zh-cn/

#### 1、搭建 Hexo 需要的环境

你需要在你的电脑上安装 git 和 Node.js，教程就不必过多赘述了，太多这方面的教程，相信这也不难！

#### 2、安装 Hexo

2.1 在你的电脑创建一个文件夹，并用命令执行，进入该文件夹

```
cd Blog
```

2.2 输入 npm install hexo -g，开始安装 Hexo

```
npm install hexo -g
```

2.3 执行完之后，检查是否安装成功

```
hexo -v
```

2.4 初始化 Hexo，过程有点长

```
hexo init
```

初始化完成后，会提示“Start blogging with Hexo！”

2.5 输入 npm install，安装所需要的组件

```
npm install
```

完成到这一步，就可以进入创建博客页面和 创作环节了

### 三、部署到 github 和生成博客页面

#### 1、打通连接 Hexo 和 github 之间的代码传输通道

1.1 设置你的用户名称与邮件地址，如果是第一次使用 git 的话

```
$ git config --global user.name "yourname"
$ git config --global user.email yourname@test.com
```

1.2 使用 ssh-keygen 生成私钥和公钥

```
\$ ssh-keygen -t rsa
```

生成后 会生成两个文件，路径地址执行命令后会提示

1.3 在 Github 页面，点击头像下的 settings 后，页面左侧找到 ssh,并点击，新建一个 new ssh key，将 id_rsa.pub 文件里的内容复制上去。

1.4 添加 ssh 后，输入 ssh -T git@github.com，查看是否成功，如果看到 Hi 后面是你的用户名，就说明成功了

1.5 配置 github 地址

打开 Blog 文件夹下的\_config.yml 文件，拉到最底部，设置你的 github 项目地址和 分支

代码如下：

```

# Deployment

## Docs: https://hexo.io/docs/deployment.html

deploy:
type: git
repository: git@github.com:yourname/yourname.github.io.git
branch: master
```

1.6 hexo 代码 部署到 gitbug ，还需要安装 hexo-deployer-git 插件,

```
npm install hexo-deployer-git --save
```

至此，hexo 代码和 github 的之间的部署通道已经打通了，接下来，就是要利用 hexo 创作文章，生成文件，部署到 gihub 中

#### 2、 新建一篇文章

```
hexo new "postName" #新建文章
```

这时候你会在 Blog 中的 source/\_post 文件夹看到你新建的文件了，这样你就可以打开这个文件进行编辑创作了

新建的文章默认会有一下属性：

---

title: postName #文章页面上的显示名称，一般是中文
date: 2013-12-02 15:30:16 #文章生成时间，一般不改，当然也可以任意修改
categories: 默认分类 #分类
tags: [tag1,tag2,tag3] #文章标签，可空，多标签请用格式，注意:后面有个空格
description: 附加一段文章摘要，字数最好在 140 字以内，会出现在 meta 的 description 里面

---

以下是正文

#### 3、创作好文章好，利用 hexo 生成静态网页

```

hexo g 或者 hexo generate
```

这时候，Blog 目录中 就会出现 public 文件夹，里面就是你生成博客的代码

#### 4、本地预览

```
hexo s 或者 hexo server
```

执行后提示

INFO Start processing
INFO Hexo is running at http://localhost:4000 . Press Ctrl+C to stop.

打开上面的地址，就可以看到你修改的实际效果了

#### 5、代码部署到 github

```
hexo d 或者 hexo deploy
```

执行结果如下：

Enumerating objects: 89, done.
Counting objects: 100% (89/89), done.
Delta compression using up to 4 threads
Compressing objects: 100% (56/56), done.
Writing objects: 100% (67/67), 776.70 KiB | 1.95 MiB/s, done.
Total 67 (delta 7), reused 0 (delta 0)
remote: Resolving deltas: 100% (7/7), done.
To github.com:yourname/yourname.github.io.git
d6d24df..21b213e HEAD -> master
Branch 'master' set up to track remote branch 'master' from 'git@github.com:yourname/yourname.github.io.git'.

则代码部署成功了。

在浏览器打开网址 http:yourname.github.io 就可以看到你自己的博客真面目啦

#### 6、修改主题

6.1、 如果对默认的主题不好看，可以选择自己喜欢的主题，Hexo 在主题方面做的非常强大，访问 https://hexo.io/themes/，网址选择自己的主题

然后点击主题名字，进入到 gihub 的仓库地址,比如我进去的是 Next 主题仓库地址

进入到自己创建的 Blog 文件夹，执行

```
git clone https://github.com/iissnan/hexo-theme-next themes/next #下载 NexT 主题
```

6.2、打开 Blog 文件夹下的\_config.yml 文件，找到 theme 选项,改成自己的主题

````

# Extensions

## Plugins: https://hexo.io/plugins/

## Themes: https://hexo.io/themes/

theme: next
```.

6.3 清楚本地缓存，重新生成静态页面文件,并部署没，最终得到自己主题博客

````

hexo clean
hexo g
hexo s

```.

### 四、 Hexo 的一些常用命令

```

hexo new "postName" #新建文章
hexo new page "pageName" #新建页面

hexo g #enerate 生成静态文件至 public 目录
hexo s #server 启动服务器。默认情况下，访问网址为： http://localhost:4000/
hexo d #deploy 部署网站。部署网站前，需要预先生成静态文件
hexo clean #clean 清除缓存文件 (db.json) 和已生成的静态文件 (public)。

hexo help # 查看帮助
hexo version #查看 Hexo 的版本

```

```
