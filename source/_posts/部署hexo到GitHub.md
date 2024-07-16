---
title: 部署hexo到GitHub
tags:
  - Hexo
categories: Hexo
keywords: Hexo
description: 部署hexo到GitHub
cover: 'https://assets.aboutnb.com/hexo_github.jpg'
sticky: 
comments: true
abbrlink: 51fdedbd
date:
---



## 部署hexo到GitHub

---

### 1. GitHub创建个人仓库

首先，你先要有一个[GitHub](https://github.com)账户
注册完登录后，在GitHub.com中看到一个`New repository`,新建仓库

<br/>

创建一个和你用户名相同的仓库，后面加`.github.io`只有这样，将来要部署到`GitHub page`的时候，才会被识别，也就是`xxxx.github.io`，其中`xxx`就是你注册GitHub的用户名。我这里是已经建过了

<br/>

点击`create repository`

### 2. 生成SSH添加到GitHub

回到你的`git bash`中

```bash
git config --global user.name "YourName"
git config --global user.email "YourEmail"
```

这里的`YourName`输入你的GitHub用户名，`YourEmail`输入你的GitHub邮箱。这样[GitHub](https://gtihub.com)才能知道你是不是对应它的账户

输入一下两条命令，检查一下你的用户名和邮箱是否正确

```bash
git config user.name
git config user.email
```

创建SSH,一路回车

```bash
ssh-keygen -t rsa -C "YourEmail"

```

这个时候它会告诉你已经生成了`.ssh`的文件夹。在你的电脑中找到这个文件夹

<br>

`SSH`，简单来讲，就是一个秘钥，其中, `id_rsa`是你这台电脑的私人秘钥，不能给别人看的，`id_rsa.pub`是公共秘钥，可以随便给别人看。把这个公钥放在GitHub上，这样

当你链接GitHub自己的账户时，它就会根据公钥匹配你的私钥，当能够相互匹配时，才能够顺利的通过git上传你的文件到GitHub上

<br>

而后在GitHub的`setting`中，找到`SSH keys`的设置选项，点击`New SSH key`

把你的`id_rsa.pub`里面的信息复制进去

<br>

在`gitbash`中，查看是否成功

```bash
ssh -T git@github.com
```

### 3. 将hexo部署到GitHub

将hexo和GitHub关联起来，也就是将hexo生成的文章部署到GitHub上，打开站点配置文件 `_config.yml`，翻到最后，修改为

YourgithubName就是你的GitHub账户

```bash
deploy:
  type: git
  repo: https://github.com/YourgithubName/YourgithubName.github.io.git
  branch: master
```

这个时候需要先安装`deploy-git` ，也就是部署的命令,这样你才能用命令部署到GitHub。

```bash
npm install hexo-deployer-git --save
```
接上一步之后
```bash
hexo clean
hexo generate
hexo deploy
```
其中 `hexo clean`清除了你之前生成的东西
`hexo generate` 生成静态文章，可以用 `hexo g`缩写
`hexo deploy` 部署文章，可以用`hexo d`缩写

部署完之后打开`http://yourname.github.io` 这个网站看到你的博客了

### 4. 设置个人域名

现在你的个人网站的地址是 `yourname.github.io`，如果觉得这个网址逼格不太够，这就需要你设置个人域名了。但是需要花钱。

注册一个阿里云账户,在阿里云上买一个域名，我买的是 `aboutnb.com`，各个后缀的价格不太一样，比如最广泛的`.com` 和 `.cn`就比较贵。

需要先去进行实名认证,然后在域名控制台中，看到你购买的域名。

点解析进去，添加解析

<br>

登录[GitHub](https://github.com)，进入之前创建的仓库，点击`settings`，设置`Custom domain`，输入你的域名`aboutnb.com`

<br>

然后在你的博客文件`source`中创建一个名为`CNAME`文件，不要后缀。写上你的域名
