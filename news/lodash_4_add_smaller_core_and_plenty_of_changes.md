#Lodash发布版本4.0，新增更小的核心和大量的改进 

## 摘要：


--------------------------------------------------
作为JavaScript实用程序库的[Lodash近期发布了](https://github.com/lodash/lodash/releases/tag/4.0.0)其4.0的版本，提供了新的核心以及其它大量的改进。

Lodash一直在持续的增加新的特性，所以文件的大小也一直在持续的增长。一些开放者需要全部的库，然而还有一些开发者并不需要全部，而是希望只要自己需要的那部分就好了。为了同时满足这相互冲突的二者的需求，新版本开发了微内核，大小只有12K（压缩后是4K）。此版本[包含](https://github.com/lodash/lodash/wiki/Build-Differences)了最为重要的65个特性，比如`foreach`和`map`。另外，完全的版本则新增了80个新的方法，诸如`flatMap`和`toLower`。

因为Lodash是遵循[语义化版本](http://semver.org/lang/zh-CN/)的。主版本号必须在有任何不兼容的修改被加入公共 API 时递增，次版本号必须在有向下兼容的新功能出现时递增。他们作了[大量的变化](https://github.com/lodash/lodash/wiki/Changelog)，所以升级到Lodash 4.0是顺势而行。

你将不会在Lodash中再看到已经失去开发者们宠爱的前端包管理器Bower的身影了。取而代之的是，npm，这将会是主流，按名称归类也取消了，所以开发独立的功能也变得容易了许多。

去年，Lodash和Underscore团队开始就[合并两个库](http://www.infoq.com/news/2015/05/underscore-lodash-merging)进行了讨论。在4.0的发行注记中，John-David Dalton谈到了此新版本是基于最终讨论的结果而定：
>>
Lodash v4的很多想法都是来自于那场讨论。Lodash若没有Underscore 的核心团队的参与和贡献是不可能开发出来的。其实此次成功的合并两个团队的实质在于有的成员本身就同时是两个程序库的贡献者。

关于项目的更多信息，请浏览其[Lodash的官方网站](https://lodash.com/)或者查看[托管在GitHub上的仓库](https://github.com/lodash/lodash/)。

查看英文原文：[Lodash 4.0 adds Smaller Core and Plenty of Changes](http://www.infoq.com/news/2016/01/lodash-4-released)
