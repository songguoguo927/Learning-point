# 表哥迷妹的怕忘录

*怕自己忘记，嘿嘿*:sweat_smile:


**npm**

:blush: 表哥笔记：

*注：在npm中，包（package）、模块（module）、依赖（dependency）说的都是一回事儿。* 

***

常用命令

* npm init 初始化项目，其实就是创建一个package.json文件。

* npm install 安装所有项目依赖。

* npm help xxx 查看xxx命令的帮助信息。

* npm search 搜索（快捷方式：find, s）

xxx 搜索xxx 如：npm search jquery。

* npm install 安装 （快捷方式：i）

xxx 搜索并安装xxx（局部）。安装多个依赖可用空格分割，如npm i jquery bootstrap。

xxx -g 搜索并安装xxx（全局）。安装多个同上。

xxx -D 安装并将依赖信息写在package.json中的devDependencies中。

快捷方式 i均可，如npm i jquery。

xxx@版本号 指定需要安装的版本号，若不指定将安装最新的稳定版本。

* npm uninstall 卸载（快捷方式：rm, r）

xxx 卸载xxx。多个依赖可用空格分割。

xxx -D 卸载xxx，并将依赖信息从package.json中的devDependencies中清除。

* npm list 列出已安装依赖（快捷方式：ls）
默认列出局部依赖。

* npm list -g 列出已安装的全局依赖。

* npm outdated 检查过期依赖

* npm update 更新依赖（快捷方式：up）

xxx 局部更新xxx。

xxx -g 全局更新xxx。

* npm root 查看依赖安装路径（也就是node_modules的路径）

默认查看局部安装路径。

-g 查看全局安装路径。

* npm view 查看模块的注册信息

xxx versions 列出xxx的所有版本， 如：npm view jquery versions。

xxx dependencies 列出xxx的所有依赖， 如：npm view gulp dependencies。


**webpack**

**git常用命令**

>在git clone的时候，所有本地分支默认与远程主机的同名分支，建立追踪关系，也就是说，本地的master分支自动"追踪"origin/master分支。
-[]也允许手动建立追踪关系---暂时没用，先放着，我不懒（不准讲我懒）。

[使用git的一些前置基本工作](https://xiajm.me/2018/08/17/%E5%A6%82%E4%BD%95%E5%B0%86%E6%9C%AC%E5%9C%B0%E6%96%87%E4%BB%B6%E4%B8%8A%E4%BC%A0%E8%87%B3github/)

`git pull`的使用

>讲个小故事：今天呢，橘子在github上的仓库中修改了一个文件readme.md，然后它在本地`git pull`了一下
>，就同步了。（前提是当前分支只有一个追踪分支）

**-[] `git pull`的自己的使用体验**
>阮大神的Git远程操作详解中说：

`git pull`命令的作用是，取回远程主机某个分支的更新，再与本地的指定分支合并

完整格式：
`git pull <远程主机名> <远程分支名>:<本地分支名>`

>远程分支名的是远程主机的分支，如果远程分支是与当前分支合并，则冒号后面的部分可以省略

**-[]`git fetch`和`git merge`**
>一旦远程主机的版本库有了更新（Git术语叫做commit），需要将这些更新取回本地，这时就要用到git fetch命令。

`git fetch <远程主机名>`，该命令将某个远程主机的更新全部取回本地

`git merge <name>`,合并某分支到当前分支

关于分支
Git鼓励大量使用分支：常用命令

* 查看分支：git branch

* 创建分支：git branch <name>

* 切换分支：git checkout <name>

* 创建+切换分支：git checkout -b <name>

* 合并某分支到当前分支：git merge <name>

* 删除分支：git branch -d <name>

**-[]`git push`就比较好理解了**
>git push命令用于将本地分支的更新，推送到远程主机。它的格式与git pull命令相仿。


**Bootstrap栅格系统**

### Grid栅格布局

Grid布局是第一个专门为解决布局问题而创建的CSS模块。用来解决复杂的二维布局。




最近虽然没有填小格子，是因为有些东西还在学习中，整理中，零零碎碎的感觉上传不太好。