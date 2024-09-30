# Github

> 之前已经使用了很长时间的github了，但还是再记录一下

## 创建一个新的仓库

如果有本地库，名字就填本地的文件名

确认后会看到一个链接：https://github.com/Q1ucheng/git-demo.git，就是远程库的链接

### 创建远程库别名

```bash
PC@LAPTOP-PMEV3U0L MINGW64 /e/桌面/git-demo (master)
$ git remote -v

PC@LAPTOP-PMEV3U0L MINGW64 /e/桌面/git-demo (master)
$ git remote add git-demo https://github.com/Q1ucheng/git-demo.git

PC@LAPTOP-PMEV3U0L MINGW64 /e/桌面/git-demo (master)
$ git remote -v
git-demo        https://github.com/Q1ucheng/git-demo.git (fetch)
git-demo        https://github.com/Q1ucheng/git-demo.git (push)
```

### 本地库代码推送至远程库

`git push <链接或者别名> <branch name>`

```bash
$ git push git-demo master
Enumerating objects: 21, done.
Counting objects: 100% (21/21), done.
Delta compression using up to 20 threads
Compressing objects: 100% (14/14), done.
Writing objects: 100% (21/21), 1.61 KiB | 412.00 KiB/s, done.
Total 21 (delta 7), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (7/7), done.
To https://github.com/Q1ucheng/git-demo.git
 * [new branch]      master -> master
```

现在github仓库中就有本地库的文件了

### 拉取远程库代码到本地

`git pull <链接或者别名> <branch name>`

作为测试，我在github上修改了我的代码，现在远程库与本地库不一致，需要pull远程库到本地

```bash
$ git pull git-demo master
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 960 bytes | 36.00 KiB/s, done.
From https://github.com/Q1ucheng/git-demo
 * branch            master     -> FETCH_HEAD
   b90c9fd..9d26101  master     -> git-demo/master
Updating b90c9fd..9d26101
Fast-forward
 hello.py | 2 ++
 1 file changed, 2 insertions(+)
```

pull可以让远程库与本地库保持同步

### 克隆远程库到本地

`git clone <链接>`

### 团队协作

在github中可以邀请成员加入项目

![](.\pic\image-20240827212408918.png)

邀请成员后，该成员就可以push他的代码了

### 跨团队协作

对于别人的代码，可以fork到自己的库中，此时修改的代码commit后只是更改了fork到自己库中的代码，别人仍然看不到，想让别人看到你的更改就需要pull requests

（可以在pull requests中与原作者“聊天”）