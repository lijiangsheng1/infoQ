#衡量开源社区的5大指标 

## 摘要：
本文系[Opensouce.com](https://opensource.com/)所发布的《开源2015年鉴》的其中一篇，介绍了评判一个开源社区的至为重要的5大指标，它们分别是：活跃度、规模、表现、人员流动、以及多样性。且看作者娓娓道来。

--------------------------------------------------

![peitu](https://opensource.com/sites/default/files/styles/image-full-size/public/images/business/yearbook2015-osdc-lead-1.png?itok=rN-X35tE)

若你决定使用一些指标来跟踪一下你的自由／开源软件（FOSS）项目的话，那么最大的问题是：哪些指标是我需要跟踪的？

要回答这个问题，你必须对自己需要什么样的信息有所了解。举个例子来说，你想知道关于项目社区的可持续性。社区是如何快速的响应问题的？社区是如何吸引、留住或流失贡献者的？一旦你明白自己需要什么样的信息，你就可以找出社区的哪些活动能够提供这样的结论。好消息是，FOSS的项目遵循开放发展的模式，这就是说在它们的软件仓库中留下了公共的数据，这样就可以用来分析有用的数据。

在本文中，作者将介绍能够提供多面视野的衡量开源社区的指标。

##活跃度

对于所有的开源社区来说，整体的社区活跃度以及如何随时间而演变都是非常有用的衡量指标。活跃度为我们提供了社区做了多少的第一印象，当然具体来说活跃度也可细分下去。举例来说，提交的次数可以表明开发者们的努力指数；处于打开状态的传票数则可洞晓项目目前有多少Bug没有修复或者是新提出了多少特性需求；邮件列表中消息的数量或论坛的帖子数量让我们对所公开讨论的内容心里有个数。

![openstack example](https://opensource.com/sites/default/files/images/business-uploads/activity-metrics.png)

上图所指是项目OpenStack的提交数以及代码审核之后的合并数，时间演进（周度数据），数据来源[OpenStack 活跃度面板](http://activity.openstack.org/)。

##规模

社区的规模常常指的是参与到社区的人员的数量，但是，也要取决于参与的类型，规模的大小也可能有所不同。通常我们最为关注的是活跃贡献者，这当然是正确的关注点了。活跃的用户会在项目的代码仓库中留下轨迹的，这也就意味着我们可以统计到哪些撰写代码较多的贡献者，比如 git 仓库的话查看作者一项即可；又如可通过查看谁解决的问题最多来统计参与的活跃度。

活动最为基本的概念（某人做某事）可以有多种延伸。常见的跟踪活动的方法是查看有多少人所做的占了多大的份额。通常为项目的代码贡献，比如，在项目社区中占有很少的份额。了解此占有份额有助于知道核心小组的意见（比如某些人是社区的领导者）。

![xen example](https://opensource.com/sites/default/files/images/business-uploads/size-metrics.png)

上图是Xen项目的邮件列表的作者数量和发信人的数量图示，时间演进（月度数据），数据来源[Xen项目开发面板](http://projects.bitergia.com/xen-project-dashboard/)。
##表现
以上，我们聚焦于衡量活跃度和贡献者的数量。但是我们仍然可以分析社区成员是如何处理问题的，或者是他们的具体表现等。举例来说，我们可以评估下他们处理某个流程需要多长时间，解决或关闭一个传票的时间可以说明此项目对于新的请求活动是如何响应的，诸如修复一个报出的bug或者是实现了一个新提出的特性。代码审核时间的长短－从代码变动的时刻到代码被接受为止这段时间－则说明了多长时间的建议变更到社区所制定的质量标准。

其它衡量的如：如何处理项目的应对工作，诸如新的和已经关闭的传票比率，没有完成的代码审核的积压。这些因素告诉我们，所投入的资源是否足够能处理完问题。


![openstack q3](https://opensource.com/sites/default/files/images/business-uploads/efficiency-metrics.png)

关闭的传票和打开的传票的比例，建议接受变更和拒绝变更的比例。数据来之于项目OpenStack，[OpenStack开发报告，2015年第三季度](http://activity.openstack.org/dash/reports/2015-q3/pdf/2015-q3_OpenStack_report.pdf)(PDF)。

##人员流动

贡献者的来来去去就可说明社区的变动。取决于随着时间的推移有多少人参与进来以及多少人离开，即所谓的社区的不同年龄（时间从成员参与到社区就算）。[社区年龄图表](http://radar.oreilly.com/2014/10/measure-your-open-source-communitys-age-to-keep-it-healthy.html)很形象的讲清楚了随时间的成员变化。图表由一组横向的进度条所组成，一对进度条表示的是“一代”加入到社区人们，对于每一代来说，attracted 进度条表示的是在此时间段内有多少新加入到社区中的人数，retained 进度条表示的是有多少仍然活跃于社区的人数。

每一代的两条进度条的关系就是留存率：就是仍然在项目中的成员的分数。整体的 attracted 进度条展示了项目在过去有多大的魅力，而整体的 retention 进度条展示的是社区当前的年龄结构。

![eclipse example](https://opensource.com/sites/default/files/images/business-uploads/demography-metrics.png)

来自 Eclipse 社区的社区年龄图表，数据来源[eclipse开发者面板](http://dashboard.eclipse.org/demographics.html)，此表每隔半年生成。
##多样性

多样性对于一个健壮的社区来说是非常重要的一个因素。一般来讲，一个社区具有更多的多样性－－参与的人或公司的一个术语－－那么说明这个社区就更加的健壮。举例来说，当一家公司要从一个FOSS项目中撤离时，那么就会考虑到它的离去所带来的潜在问题就是其员工所贡献的将会缩水，从85%变为5%。

[小马因子](https://ke4qqq.wordpress.com/2015/02/08/pony-factor-math/)，这是由[Daniel Gruno](https://twitter.com/humbedooh)所定义的一个术语，意思是贡献了50%的开发者的最少数，以此类推，大象因子表示的就是贡献了50%的公司的最少数。此两个数字均提供了社区所依赖的开发者和公司的数量。

![open cloud](https://opensource.com/sites/default/files/images/business-uploads/diversity-metrics.png)

云计算领域的一些FOSS项目的小马和大象因子。数据来源：[2015开放云的定量状态](https://speakerdeck.com/jgbarah/the-quantitative-state-of-the-open-cloud-2015-edition)（演示文稿）。

对于量化社区还有很多的有用的指标，当决定收集哪些指标时，要明确社区的目标，然后在去寻找哪些指标可以帮助你实现它。

## 关于作者
![Image of author 1](https://opensource.com/sites/default/files/styles/profile_pictures/public/jesus.jpg?itok=CyG9o9xt)Jesus M. Gonzalez-Barahona 是[Bitergia](http://bitergia.com/)的联合创始人，Bitergia是一家针对软件开发的分析公司，特别是对自由／开源软件项目。他同时还在 Rey Juan Carlos 大学（西班牙）进行[教学和研究](http://gsyc.es/~jgb)，也隶属于[GSyC/LibreSoft](http://libresoft.es/)研究小组。他的兴趣包括有学习社区的软件开发，重点在于定量和实证的研究。他还非常乐意和大家分享他[尝遍世界各地的咖啡的照片](http://www.flickr.com/photos/jgbarah/sets/72157633382014597/)。大家可以关注他的Twitter：[@jbbarah](http://twitter.com/jgbarah)。

本文由作者[Jesus M. Gonzalez-Barahona](https://opensource.com/users/jgbarah) 发表在Opensource.com上：[Top 5 open source community metrics to track](https://opensource.com/business/15/12/top-5-open-source-community-metrics-track)。经授权，在InfoQ中文站翻译共享。本文在[Creative Commons BY-SA 4.0](http://creativecommons.org/licenses/by-sa/4.0/)许可证下发布。

