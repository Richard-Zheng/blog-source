---
title: 使用 Hexo 搭建个人博客
date: 2021-07-09 18:00:00
tags: 计算机
---

本文意在简要说明搭建博客的过程，前面会有一些关于基本概念和运作原理的介绍。如果你已经有了一定的背景知识，可以跳到后面阅读。

## 博客怎样工作？

这个博客最早搭建于2019年9月7日。当时我还没有一台能长期开机的服务器（其实现在也没有），所以无意间看到 Hexo 这个博客引擎就被吸引住了，按着说明文档自己一步步搭了下来。其实搭建过程并不需要什么编程知识，只是需要充分的时间和耐心，以及遇到问题就去搜索引擎的反应。为什么 Hexo 的运作不需要服务器呢？其实 Hexo 只干了一件事：把编辑器输出的Markdown文档（Microsoft Word虽然也是这一类文件，但是不被Hexo支持）转换成HTML 5网页（包括HTML、CSS、JavaScript）。而这些网页从此就算「独立」了：不需要与生成它的那台机器相连接，它自己就能在任何能打开它的浏览器上工作，也不需要在任何服务器上运行代码。所以，我们只需要给这些网页找一个「网盘」（前提是得支持Http连接），就能通过访问这个网盘打开网页了。「网盘」也叫静态网站托管服务、OSS等，我使用的 GitHub Pages 就是其中之一。它是完全免费的。

但是需要一台电脑安装Hexo和相关的依赖，并在文章更新时运行一次生成、上传到GitHub还是让你觉得很不爽，怎么办？有没有免费运行Hexo的服务？还真有，那就是这篇文章要说的 GitHub Actions。

## 在本地计算机配置 Hexo 及主题

1. 请参见 [Hexo 文档](https://hexo.io/zh-cn/docs/) 安装 Hexo，并新建一个 Hexo 网站。
2. 之后在网站根目录下运行 `hexo server`，此时访问 http://localhost:4000/，你此时应该能访问一个简单的博客网站。
3. 安装 [NexT 主题](https://theme-next.js.org/docs/) ：`npm install hexo-theme-next`
4. 找到`node_modules/hexo-theme-next/_config.yml`并复制到 Hexo 目录并重命名为`_config.next.yml`（[文档](https://theme-next.js.org/docs/getting-started/configuration.html)）
5. 按照[文档](https://theme-next.js.org/docs/getting-started/#Enabling-NexT)编辑`_config.yml`
6. 继续按照[文档](https://theme-next.js.org/docs/theme-settings/#Choosing-Scheme)编辑`_config.next.yml`（注意此时文档中的`next/_config.yml`应视为`_config.next.yml`）

（可能有些太简略了，待补充）

现在，你已经成功配置好自己的个人博客，在命令行执行`hexo server`即可在本机上运行博客。下一步就是把博客托管至GitHub了。

## 将博客托管到 GitHub Pages

1. 首先你需要[登录](https://github.com/login)自己的 GitHub 账号。如果没有 GitHub 账号，请使用邮箱注册一个。注意，注册时请选一个理想的用户名，因为这将成为你博客域名的一部分：[username].github.io

2. 然后[新建一个 repository](https://github.com/new)，repository name填入`[username].github.io`（username即为注册时填入的用户名），其余保持默认。

3. 参考[此处](https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%88%9D%E6%AC%A1%E8%BF%90%E8%A1%8C-Git-%E5%89%8D%E7%9A%84%E9%85%8D%E7%BD%AE#_%E7%94%A8%E6%88%B7%E4%BF%A1%E6%81%AF)配置 Git 用户信息。请使用你在注册 GitHub 时提供的邮箱和用户名。

4. 配置 Hexo 以将博客部署至 GitHub。打开`_config.yml`并找到下面这块配置（注意编辑repo中的`<username>`）（[文档](https://hexo.io/zh-cn/docs/github-pages#%E7%A7%81%E6%9C%89-Repository)）

   ```yaml
   deploy:
     type: git
     repo: https://github.com/<username>/<username>.github.io
     # example, https://github.com/hexojs/hexojs.github.io
     branch: gh-pages
   ```

5. 运行 `hexo clean && hexo deploy` ，输入 GitHub 用户名和密码。

6. 进入repository页面，点击 Settings - pages，确保已启用 GitHub Pages。此时`https://<username>.github.io`应已可以访问。

## 使用 GitHub Actions 部署博客

1. 登录GitHub，再新建一个repository。名字可以自己取，我的是`blog-source`。

2. 新建文件`博客目录/.github/workflows/deploy.yml`，内容如下：（注意替换`<username>`及`<useremail>`）

   ```yaml
   name: Deploy blog to Github
   on: [workflow_dispatch]
   jobs:
     build:
       runs-on: ubuntu-latest
       steps:
       - name: Checkout
         uses: actions/checkout@v1
       - name: Checkout GitHub Pages repository
         uses: actions/checkout@v2
         with:
           repository: '<username>/<username>.github.io'
           path: '.deploy_git'
       - name: Setup Node.js environment
         uses: actions/setup-node@v2-beta
         with:
           node-version: '12'
       - name: Install pandoc (Latex support)
         run: |
           wget -O pandoc.deb https://github.com/jgm/pandoc/releases/download/2.13/pandoc-2.13-1-amd64.deb
           sudo dpkg -i pandoc.deb
       - name: Setup Hexo environment
         run: npm install
   
       # 从之前设置的 secret 获取部署私钥
       - name: Set up environment
         env:
           DEPLOY_KEY: ${{ secrets.DEPLOY_KEY }}
         run: |
           sudo timedatectl set-timezone "Asia/Shanghai"
           mkdir -p ~/.ssh
           echo "$DEPLOY_KEY" > ~/.ssh/id_rsa
           chmod 600 ~/.ssh/id_rsa
           ssh-keyscan github.com >> ~/.ssh/known_hosts
           git config --global user.email "<useremail>"
           git config --global user.name "<username>"
       # 生成并部署
       - name: Deploy
         env:
           MESSAGE: ${{ format('Site updated {0}@{1}', github.repository, github.sha) }}
         run: |
           npx hexo deploy --generate --message "$MESSAGE"
   ```
   
4. 修改`博客目录/.gitignore`在最后一行添加`package-lock.json`

5. 在博客目录下运行

   ```bash
   git init
   git add --all
   git commit -m "first commit"
   git branch -M main
   git remote add origin https://github.com/<username>/blog-source.git
   git push -u origin main
   ```

5. 生成SSH密钥：`ssh-keygen -f hexo-deploy-key`一路回车即可
6. 记事本打开 `hexo-deploy-key.pub` ，将里面的内容设置为仓库`<username>.github.io`的部署密钥（Settings > Deploy keys）
7. 在仓库`blog-source`的 Settings > Secrets 中新增一个 secret，命名为 `DEPLOY_KEY`，把私钥 `hexo-deploy-key` 的内容复制进去。
8. 最后点击`blog-source`的Actions > Deploy blog to Github > Run workflow

## 参考

- [使用 GitHub Actions 自动部署 Hexo 博客](https://printempw.github.io/use-github-actions-to-deploy-hexo-blog/)

