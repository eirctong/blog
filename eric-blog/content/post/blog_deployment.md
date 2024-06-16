+++
title = 'Blog_Deployment'
date = 2024-06-16T02:26:22+08:00
draft = false
+++
GitHub Pages + Hugo 搭建个人博客

# 1. 仓库内容


## 1.1 文件git init详细说明
```python
目前存在的仓库
~ is /Users/bytedance/Library/Mobile Documents/com~apple~CloudDocs/Desktop/eric_blog/
```

### erictong.github.io
https://github.com/eirctong/eirctong.github.io 

GitHub Pages 仓库：储存由 Hugo 从Markdown 文件生成的 HTML 文件；用于一组静态网页集合（Static Web Page），这些静态网页由 GitHub 托管（host）和发布，所以是 GitHub + Pages


```python
init directory is ~/blog/eric_blog/public
```

### blog

https://github.com/eirctong/blog

```python
init directory is ~/blog
```

博客源仓库：储存所有 Markdown 源文件（博客内容），和博客中用到的图片等

# 2. deployment
```python
# 进入blog的路径 启动hugo server 在本地检查markdown转换成html有无问题
cd /Users/bytedance/Library/Mobile Documents/com~apple~CloudDocs/Desktop/eric_blog/blog/eric-blog
hugo server # try http://localhost:1313/
hugo new post/xxx.md


# push所有内容到博客源仓库,用于远程备份
# 如果没有把博客源文件推送到远端仓库备份，假设你丢失了本地文件（比如电脑坏了），那只根据public文件夹中的内容是很难复原你的所有博客内容的
cd /Users/bytedance/Library/Mobile Documents/com~apple~CloudDocs/Desktop/eric_blog/blog
git stash -u
git pull --rebase origin main
git stash pop
git add .
git commit -m "feat(init deploy): test publish"
git push


# 向GitHub Pages 推送, 静态网页资源将会Automatic Action
hugo # 通过 hugo 命令生成静态网页文件,会修改toml中的baseurl所关联的html中的item
cd blog/eric-blog/public
git stash -u
git pull --rebase origin main
git stash pop
git add .
git commit -m "feat(update blog): push blog"
git push
# try https://eirctong.github.io/
```