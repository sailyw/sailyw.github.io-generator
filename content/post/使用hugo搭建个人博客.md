---
title: "使用hugo搭建个人博客"
date: 2020-04-20T14:50:17+08:00
draft: false
---

1.首先到[Hugo releases 页面](https://github.com/gohugoio/hugo/releases)下载，由于我的电脑是 windows64 位,大家可以按需选择要下载的是 32 位还是 64 位。最好将解压后的 hugo.exe 放到 E:\software\hugo\hugo.exe 下，并且将 E:\software\hugo 加入到环境变量中，然后启动终端，运行`hugo version`查看版本，是否安装成功。

![](/imgs/使用hugo搭建个人博客/download.png)

2.进入[hugo 官网](https://gohugo.io/)点击 get started，进入后，由于第一步安装已经完成了，从第二步开始走，选择一个安全的文件夹，在终端中执行下面代码。

![](/imgs/使用hugo搭建个人博客/getStarted.png)

```
# sailyw是我的github名称，名字为博客生成器
hugo new site sailyw.github.io-creator
# add a theme
cd sailyw.github.io-creator
git init
git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke
echo 'theme = "ananke"' >> config.toml
# 开始第一篇文章编写
hugo new posts/my-first-post.md
```

3.这时，我们的第一篇文章就已经创建了，存放在了 sailyw.github.io-creator\content\posts 中了，其中默认 draft:true 为草稿状态，当写完后文章后，应该 true 改成 flase，便不为草稿状态。

```
---
title: "My First Post"
date: 2019-03-26T08:47:11+01:00
draft: true
---
```

4.在终端输入下列命令，会得到一个http://localhost:1313/网址，按CTRL键+鼠标就可以进行访问了。

```
hugo server -D
```

![](/imgs/使用hugo搭建个人博客/localhost1313.png)

![](/imgs/使用hugo搭建个人博客/myNewBlog.png)

5.进行网站配置，进入 config.toml，修改标题

```
baseURL = "http://example.org/"
languageCode = "zh-Hans"
title = "Sailyw的博客"
theme = "ananke"
```

![](/imgs/使用hugo搭建个人博客/settings.png)

6.建立静态页面,此时出现了 public 文件夹

```
hugo -D
```

7.挂载到 github 上，首先新建.gitignore，将`/public/`写入其中，也就是当前仓库自成一个仓库。然后执行以下代码。

```
cd public
git init
git add .
git commit -v
```

8.进入[github 官网](https://github.com/)，新建一个仓库，仓库名必须是你的 github 名.github.io，例如我自己的 sailyw.github.io，然后在终端 public 中输入

```
git remote add origin git@github.com:xxx/xxx.github.io.git
git push -u origin master
```

9.接下来，我们可以点击该仓库的 settings 下的 GitHub Pages 下的地址访问到我们的博客挂在了 github 上，如果没有出现，可以看到下面有个 master 按钮，选中即可。然后点击下面的链接，便可看到之前的博客网站。

![](/imgs/使用hugo搭建个人博客/gitpages.png)

10.如果不想使用系统默认的主题，可以在 step3 中，点击红框圈住的链接，接着点击 homepage，进入 public 上一级目录运行。本次博客使用的主题是[Jane](https://github.com/xianmin/hugo-theme-jane/blob/master/README-zh.md)

![](/imgs/使用hugo搭建个人博客/addATheme.png)

![](/imgs/使用hugo搭建个人博客/homepage.png)

```
git clone https://github.com/xianmin/hugo-theme-jane.git --depth=1 themes/jane
cp -r themes/jane/exampleSite/content ./
cp themes/jane/exampleSite/config.toml ./
hugo server
```

11.配置

- 进行汉化

```
# language support # en / zh-cn / other... translations present in i18n/
defaultContentLanguage = "zh-cn"           # Default language to use
[languages.zh-cn]
  languageCode = "zh-cn"
```

- 改变作者名

```
[author]                  # essential                     # 必需
  name = "sailyw"
```

12.上传

```
hugo
cd public
git push
```
