#Git及GitHub在线教程，内容回顾与作者采访 

## 摘要：
由Addison-Wesley Professional出版发行的Git和GitHub在线教程是基于Peter Bell在一些现场研讨会上的视频课程。目标学习者是那些没有任何Git经验或其它源代码管理工具经验的人们。这次，我们回顾下目前的课程内容，以及向教程的作者提几个问题。

--------------------------------------------------
由Addison-Wesley Professional出版发行的[Git和GitHub在线教程](http://www.informit.com/store/git-and-github-livelessons-workshop-9780133991772)是基于Peter Bell在一些现场研讨会上的视频课程。课程是属于慢节奏的，Peter非常的注重课程中所出现的每个新的概念都希望确保受众能够清晰的理解。目标学习者是那些没有任何Git经验或其它源代码管理工具经验的人们。这次，我们回顾下目前的课程内容，以及向教程的作者提几个问题。

课程有11个章节，总共大约需要花费5个小时看完。

第一课：Git 配置

在课程的第一部分，Peter介绍了Git的三个层次的配置，并解释了用户应该何时在给定的上下文中使用这个或是其它。另外还展示了一些可能有用的属性，Peter还解释了用户应该如何去定义命令的别名。

第二课：入门

此课程以最原始的命令开始：通过```git init```创建一个本地的仓库，然后为之添加一些个文件，并且非常仔细的解释了git的staging区域扮演着在推送staged的文件到git历史中之前的一个缓冲的角色。

Peter的介绍的特点就是在所有的课程，都会始终去详尽的解释Git的设计决定，而且会不言自明的摆在首位。这种情况，举个例子，Git的staging区域，这是Git非常关键的一个特性，可以让书写意义更加丰富的commit变得更加简单。另外一个展现Peter的能力的例子是他为学生们解释Git使用UUID背后的原因，这里有着Peter深刻的洞见，Git为何使用UUID替代类似SVN那样增长的数字，以及Git的如此行为为何又是必不可少的。

命令回顾：```init,add,commit,status,log```

第三课：GitHub

GitHub的引入是作为一种离线备份用户代码的机制，然后Peter展示了用户应如何在GitHub创建一个仓库，并且让其连接到用户的本地仓库。

命令回顾：```add origin,push,init```

第四课：重命名、删除、和.gitignore

第四课覆盖了在git中关于文件的基本操作，并展示了如何去在staging区域重命名一个文件或者是删除它。另外，介绍了.gitignore，此文件中所标记的git会在鉴定文件时会自动忽略。

命令回顾：```mv、rm、.gitignore、commit －a```

第五课：分支、合并和rebasing

命令回顾：```branch,checkout,merge,diff,commit,log,rebase```

第六课：Git内部工作原理

命令：```cat-file```

第七课：GitHub

命令：```clone,fork```

第八、九课：GitHub的特性和配置

第十课：发布流程

第十一课：还原

命令：```commit --amand,reset,rebase -i```

InfoQ有幸就Peter Bell的背景和他关于Git，GitHub和软件开发方面的个人意见作了采访。

InfoQ:你好，Peter，你将你自己定义为一名“[创业专家](http://www.linkedin.com/in/peterfbell)”，麻烦你和我们解释一下它的具体含义。

>>




InfoQ: 

>>



InfoQ:
 
>>




InfoQ:
 
>>


InfoQ:

>>




InfoQ: 

>>



InfoQ:
 
>>




InfoQ:
 
>>


InfoQ:
 
>>




InfoQ:非常感谢，彼得
 
>>非常感谢您抽出宝贵时间对我们的采访！

Git是一款分布式版本控制和源代码（SCM）管理系统，最初是由Linus Torvalds为Linux内核开发的，它现在已经[广泛的应用于](http://ianskerrett.wordpress.com/2014/06/23/eclipse-community-survey-2014-results/)各种软件开发的版本控制系统。

GitHub是一基于Web的托管服务，构建在Git之上，除提供Git的所有功能之外，它还增加了自身的特性，诸如Wiki、任务管理、以及bug跟踪。GitHub获得了空前的成功，在2013年12月，[他们宣布](https://github.com/blog/1724-10-million-repositories)已经有1千万个仓库托管在GitHub上。

Git及GitHub的在线播放列表如下YouTube列表:

[![video](https://img.youtube.com/vi/myD1zPfdjRs?list=PLQwEegbFUjHF0TGM_HigwCHOXMJGXvcwe/0.jpg)](https://youtu.be/myD1zPfdjRs?list=PLQwEegbFUjHF0TGM_HigwCHOXMJGXvcwe)


## 关于作者
![Image of author 1](http://cdn.infoq.com/statics_s1_20151020-0055-2u1/resource/articles/git-github-livelessons-review/en/resources/peter-bell.jpg)
Peter Bell是一位创业公司的技术专家，他是GitHub培训团队的签约成员，也是[Pragmatic Learning](http://www.praglearn.com/)的创始人，Pragmatic Learning是一家企业级培训机构，旨在帮助企业能够实践最佳的开源技术和流程。他同时也是哥伦比亚大学商学院的兼职教授，为商务人员讲授如何更好的雇佣和管理开发者。

他曾在一系列的会议上作演讲，如DLD会议、ooPSLA、QCon NY、QCon SF、RubyNation、SpringOne2GX、Code Generation、实用产品线、英国计算机协会软件实践推进会议、GraphConnect、DevNexus、cf.Objective()、CF United、Scotch on the Rocks、WebDU、WebManiacs、UberConf、the Rich Web Experience and the No Fluff Just Stuff Enterprise Java tour。他的文章曾经在IEEE软件、 Dr. Dobbs、IBM developerworks、信息周刊、方法&工具、 Mashed Code、开源杂志、NFJS和GroovyMag杂志等。

查看英文原文：[Git and GitHub LiveLesson Review and Q&A with Author](http://www.infoq.com/articles/git-github-livelessons-review)



