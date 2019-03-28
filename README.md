## 我的博客
这里是使用 hugo + maupassant 主题搭建的博客，访问路径：[https://itzjm.github.io](https://itzjm.github.io)

### 搭建过程
1. 安装 hugo
我使用的是 mac，windows 下类似。
```sh
brew install hugo
```

检查版本
```sh
hugo version
Hugo Static Site Generator v0.53/extended darwin/amd64 BuildDate: unknown
```

2. 创建 hugo 项目

```sh
localhost:Blog zhangjinmiao$ pwd
/Users/zhangjinmiao/Documents/Blog
localhost:Blog zhangjinmiao$ hugo new site blog
Congratulations! Your new Hugo site is created in /Users/zhangjinmiao/Documents/Blog/blog.

Just a few more steps and you're ready to go:

1. Download a theme into the same-named folder.
   Choose a theme from https://themes.gohugo.io/, or
   create your own with the "hugo new theme <THEMENAME>" command.
2. Perhaps you want to add some content. You can add single files
   with "hugo new <SECTIONNAME>/<FILENAME>.<FORMAT>".
3. Start the built-in live server via "hugo server".

Visit https://gohugo.io/ for quickstart guide and full documentation.
```

3. 添加主题

```sh
localhost:Blog zhangjinmiao$ cd blog/
localhost:blog zhangjinmiao$ ls
archetypes	content		layouts		themes
config.toml	data		static
localhost:blog zhangjinmiao$ git init
Initialized empty Git repository in /Users/zhangjinmiao/Documents/Blog/blog/.git/
localhost:blog zhangjinmiao$ git submodule add https://github.com/itzjm/maupassant-hugo.git themes/maupassant
Cloning into '/Users/zhangjinmiao/Documents/Blog/blog/themes/maupassant'...
remote: Enumerating objects: 45, done.
remote: Counting objects: 100% (45/45), done.
remote: Compressing objects: 100% (31/31), done.
remote: Total 442 (delta 22), reused 28 (delta 14), pack-reused 397
Receiving objects: 100% (442/442), 555.19 KiB | 71.00 KiB/s, done.
Resolving deltas: 100% (244/244), done.
```
主题配置文件 config.toml，参考 GitHub 官方主题样例。

4. 添加内容
blog 根目录执行，my-first-blog.md 自动添加到了 content/post 下。

```sh
localhost:blog zhangjinmiao$ ls
archetypes	content		layouts		static
config.toml	data		resources	themes
hugo new post/my-first-blog.md
/Users/zhangjinmiao/Documents/Blog/blog/content/post/my-first-blog.md created
```

简单编辑下内容。

5. 添加 about 页面

```sh
localhost:blog zhangjinmiao$ pwd
/Users/zhangjinmiao/Documents/Blog/blog
localhost:blog zhangjinmiao$ hugo new about.md
/Users/zhangjinmiao/Documents/Blog/blog/content/about.md created
```
可以看到，about.md 页面在 content 下，也简单编辑下。

6. 运行调试

```sh
hugo server --theme=maupassant --buildDrafts --watch


                   | EN
+------------------+----+
  Pages            |  8
  Paginator pages  |  0
  Non-page files   |  0
  Static files     |  7
  Processed images |  0
  Aliases          |  1
  Sitemaps         |  1
  Cleaned          |  0

Total in 9 ms
Watching for changes in /Users/zhangjinmiao/Documents/Blog/blog/{content,data,layouts,static,themes}
Watching for config changes in /Users/zhangjinmiao/Documents/Blog/blog/config.toml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
```
以上，theme 用于指定主题名，buildDrafts 用于运行 build 草稿，watch 用于监控文件的改动。

启动完毕后可以在浏览器中输入以下命令观察生成的站点

```sh
http://localhost:1313
```


7. 部署到 GitHub

- 首先在 GitHub上创建一个 Repository，命名为： itzjm.github.io (这要和你的baseURL一致。)
- 在本地 blog 根目录下执行以下命令
```sh
 hugo --theme=maupassant --buildDrafts --baseUrl="https://itzjm.github.io/"

 
                   | EN
+------------------+----+
  Pages            |  8
  Paginator pages  |  0
  Non-page files   |  0
  Static files     |  7
  Processed images |  0
  Aliases          |  1
  Sitemaps         |  1
  Cleaned          |  0

Total in 13 ms

```

--buildDrafts 不加会生成无内容的网站
--baseUrl 要和 config.toml 的地址一致。

顺利的话会创建 public 文件（里面的内容就是你要上传的静态网站的文件。）

```sh
$ cd public
$ git init
$ git remote add origin https://github.com/itzjm/itzjm.github.io.git
$ git add -A
$ git commit -m "first commit"
$ git push -u origin master
```

最后，浏览器里访问：[https://itzjm.github.io/](https://itzjm.github.io/) 就可以访问你的博客了