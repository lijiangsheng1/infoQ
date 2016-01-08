#Git 2.6 发布，带来许多新的特性和改进 

## 摘要：

git 近期发布了其最新的2.6版本，增加了许多新的特性，对许多内部实现和性能方面进行了改进，以及修复了大量的Bug。

--------------------------------------------------
git 近期[发布](https://github.com/blog/2066-git-2-6-including-flexible-fsck-and-improved-status)了其最新的2.6版本，增加了许多新的特性，对许多内部结构和性能方面进行了改进，以及修复了大量的Bug。

新的工作流和用户接口特性

Git2.6引入了新的特性，即命令`git fsck`，此命令可在项目的历史记录中解决一些小的错误。`git fsck`用于验证仓库的完整性。经常遇到的情况时，当`git fsck`会对过去的提交过于吹毛求疵时，标记为不当的形式，以及不值当的历史记录修改等，例如，当很多用户已经克隆了仓库时。在此情况下，Git 2.6 允许开发者通过指定`git fsck`来调整严重性，例如，命令`git config fsck.badEmail ignore`会忽略不合法的电子邮箱地址。

`git fsck`也可以用于自动地检查对象的完整性，这些对象是指已经push到仓库的对象，从而防止旧的对象进入到项目的历史。在此情况下，这对告诉`git fsck`简单的忽略处于不好状态的提交蛮有用处，同时还能保持对新push的对象作全面的检查。这可以通过`git config: git config fsck.skiplist "$PWD/.git/skiplist"`所提供的可忽略的提交列表来完成 。

当执行一次rebase期间，命令`git status`能够显示更加详细的内容，它会提供关于在rebase日志中最后步骤和接下来的步骤的细节。这在大批量的提交后，再rebase时可以很好的跟踪一些记录。

以下是其它一些较有用的新特性：

 * `git log --date` 允许开发者使用自定义的日期格式：`git config log.date "format:%c"`；
 * `git log --cc` 现在实现了`-p`的功能，所以它实际上显示合并提交的不同；
 * `git fast-import` 支持一个新的`get-mark`属性，使得SHA－1所对应的文件描述符被标记为可打印；
 * `git log`  支持一个新的配置项：`--follow`，继续列出经过重命名的文件的历史；
 * `git pull --rebase` 现在会考虑用户的`rebase.autostash`配置，此配置项默认会启用`--autostash`属性，从而让用户可以rebase一个脏的worktree。
 
性能和内部实现改进。

在前端交互方面，用C重写了一些命令，例如`git pull`和`git am`。另外，对`commit`和`status`在multi-tree合并后进行了加速。还有，对Git的一些内部实现作了一些变更，为的是准备好让不同的`ref`后端能够插入到Git。

根据Git邮件列表的[通告](http://lkml.iu.edu/hypermail/linux/kernel/1509.3/02871.html) ，Git2.6包含了从Git2.5以来479次未合并的提交。关于新特性的完整列表，以及所修复的Bug，请阅读其[发行注记](https://raw.githubusercontent.com/git/git/master/Documentation/RelNotes/2.6.0.txt)。

查看英文原文：[Git 2.6 Brings Many New Features and Improvements](http://www.infoq.com/news/2015/10/git-26-released)
