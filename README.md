# Macintosh-c.github.io

新建了hexo分支，用于上传hexo原始文件，已支持多地更新博文

在github上将分支默认设为hexo，并在新的地方 进行clone，clone下来后记得npm install安装依赖包，(由于仓库有一个.gitignore文件，里面默认是忽略掉 node_modules文件夹的，也就是说仓库的hexo分支并没有存储该目录[也不需要]，所以需要install下)，这样就可以像原来一样正常更新修改博文，hexo d发布前将本次修改记录提交到hexo分支，然后hexo d发布到master分支，下次在其他地方更新博文前记得git pull 一下hexo分支，保持最新状态，然后正常操作。

在没有环境的pc上首先要配置环境，github添加ssh等等
