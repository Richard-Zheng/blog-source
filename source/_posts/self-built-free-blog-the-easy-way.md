---
title: 零编程基础自建免费博客指南
date: 2021-11-29 12:12:00 +08:00
tags: 
mathjax: true
---

本文的标题中强调了“零基础”，但是你仍然需要用到一些常见的开发工具。但请放心，上手使用这些工具并不难！这只需要你有足够的耐心，和一定的信息搜索能力。另外，如果能稍微了解一下原理而不是不求甚解拿来就用，那么维护博客对你来说就更不是件难事。

## 从这里开始

Hexo 使用 Markdown 作为文章的格式，所以你需要了解 [Markdown 标记语言](https://www.runoob.com/markdown/md-tutorial.html) 并选择一个趁手的 Markdown 编辑器。这方面的选择很多，我个人以前一直在用 Typora，但是最近它开始收费了。所以我推荐你用开源的在线 Markdown 编辑器 [Arya](https://markdown.lovejade.cn/?utm_source=markdown.lovejade.cn&pid=about-arya). 即时预览的界面用起来几乎把学习成本降到了最低。

### 原理

为什么 Hexo 的运作不需要服务器呢？其实 Hexo 只干了一件事：把编辑器输出的 Markdown 文档（Microsoft Word 虽然也是这一类文件，但是不被 Hexo 支持）转换成 HTML 5 网页（包括 HTML、CSS、JavaScript）。而这些网页从此就算「独立」了：不需要与生成它的那台机器相连接，它自己就能在任何能打开它的浏览器上工作，也不需要在任何服务器上运行代码。所以，我们只需要给这些网页找一个「网盘」（前提是得支持 HTTP 连接），就能通过访问这个网盘打开网页了。

而是谁运行 Hexo，编译输出网页呢？我们这里用的是 Cloudflare 免费提供的自动构建服务器。你也可以在你自己的计算机上做这个事情，具体操作请看 Hexo 官方文档。

## 注册

你需要在两个地方注册账号：

- [GitHub](https://github.com/join)：与 Git 深度集成，用于存放博客源代码库。
- [Cloudflare](https://dash.cloudflare.com/sign-up)：用于托管编译出的博客。

这两者都只需要邮箱注册。另外尽管这次使用 Cloudflare 提供的托管服务，GitHub 同样也有类似的 GitHub Pages，而它提供的域名其中一部分将是你的用户名。加上用户名注册后不可更改，建议你选一个你喜欢的、好记且好输入的用户名。

## 配置

注册完成之后请打开我预先准备好的 [模板](https://github.com/Richard-Zheng/hexo-next-starter)。然后点击 Use this template，填入你的存储库名称（如 `blog-source`）然后直接点击 Create repository from template.

登入 Cloudflare 控制台，点击右边栏的 Pages，然后点击 Create a project. 再下一个页面中点击 Connect GitHub，授权访问你刚刚创建的存储库（或者所有存储库）。再次回到创建 project 的页面，选中你的存储库并下一步。

- 在 Project name 中填入你博客的名字（将成为你博客域名中的一部分，所以建议你选一个你喜欢的、好记且好输入的名字）
- 在 Build command 中填入 `npm run build`
- 在 Build output directory 中填入 `public`

其他都保持默认，点击 Save and deploy.

等2到3分钟后，访问 `[名字].pages.dev`，看看博客是不是已经出现了？

## 自定义

Hexo 的配置是用 [YAML 格式](https://www.runoob.com/w3cnote/yaml-intro.html) 写的。所以简单了解一下它的格式会极大地帮助你修改配置以及减少出错概率。但是目前来说，你只需要记住以下几点：

- 数据之间的层级关系是通过缩进来体现的，所以你必须严格遵守缩进，且只能使用空格。
- 单个配置值使用冒号结构表示 `key: value`，注意冒号后有一个空格。
- `#` 开头的为注释

准备好后打开你刚刚在 GitHub 上创建的博客存储库，点开主目录下的 `_config.yml` 文件，然后在文件内容上方的右侧找到修改按钮（图标为一支笔）点开。

这时你就在修改你的 Hexo 配置文件了，这个配置文件的详细说明文档在 [此处](https://hexo.io/zh-cn/docs/configuration.html)。但如果你没有额外要求，只用改以下几个部分：

- `title` 网站标题
- `subtitle` 网站副标题（可选）
- `author` 你的名字
- `url` 填入`[名字].pages.dev`

填好以后直接点击 Commit changes 提交更改。

可选：然后重复相同的步骤，修改 `_config.next.yml` 文件，这是主题的配置文件。详细文档在 [此处](https://theme-next.js.org/docs/getting-started/configuration)。你可以参考 [文档](https://theme-next.js.org/docs/theme-settings/#Choosing-Scheme) 挑选一个你喜欢的主题。在大多数情况下，你不需要修改其它的配置。

修改完以后过2到3分钟再次访问你的博客，看看有什么变化？

## 写作

你的文章存放在 `source/_posts` 目录中，修改文章的方式和修改配置基本相同，但是有一点需要注意：每个文章开头都会有这一段：

```
---
title: Hello World
date: 2021-01-01 00:00:00 +08:00
tags: [标签1,标签2,标签3]
mathjax: true
---
```

这个叫做 YAML front matter，其实就是在 Markdown 文件头部加了一段 YAML 格式的配置/说明。你需要注意的是如果文章中有数学公式需要加上一行 `mathjax: true`。

小技巧：Hexo 会使用每篇文章的文件名作为它的 URL，但是中文出现在 URL 中很不美观，你可以把文章英文名作为 Markdown 文件的名字（全部小写，空格换成短横线，如 `hello-world`），然后在 `title: 你好世界` 这里写这篇文章的中文名。实际页面中文章的名字全部取决于这个 `title` 的值。

如果要新建一篇文章，你可以导航到 `source/_posts` 目录，然后点击 Add file，选择创建新文件（直接在网页编辑）或是从本地上传 Markdown 文件。

每次博客存储库有更改，在2到3分钟后网站即会更新。