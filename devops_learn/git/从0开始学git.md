# 从0开始学git

既然要记录整个devops的学习与实践过程，那么git是不得不学的。 记得刚毕业那会，我也会使用git。大学期间做项目。也会使用SVN。

那时候，认识还比较浅显。觉得他们两个都差不多，用来多人协同开发的。每天我只需要，推代码和拉取代码就可以了。还特别害怕又代码冲突。因为不好解决。虽然吭哧吭哧也解决了。回想以前，还真是听菜鸟的。



## 认识版本控制

什么是版本控制？

版本控制是指对软件开发过程中各种程序代码、配置文件及说明文档等文件变更的管理，是软件配置管理的核心思想之一。（百度百科）

版本控制的常用工具：SVN、Git

### Git

Git 是一个开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。Git 是 Linus Torvalds 为了帮助管理 Linux 内核开发而开发的一个开放源码的版本控制软件。(所以下面使用windows安装的git的时候，通过git bash可以使用shell命令访问我们电脑的所有文件和目录)

### SVN

是一个集中式的版本控制系统，通过单一的服务器**存储所有文件**修订版本的方式。所有客户端连接该服务器，取出文件或者更新的内容文件。

### Git与SVN的区别

- Git是分布式的，SVN不是
- Git通过元数据存储文件，Git内容存储通过哈希算法（SHA-1），这样可以确保内容的完整性。SVN是按文件进行存储
- Git没有一个全局的版本号，而SVN有
- 分支概念不同，SVN是版本的另一个目录（比较占资源），Git的分支是指向提交的commitId的指针

#### 说一下SVN集中式与GIT分布式

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200321214519512.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM5MzE2ODQ4,size_16,color_FFFFFF,t_70)

集中式：指的是存在服务端和客户端。服务端充当中央代码库。客户端从服务端中获取代码。

分布式：Git的分布式，没有服务端和客户端之分，所谓的服务端就是安装了Git的服务器。因此就没有服务端和客户端之分。

## Git学习

### 基本概念

- **工作区：**   就是我们安装在电脑上，能清晰的看到的目录。目录中能看到具体的文件内容，可以进行编辑、删除等等操作。

- **暂存区:**  暂存区，英文就是stage或者index。存在工作区目录下".git"下的index文件中

- **版本库:** 工作区目录下".git"目录不属于工作区，而是Git的版本库

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200321214550320.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM5MzE2ODQ4,size_16,color_FFFFFF,t_70)

### 安装Git

使用Git之前，需要先安装Git。

Git各平台安装包下载地址：[ http://git-scm.com/downloads]( http://git-scm.com/downloads)

### 玩转Git命令

### 一、Git的相关配置

1.  配置全局账户，也就是你这台服务器所有的Git仓库,对此账户都有效

```shell
git config --global user.name '账户名称'
git config  --global user.email ‘账户Email’
```

2. 配置局部账户，也就是这个账户，只对当前仓库，有效

```shell
git config --local user.name '账户名称'
git config --local user.email '账户Email'
```

注意：一个仓库同时配置了global,则仓库有限使用本地设置。

3. 查看相关配置

   查看配置是否该生效

```shell
git config --global --list
==or
git config --local --list
```

### 二、本地基本操作

这部分也是我工作中使用比较多的命令

#### 1. 基本操作

1. 查看变更情况

``` shell
git status
```

2. 查看当前分支属于哪个分支

```shell
git branch -v
```

3. 切换到指定分支

```shell
git checkout 'branchname'
```

4. 把当前目录以及子目录下所有的变更都添加到暂存区

```shell
git add .
```

5. 把仓库内所有的变更都加入到暂存区

```shell
git add -A
```

6. 把指定的文件添加到暂存区

```shell
git add 文件1 文件2 ...文件n
```

7.  创建正式的commit,也就是把当前的数据从暂存区提交到版本库（记住文件变更需要先提交到暂存区，才能进行版本库的提交）

```shell
git commit -m "message" 
```

#### 2. 比较差异

1.  比较某文件工作区与暂存区的差异

```shell
git diff 某文件
```

2. 比较某文件暂存区与HEAD差异

```shell
git diff --cache 某文件
```

3. 比较工作区和暂存区的所有差异

```shell
git diff
```

4. 比较暂存区和HEAD的所有差异

```shell
git diff --cache
```

5. 用difftool工具比较任意两个commit之间的差异

```shell
git difftool commit1 commit2 
```

#### 3. 暂存区和工作区之间的回滚

1. 把工作区指定的文件恢复到和暂存区一样

```shell
git checkout 文件1 文件2 ... 文件n
```

2. 把暂存区指定文件恢复到和HEAD一样

```shell
git reset 文件1 文件2 ... 文件n
```

3. 把暂存区和工作区所有的文件恢复到和HEAD一样

```shell
git reset --HEAD
```

#### 4. 查看哪些文件没有被git管控

```shell
git ls-files --others
```

### 三、 加塞临时任务

1. 把未处理完的变更先保存到stash中

```shell
git stash
```

2. 临时任务处理完后继续之前的工作

```shell
git stash pop 
或者
git stash apply
```

3. 查看所有的stash

```shell
git stash list
```

4. 取回某次的stash的变更

```shell
git stash pop stash @{数字}
```

### 四、 修改个人分支历史

1. 修改最后一次commit

```shell
git add 
git commit --amend
```

2. 修改中间的commit(某一次的)

```shell
1. git rebase -i X前面的一个commit的id
2. 在工作区修改文件
3. git add 
4. git rebase --contiue
```

### 五、 查看变更日志

1.  当前分支所有信息

```shell
git log 
```

2. 当前分支最近的n条commit信息

```shell
git log -n 
```

3. 用图形显示所有分支的提交历史

```shell
git log --all --graph  
```

4. 查看某个文件的的提交历史

```shell
git log 某文件 
如果觉得展示信息太多，可以展示一行
git log  --oneline
```

5. 某个文件各行最后修改对应的commit以及作者

```shell
git blame 某文件
```

### 六、 分支与标签

#### 1. 创建分支

1. 基于当前分支创建新分支

```shell
git branch 新分支
```

2. 基于指定分支创建新分支

```shell
git branch 新分支 已有分支
```

3. 基于某一个commit创建分支

```shell
git branch 新分支  某个commit的id
```

4. 创建分支并切换分支

```shell
git checkout -b 新分支
```

#### 2. 列出分支

1. 列出本地分支

```shell
git branch -v
```

2. 列出本地和远端分支

```shell
git branch -av
```

3. 列出远端所有分支

```shell
git branch -rv
```

4. 列出名称符号某样式的远端分支

```shell
git branch -rv -l '某样式'
```

#### 3. 删除分支

1. 安全删除本地分支

```shell
git branch -d 分支名
```

2. 强行删除本地分支

```shell
git branch -D 分支名
```

3. 删除已经合并到master分支的所有本地分支 (就是筛选出所有的合并到master上的分支除去*或者master分支，然后逐一删除)

```shell
git branch --merged master | grep -v '^\*\|master' | xargs -n 1 git branch -d 
```

4. 删除远端origin已经不存在的所有本地分支

```shell
git remote prune origin
```

### 4. 创建标签

1. 在具体的commit的上创建标签

```shell
git tag 标签名 commit_id
```

### 七、 两个分支之前的合并集成

1. 把A分支合并到当前分支，且为该合并创建一个commit

```shell
git merge A分支
```

2. 把A分支合并到B分支，且为该合并创建一个commit

```shell
git merge A分支 B分支
```

3. 把当前分支基于B分支做 rebase 以便把B分支合入到当前分支

```shell
git rebase B分支
```

4. 把A分支基于B分支做rebase,以便把B分支合并到A分支

```shell
git rebase B分支 A分支
```

5. 用mergetool解决冲突

```shell
git mergetool
```

### 八、 和远端进行交互

1. 列出所有的remote

```shell
git remote -v
```

2. 增加remote

```shell
git remote add url地址
```

3. 删除remote

```shell
git remote remove remote名称
```

4. 改变remote的name

```shell
git remote rename 旧名称  新名称
```

5. 把远端所有分支和标签的变更都拉取到本地

```shell
git fetch remote
```

6. 把远端所有分支变更到本地，且merge到本地分支

```shell
git pull remote名称 分支名称
```

7. 把本地分支push到远端

```shell
git push -u remote名称 分支名称
```

8. 删除远端分支

```shell
git push remote --delete 远端分支名称
or
git push remote:远端分支名称
```

9. 向远端分支提交指定的标签

```shell
git push remote  标签名称
```

10. 向远端分支提交所有的标签

```shell
git push remote --tags
```

### 九、 常见的回滚操作系统

#### 1. 未执行commit之前

1. 如果文件修改了，但是还没有添加到暂存区，也就是还没有执行git add操作，则可以使用checkout来回滚

```shell
git checkout -- filename
```

2. 如果已经添加了暂存区，则可以用reset来撤销

```shell
git reset HEAD filename
```

#### 2. 执行了commit之后

1. 使用revert来撤销某次提交

```shell
git revert commitID
```

2. 使用reset直接回滚到某个版本，回滚之后，该commit_id之后的内容全没有了，且不可追回

```shell
git reset --hard commitID
```



### 写在最后：

会持续更新git相关命令，Git命令还是很多的，需要多使用多练习。当然单单会命令还不行。理解原理，对命令的掌握和理解有很大的帮助。也会慢慢更新相关的原理文章。期待自己，也期待读者从本质上读懂git
