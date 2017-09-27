# 我的 git 学习历程

> 我在学习中使用的[参考教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)为廖雪峰的 git 教程

## 1.github 简介

>对 github 的了解和常用几个功能的理解

- 功能：版本控制，借助 github 托管代码
- 仓库(Repository): 存放项目的地址。仓库用来存放项目代码，多个项目对应多个仓库
- 收藏(Star): 收藏项目，方便下次查看
- 复制克隆项目(Fork): 把别人的项目复制克隆到自己的github 中，该项目独立存在。
- 发起请求(pull request): 基于fork ，克隆者把修改后的项目发给原有代码者，原有项目创建者接受更改。
- 关注(watch): 关注项目，接收项目更新提醒
- 事物卡片(issue): 发现bug,没有成型代码，需要进行讨论。

## 2.git 使用

### 2.1 git 工作区

> 对 git 工作区的理解
区域 | 方法
---|---
工作区 |  git status git add test.php 提交到暂存区
暂存区  | git status 查看状态
git 仓库 | git commit -m "提交描述" 提交到仓库

### 2.2 git 基础设置

1.git 安装之后，进行基本信息设置

```bash
# 设置用户名：
git config --global user.name "your name"
# 设置用户邮箱：
git config --global user.email ""
# 查看设置：
git config --list
```

![图片](http://om0ttwn6c.bkt.clouddn.com/LU%5B%5DT2AWIYUSI%29H%7DYCY2D~H.png)

2.初始化一个新的 git 仓库

```bash
# 创建文件夹
mkdir test
# 在文件内初始化 git
git init
```

3.向仓库中添加文件

```bash
# 步骤
touch a1.php
git status
git add a1.php
git status
git commit -m "message"
```

![图片](http://om0ttwn6c.bkt.clouddn.com/17RGI9EV6X%5BYBSOG%29~%60%5D6TP.png)

4.向仓库中修改文件

```bash
vi a1.php

git reset a1.php

git diff HEAD --a1.php

```

![图片](http://om0ttwn6c.bkt.clouddn.com/4KLK$7CI%5BK_@O8%7DWU80%28LQ2.png)
5.向仓库中删除文件

```bash
rm -rf a1.php
git rm test.php
git commit -m "message"
```

![图片](http://om0ttwn6c.bkt.clouddn.com/2V%28I5PW%7B2$9P6%5B7@JGIJ$OH.png)
6. 版本切换

```bash
#切换指定id的版本：
git reset --hard id

#回退到上个版本：
#HEAD 当前版本 HEAD^ 上一个版本 HEAD~number 指定数字版本
git reset --hard HEAD^

#把暂存区的修改撤回重新放回工作区
git reset HEAD file

```

![图片](http://om0ttwn6c.bkt.clouddn.com/WF_%28O%7B51W08RAW%5B5FQT8SM2.png)
7.查看各个版本库状态

```bash
#从进到远的提交日志：
git log
git log --pretty=oneline
#查看命令历史,可以获得最近命令的 id，便于切换
git reflog

```

8.丢弃工作区的修改

```bash
# 丢弃指定文件在工作区的修改
git checkout -- file
```

## 2.3 git 管理远程仓库

1. git 克隆操作

```bash
git clone url
```

2.本地仓库同步到远程仓库

```bash
git push origin master
```

![图片](http://om0ttwn6c.bkt.clouddn.com/TRD%29@K$9_NYPS2QKXQ%25%28CAM.png)
3.关联远程仓库

```bash
#要关联一个远程库，使用命令
git remote add origin git@server-name:path/repo-name.git；

#关联后，使用命令git push -u origin
master第一次推送master分支的所有内容；

#此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；
```

## 4. git 分支

- Git鼓励大量使用分支

- 查看分支：`git branch`

- 创建分支：`git branch <name>`

- 切换分支：`git checkout <name>`

- 创建+切换分支：`git checkout -b <name>`

 ![图片](http://om0ttwn6c.bkt.clouddn.com/MTYZ9%7B%5DB438G22MQNRO2~4P.png)

- 合并某分支到当前分支：`git merge <name>`不保留分支合并历史; `git merge --no-ff` 保留分支合并历史

- 删除分支：`git branch -d <name>`

- 当Git无法自动合并分支时，就必须首先解决冲突(冲突只能手动解决)。解决冲突后，再提交，合并完成。

![图片](http://om0ttwn6c.bkt.clouddn.com/AX~%6027Q4%5DG$G5%7D~GAFW5%29AE.png)

- 用`git log --graph`命令可以看到分支合并图。

![图片](http://om0ttwn6c.bkt.clouddn.com/%7B$$BLRRM96N98%60L2RD7%29%28BS.png)
- Git分支十分强大，在团队开发中应该充分应用。

- 合并分支时，加上`--no-ff`参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而`fast forward`合并就看不出来曾经做过合并。`git merage

- bug 分支：修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；

- 当手头工作没有完成时，先把工作现场`git stash`一下，然后去修复bug，修复后，1.再`git stash pop`，2.用`git stash apply`恢复，但是恢复后，stash内容并不删除，你需要用`git stash drop`来删除；回到工作现场。
- feature 分支:开发一个新feature，最好新建一个分支；如果要丢弃一个没有被合并过的分支，可以通过`git branch -D <name>`强行删除。