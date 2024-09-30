# Git

> Git是一个免费的开源的分布式版本控制系统，可以快速高效地处理从小型到大型的项目

版本控制是一种记录文件内容变化，以便将来查阅特定版本修订情况的系统（可以查看历史版本）

## Git工作机制

```mermaid
graph LR
  A[工作区] -->|git add| B[暂存区];
  B --> |git commit| C[本地库];
  C --> |push| D[远程库]
```

## git 常用命令

| 命令                        | 作用描述                                     |
| --------------------------- | -------------------------------------------- |
| `git init`                  | 初始化一个新的Git仓库                        |
| `git clone <repository>`    | 克隆一个远程Git仓库到本地                    |
| `git status`                | 查看当前工作区的状态                         |
| `git add <file>`            | 将指定文件添加到暂存区                       |
| `git commit -m "<message>"` | 将暂存区的内容提交到本地仓库，并添加提交信息 |
| `git reflog`                | 查看历史版本                                 |
| `git reset --hard <版本号>` | 版本穿梭                                     |

### 设置签名

首次安装需要设置用户签名

```bash
$ git config --global user.name Wayne
$ git config --global user.email zhaoqiucheng21@gmail.com
```

### 初始化本地库

对项目使用`git init`初始化生成`.git`文件

```bash
$ git init
Initialized empty Git repository in E:/git-demo/.git/
```

查看本地库

```bash
$ git status
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

告诉了所在分支（默认为master），没有commit的记录，没有需要commit的东西

现在用vim写一个文件后再执行`git status`

```bash
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        hello.py

nothing added to commit but untracked files present (use "git add" to track)
```

告诉了我有文件未被git追踪，也就是要添加到暂存区

```bash
$ git add hello.py
warning: in the working copy of 'hello.py', LF will be replaced by CRLF the next time Git touches it
```

提示我git自己更改了换行符，再次查看日志

```bash
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   hello.py
```

现在git已经追踪到文件了，想删除暂存区中的文件可以使用`git rm --cached <file>`（注意工作区中的文件仍然还在）

```bash
PC@LAPTOP-PMEV3U0L MINGW64 /e/git-demo (master)
$ git rm --cached hello.py
rm 'hello.py'

PC@LAPTOP-PMEV3U0L MINGW64 /e/git-demo (master)
$ git status
On branch master
No commits yet
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        hello.py
nothing added to commit but untracked files present (use "git add" to track)
```

### 提交本地库

`git commit -m "提交信息" <文件名>`

```bash
$ git commit -m "My first commit" hello.py
warning: in the working copy of 'hello.py', LF will be replaced by CRLF the next time Git touches it
[master (root-commit) de7a558] My first commit
 1 file changed, 9 insertions(+)
 create mode 100644 hello.py
```

其中`de7a558`为版本号，此时的日志为：

```bash
$ git status
On branch master
nothing to commit, working tree clean
```

可以`git reflog`或`git log`（更详细的信息）查看历史版本信息

```bash
$ git reflog
de7a558 (HEAD -> master) HEAD@{0}: commit (initial): My first commit
$ git log
commit de7a558a768c46e32e54a297255c27a8bd967d9e (HEAD -> master)
Author: Wayne <zhaoqiucheng21@gmail.com>
Date:   Tue Aug 27 17:01:45 2024 +0800

    My first commit
```

修改文件后再提交：

```bash hl_lines="18"
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   hello.py

no changes added to commit (use "git add" and/or "git commit -a")

PC@LAPTOP-PMEV3U0L MINGW64 /e/桌面/git-demo (master)
$ git add hello.py
warning: in the working copy of 'hello.py', LF will be replaced by CRLF the next time Git touches it

PC@LAPTOP-PMEV3U0L MINGW64 /e/桌面/git-demo (master)
$ git commit -m "add something" hello.py
warning: in the working copy of 'hello.py', LF will be replaced by CRLF the next time Git touches it
[master e36164f] add something
 1 file changed, 1 insertion(+), 1 deletion(-)
```

告诉我一个文件有更改，一行新增一行删除（git删去原来的行再新增修改的行），此时再执行`git relog`可以看到指针指向的是最新的文件：（工作区中呈现的文件是指针指向的文件，用`cat`查看文件也会呈现出指针指向的文件）

```bash
$ git reflog
e36164f (HEAD -> master) HEAD@{0}: commit: add something
de7a558 HEAD@{1}: commit (initial): My first commit
```

### 历史版本的相关操作

使用`git reset --hard <版本号>`穿梭到指定历史版本

```bash hl_lines="8 13 15"
PC@LAPTOP-PMEV3U0L MINGW64 /e/git-demo (master)
$ git reflog
ca2dd4d (HEAD -> master) HEAD@{0}: commit: add something again
e36164f HEAD@{1}: commit: add something
de7a558 HEAD@{2}: commit (initial): My first commit

PC@LAPTOP-PMEV3U0L MINGW64 /e/git-demo (master)
$ git reset --hard e36164f
HEAD is now at e36164f add something

PC@LAPTOP-PMEV3U0L MINGW64 /e/git-demo (master)
$ git reflog
e36164f (HEAD -> master) HEAD@{0}: reset: moving to e36164f
ca2dd4d HEAD@{1}: commit: add something again
e36164f (HEAD -> master) HEAD@{2}: commit: add something
de7a558 HEAD@{3}: commit (initial): My first commit
```

此时`cat`查看的文件就是指定历史版本了，工作区的文件也变成了历史版本

现在就可以体现出git的工作原理了：**Git通过指针管理各个版本的引用信息，并使用快照的方式存储文件的内容。不同于传统的版本控制系统通过保存每个版本的完整副本，Git通过存储每次提交的快照和文件差异来实现版本的管理和回溯。**

### git的分支操作

有了分支的操作，开发者就可以将自己的工作从主线上分离开来，开发自己的分支时不会影响主线的运行

| 命令                         | 作用                       |
| ---------------------------- | -------------------------- |
| `git branch`                 | 创建分支                   |
| `git branch -v`              | 查看分支                   |
| `git checkout <branch name>` | 切换分支                   |
| `git merge <branch name>`    | 把指定分支合并到当前分支上 |

从创建分支到在新分支上修改文件并commit

```bash hl_lines="10 11"
PC@LAPTOP-PMEV3U0L MINGW64 /e/桌面/git-demo (master)
$ git branch hot-fix

PC@LAPTOP-PMEV3U0L MINGW64 /e/桌面/git-demo (master)
$ git branch -v
  hot-fix ca2dd4d add something again
* master  ca2dd4d add something again

PC@LAPTOP-PMEV3U0L MINGW64 /e/桌面/git-demo (master)
$ git checkout hot-fix
Switched to branch 'hot-fix'

PC@LAPTOP-PMEV3U0L MINGW64 /e/桌面/git-demo (hot-fix)
$ vim hello.py

PC@LAPTOP-PMEV3U0L MINGW64 /e/桌面/git-demo (hot-fix)
$ git add hello.py

PC@LAPTOP-PMEV3U0L MINGW64 /e/桌面/git-demo (hot-fix)
$ git commit -m "add something on hotfix branch" hello.py
[hot-fix 95eb457] add something on hotfix branch
 1 file changed, 1 insertion(+), 1 deletion(-)

PC@LAPTOP-PMEV3U0L MINGW64 /e/桌面/git-demo (hot-fix)
$ git reflog
95eb457 (HEAD -> hot-fix) HEAD@{0}: commit: add something on hotfix branch
ca2dd4d (master) HEAD@{1}: checkout: moving from master to hot-fix
ca2dd4d (master) HEAD@{2}: reset: moving to ca2dd4d
e36164f HEAD@{3}: reset: moving to e36164f
ca2dd4d (master) HEAD@{4}: commit: add something again
e36164f HEAD@{5}: commit: add something
de7a558 HEAD@{6}: commit (initial): My first commit
```

将hot-fix分支合并到master分支上（需要先将当前分支切换为master）

```bash
$ git merge hot-fix
Updating ca2dd4d..95eb457
Fast-forward
 hello.py | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```

此时master分支上的文件就有了hot-fix分支上的修改

但合并分支时，如果两个分支在同一文件同一位置有不同的修改，git无法替我们决定使用哪一个，就需要人工介入

我修改了master分支下的第六行，再修改了hot-fix分支下的第七行，将hot-fix合并到master时产生了冲突：

```bash
$ git merge hot-fix
Auto-merging hello.py
CONFLICT (content): Merge conflict in hello.py
Automatic merge failed; fix conflicts and then commit the result.
```

而且此时的分支名也变成了`master|MERGING`，查看文件

```python
print('hello!')
print('hello!')
print('hello python!')
print('hello world!')
print('hello!')
<<<<<<< HEAD
print('hello!')
print('hello master test!')
=======
print('hello! hotfix test')
print('hello!')
>>>>>>> hot-fix
print('hello!')
print('hotfix!')
```

此时git已经标记出了冲突的位置，需要手动修改为我们希望的样子，最后`add`和`commit`

**注意：现在的`commit`不能加文件名，否则会报错**

```bash hl_lines="8"
PC@LAPTOP-PMEV3U0L MINGW64 /e/git-demo (master|MERGING)
$ git add hello.py

PC@LAPTOP-PMEV3U0L MINGW64 /e/git-demo (master|MERGING)
$ git commit -m "merge test"
[master b90c9fd] merge test

PC@LAPTOP-PMEV3U0L MINGW64 /e/git-demo (master)
```





