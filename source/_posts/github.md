---
title: github参与开源应该做什么
---
# 第一次参与开源项目应该做些什么
借鉴Moment老哥文档

https://juejin.cn/post/7354233858063925267

#### 第一步fork
fork到自己的仓库下 且选择fork所有分支 这样就可以有修改项目的权限
通过Pull Request方式 commits合到上游项目

#### 第二步克隆项目
git clone ...

#### 第三步更新本地分支代码
~~~
git remote add upstream <原始仓库的URL>
git fetch upstream
git checkout main
git rebase upstream/main
~~~
##### 根据ai理解 上述git指令

git remote add upstream <原始仓库的URL>
这条命令是将原始仓库添加为远程仓库，通常在你 fork 了一个 GitHub 仓库后，会创建一个 origin 指向你自己的远程仓库，但原始仓库（即你 fork 的那个仓库）并没有设置

-----
命令解释：

git remote add：

用于添加一个新的远程仓库。
upstream：这是你为原始仓库起的别名。通常我们使用 upstream 来表示原始仓库，而 origin 则表示你 fork 后的仓库。
<原始仓库的URL>：你需要替换成原始仓库的 URL，通常是类似 ~~https://github.com/owner/repository.git~~ 这样的形式。
举个例子： 假设你从 GitHub 上 fork 了一个叫做 awesome-project 的仓库，原始仓库的 URL 是 ~~https://github.com/original-owner/awesome-project.git，~~ 你可以运行以下命令：
git remote add upstream ~~https://github.com/original-owner/awesome-project.git~~
----

git fetch upstream

、这条命令是从原始仓库拉取最新的变化，但它并不会改变你当前的工作分支。它会将原始仓库的更新下载到你本地，但不自动合并到你的分支中。
举个例子： 继续使用上面的例子，如果原始仓库 awesome-project 有了新的提交，你可以通过以下命令来获取这些更新：
git fetch upstream
这条命令会从 upstream（原始仓库）拉取最新的提交，但是你的当前分支的代码还不会发生变化。
---

git rebase upstream/main

这条命令是将原始仓库（upstream）的 main 分支的最新提交应用到你本地的 main 分支上。
通过 rebase，你可以把你本地的提交历史 "重新基于" 原始仓库的更新，保持你的提交历史更加整洁。

 **总结：** 这样，本地 main 分支就会包含原始仓库的最新更改，并且历史记录会保持整洁。如果有冲突，Git 会提示你解决冲突并继续 rebase。

**注意：**
----在项目中不应该轻易的在main分支上做更改而是创建的分支 最好保证每个功能一个分支

创建分支在分支中编写代码
~~~
git checkout -b feat-xxx

~~~

#### feat前缀
feat 前缀用于标记新增功能（feature）的提交。它表示该提交引入了一个新的特性或扩展了项目的功能。使用 feat 可以快速识别出项目功能的增长点。

~~~
feat: add user login functionality

~~~

#### fix前缀
fix 前缀用于标记修复 bug 的提交。它说明该提交解决了项目中的一个或多个已知问题。

~~~
fix: correct minor typos in code
~~~
等等指令在此省略 详细的等到具体运用中再做增加

#### 写入你想更改的地方
提交你的更改 

#### 开一个PR
在完成 push 操作后，我们打开 GitHub，可以看到一个黄色的提示框，告诉我们可以开一个 Pull Request 了

参考：

https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fxun082%2Fcreate-neat%2Fpull%2F83
一定要参与一次实践，才懂得如何去做。只有错过了，才能保证下一次的完美运行。

---


---最后希望自己早入加入开源大家庭中，加油！ 
-                          2024 11.5日
