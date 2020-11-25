# Git
## 基本信息
1. 分布式版本控制系统
2. 工作区：电脑可以看到的目录
3. 版本库/仓库（repository）: .git目录 = 暂存区 + 分支（+指针）
4. 版本控制系统只能追踪文本文件的改动（建议使用UTF-8编码）

## 操作指南
### 安装Git
#### Linux
```
# Debian/Ubuntu
$ sudo apt-get install git
```
#### MacOS
1. 通过homebrew安装
2. 安装Xcode
#### Windows
1. Git官网下载
2. 在Git Bash中输入
   ```
   $ git config --global user.name "Yiming Shi"
   $ git config --global user.email "812878146@qq.com"
   ```

### 初始化仓库
```
# 把当前目录变成Git可管理的仓库
$ git init
Initialized empty Git repository in C:/Data/Others/Study/Git/learngit/.git/

# 当前目录下会多出一个.git目录
$ ls -a
./  ../  .git/
```

### 添加文件到仓库
```
$ git add readme.txt
$ git commit -m "wrote a readme file"
[master (root-commit) 8a9a9f6] wrote a readme file
 1 file changed, 2 insertions(+)
 create mode 100644 readme.txt
# 'git add'提交文件到暂存区
# 'git commit'提交暂存区的所有修改
```

### 删除文件
```
$ git rm test.txt
rm 'test.txt'
$ git commit -m "remove test.txt"
```

### 撤销修改
```
$ git checkout -- readme.txt
# 修改文件后未添加到暂存区，回到版本库的状态
# 文件已经添加到暂存区且又作了修改，回到到暂存区的状态

# 文件修改后已经添加到暂存区，把暂存区修改退回到工作区
$ git reset HEAD readme.txt
[master ba0cccc] remove test.txt
 1 file changed, 0 insertions(+), 0 deletions(-)
 delete mode 100644 test.txt
```

### 版本回退
```
# 回退后'git log'将看不到“未来的”版本
# 回退到上一个版本
$ git reset --hard HEAD^

# 回退到上上个版本
$ git reset --hard HEAD^^

# 回退到上100个版本
$ git reset --hard HEAD~100

# 回退到指定版本
$ git reset --hard 版本号
```

### 查看文件的修改内容
``` 
git diff readme.txt
diff --git a/readme.txt b/readme.txt
index d8036c1..013b5bc 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,2 +1,2 @@
-Git is a version control system.
+Git is a distributed version control system.
 Git is free software.
\ No newline at end of file
```

### 查看仓库当前状态
```
# 仅修改readme.txt后
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")

# 'git add'后未'git commit'
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   readme.txt

# 'git commit'后
$ git status
On branch master
nothing to commit, working tree clean

# 'git merge'发生冲突时
$ git status
On branch master
Your branch is ahead of 'origin/master' by 2 commits.
  (use "git push" to publish your local commits)

You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

### 查看历史记录（看不到“未来”）
```
$ git log
commit 3b8485d8772199a721d9818fd43d09b208edda48 (HEAD -> master)
Author: Yiming Shi XiaoXinAir14 <812878146@qq.com>
Date:   Wed Nov 25 10:58:30 2020 +0800

    append GPL

commit b0478a529287e7f61b1dcd7e5b04392596d7ca47
Author: Yiming Shi XiaoXinAir14 <812878146@qq.com>
Date:   Wed Nov 25 10:56:15 2020 +0800

    add distributed

commit 8a9a9f6863c307b16a4d0e944dc14d172d0a7447
Author: Yiming Shi XiaoXinAir14 <812878146@qq.com>
Date:   Wed Nov 25 10:47:04 2020 +0800

    wrote a readme file

# 仅查看重要信息
$ git log --pretty=oneline
3b8485d8772199a721d9818fd43d09b208edda48 (HEAD -> master) append GPL
b0478a529287e7f61b1dcd7e5b04392596d7ca47 add distributed
8a9a9f6863c307b16a4d0e944dc14d172d0a7447 wrote a readme file

# 查看分支的合并情况
$ git log --graph --pretty=oneline --abbrev-commit
*   c3b1ee7 (HEAD -> master) confilct fixed
|\
| * 5eb0c41 (feature1) AND simple
* | f683962 & simple
|/
* 6e77e44 branch test
* ba0cccc (origin/master) remove test.txt
* 1a5ef4a add test.txt
* 1449590 changes of files
* 78c75c3 git track changes
* a020c17 understand how stage works
* 3b8485d append GPL
* b0478a5 add distributed
* 8a9a9f6 wrote a readme file
```

### 查看每一次命令
```
$ git reflog
3b8485d (HEAD -> master) HEAD@{0}: reset: moving to 3b84
b0478a5 HEAD@{1}: reset: moving to HEAD^
3b8485d (HEAD -> master) HEAD@{2}: commit: append GPL
b0478a5 HEAD@{3}: commit: add distributed
8a9a9f6 HEAD@{4}: commit (initial): wrote a readme file
```

### 创建新的分支
```
# 创建并切换到dev分支
$ git checkout -b dev

# 与上述操作等价
$ git branch dev
$ git checkout dev

# 或者
$ git switch -c dev
```

### 切换分支
```
$ git checkout dev

# 或者
$ git switch dev
```

### 查看当前分支
```
$ git branch
* dev
  master
```

### 复制提交
```
# 复制特定的提交到当前的分支（在当前分支上做一次提交）
$ git cherry-pick 4c805
```

### 合并分支
```
# 把dev分支合并到当前分支
$ git merge dev

# 发生冲突时
$ git merge feature1
Auto-merging readme.txt
CONFLICT (content): Merge conflict in readme.txt
Automatic merge failed; fix conflicts and then commit the result.

# 强制禁用'Fast forward'模式
$ git merge --no-ff -m "merge with no-ff" dev
Merge made by the 'recursive' strategy.
 readme.txt | 3 ++-
 1 file changed, 2 insertions(+), 1 deletion(-)
```

### 删除分支
```
$ git branch -d dev
```

### 隐藏分支（[bug分支](https://www.liaoxuefeng.com/wiki/896043488029600/900388704535136)）
```
# 隐藏当前分支
$ git stash

# 查看隐藏的分支
$ git stash list

# 恢复隐藏的分支并删除stash中内容
$ git stash apply stash@{0}
$ git stash drop stash@{0}

# 与上一个操作等价
$ git stash pop
```

### 整理提交历史
```
$ git rebase
```

## [多人协作模式](https://www.liaoxuefeng.com/wiki/896043488029600/900375748016320)
>首先，可以试图用git push origin <branch-name>推送自己的修改；<br>
如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；<br>
如果合并有冲突，则解决冲突，并在本地提交；<br>
没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！<br><br>
P.S. 如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。

### 关联远程仓库
```
$ git remote add origin git@github.com:NO11s/learngit.git
$ git push -u origin master
# 由于远程库为空，第一次推送master分支时加上了'-u'参数
```

### 关联远程分支与本地分支
```
$ git branch --set-upstream-to=origin/dev dev

# 若本地没有dev分支
$ git checkout -b dev origin/dev
```

### 推送本地master分支
```
$ git push origin master
```

### 抓取远程库
```
$ git pull
```

### 从远程库克隆一个本地库
```
$ git clone git@github.com:NO11s/gitskills.git
```

### 查看远程库的信息
```
$ git remote

# 查看更详细的信息
$ git remote -v
```

### 打标签
```
# 在当前commit打标签
$ git tag v1.0

# 给特定commit打标签
$ git tag v0.9 f52c6

# 查看所有标签
$ git tag

# 查看标签信息
$ git show <tagname>
```

### 删除标签
```
$ git tag -d v0.1

# 若要从远程删除，需要再加上
$ git push origin :refs/tags/v0.1
```

### 推送标签到远程
```
$ git push origin <tagname>

# 一次性推送全部未推送到远程的本地标签
$ git push origin --tags
```

### 让Git显示颜色
```
$ git config --global color.ui true
```

### 忽略特殊文件
1. 创建.gitignore文件
2. 书写.gitignore文件（[各种配置文件](https://github.com/github/gitignore)）

### 配置别名
```
$ git config --global alias.st status
$ git config --global alias.ci commit
$ git config --global alias.unstage 'reset HEAD'
```