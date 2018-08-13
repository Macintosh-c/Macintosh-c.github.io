---
title: hexo+github搭建博客之---多地提交更新博客
date: 2018-08-13 23:46:59
categories: 博客搭建 | blog
tags: blog
---
对于之前的搭建过程不在详述，[写在独立博客开创时](https://macintosh-c.github.io/2018/08/12/%E5%86%99%E5%9C%A8%E7%8B%AC%E7%AB%8B%E5%8D%9A%E5%AE%A2%E5%BC%80%E5%88%9B%E6%97%B6/)里说过，这里主要还是记录一些后续搭建过程中碰到的问题。由于经常会在公司和家两地去更新博文，于是碰到了此篇文章提到的问题，下面是解决过程，个人觉得主要还是对于git的使用理解。

## github搭建hexo博客原理
hexo博客的部署环境目录:
![](https://i.imgur.com/RbL2AQv.png)
hexo博客的目录结构解析：
![](https://i.imgur.com/S8cN7do.png)
上传到github上的文件：
![](https://i.imgur.com/5eQfcks.png)

1. hexo帮助把博客发送到github，同时把md文件转换成网页文件。
2. hexo目录下的文件和github上的文件是不同的，public文件夹的文件通过hexo d 上传到github去了，其他的文件则留在本地目录下。

## 本地github上处理

1. 对username.github.io仓库新建hexo分支，并克隆
在Github的username.github.io仓库上新建一个xxx分支，并切换到该分支，并在该仓库->Settings->Branches->Default branch中将默认分支设为xxx，save保存；然后将该仓库克隆到本地，进入该username.github.io文件目录。
完成上面步骤后，在当前目录使用Git Bash执行git branch命令查看当前所在分支，应为新建的分支xxx。

2. 将本地博客的部署文件拷贝进username.github.io文件目录
先将本地博客的部署文件（Hexo目录下的全部文件，除去图中划红线的不要拷贝）全部拷贝进username.github.io文件目录中去。拷贝之前也可以先删除原来切xxx分支时同步过来的master文件目录（那些文件没有作用）
![](https://i.imgur.com/j5Gsi36.png)
接下来，进入username.github.io文件目录下，将该目录下的全部文件提交到xxx分支，提交之前需注意：
将themes目录以内中的主题的.git目录删除（如果有），因为一个git仓库中不能包含另一个git仓库，提交主题文件夹会失败。
可能有人会问，删除了themes目录中的.git不就不能git pull更新主题了吗，很简单，需要更新主题时在另一个地方git clone下来该主题的最新版本，然后将内容拷到当前主题目录即可

3. 提交hexo分支
执行git add .，git commit -m 'back up hexo files'（引号内容可改），git push即可将博客的hexo部署环境提交到GitHub个人仓库的xxx分支。
master分支和xxx分支各自保存着一个版本，master分支用于保存博客静态资源，提供博客页面供人访问；xxx分支用于备份博客部署文件，供自己维护更新，两者在一个GitHub仓库内互不冲突，完美！
至此，你的博客已经可以在其他电脑上进行同步的维护和更新了

## 异地更新博客
将新电脑的生成的ssh key添加到GitHub账户上
在新电脑上克隆username.github.io仓库的xxx分支到本地，此时本地git仓库处于xxx分支
切换到username.github.io目录，执行npm install(由于仓库有一个.gitignore文件，里面默认是忽略掉 node_modules文件夹的，也就是说仓库的hexo分支并没有存储该目录[也不需要]，所以需要install下)

到这里了就可以开始在自己的电脑上写博客了！

编辑、撰写文章或其他博客更新改动
依次执行git add .、git commit -m 'back up hexo files'（引号内容可改）、git push指令，保证xxx分支版本最新
执行hexo d -g指令（在此之前，有时可能需要执行hexo clean），完成后就会发现，最新改动已经更新到master分支了，两个分支互不干扰！

## 回到本地
** 注意： 每次换电脑进行博客更新时，不管上次在其他电脑有没有更新，最好先git pull**

按照之前的方法写自己博客，
然后将目录切换下username.github.io下，此时需要安装一下npm install，
最后执行hexo g、hexo s、hexo d等命令即可提交成功


