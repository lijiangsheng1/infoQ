# Google 教你如何“做”开源

> InfoQ 主编郭蕾先生在今年的硅谷行探访Google的时候，从Google员工的眼神中读懂“Google的技术才是最厉害的，云计算我们不该输给别人。”的信息，刚刚过去的Google Next 2017 大会，Google更是将开放的策略表露无遗。称这是“云计算的民主化、人工智能的民主化”。这不没过多少天，Google开源项目部，整合了Google开源项目及相关，并办了新家，建立全新的站点：[Google开源全新站点](http://opensource.google.com)

## 引言

在2016年，IDG旗下网站ARN发表了一篇文章：[展望2017年的顶级技术](http://www.arnnet.com.au/article/611897/top-tech-watch-partners-2017/)，将开源和人工智能、深度学习、虚拟现实、云计算安全一并列举为2017年的流行技术趋势。果不其然，2017年第一季度已经过去，回顾一下这个预测，某种程度上验证了这一预测：

* GitHub 发布开源指南，旨在帮助人们利用开源，参与开源，治理开源。
* AT&T、Alibaba加入Linux基金会。
* Amazon 开源旗下深度学习框架MXNet，并捐赠给Apache基金会。
* Google 捐赠给Apache下一代大数据框架Beam。
* 在刚刚结束的云原生技术研讨会上，Linux基金会主席的Keynote讲到，Kubernetes 将会是下一个云计算中的Linux。
* ......

不过，所有这些事件，均仿佛是为今天的事情作铺垫——Google为其开源建立了新家：opensource.google.com。

## 背景介绍：Google与开源

Google 对于开源的理解，在业界是独树一帜的。从2005年就成立了开源项目部（OSPO），并由业内对开源有深刻理解的Chris DiBona来主持工作。Google 或许并不是贡献代码最多的公司，在 Kubernetes 项目之前，Google的开源项目甚至是只有很小的贡献率、或者是强约束并非完全的开放（比如，Chrome和Android），但是它依旧在开源开发者圈具有强大的影响力（甚至有人说是最大的），这就是一旦彻底开放如Kubernetes这样的平台，就促使这个项目异常的成功。再说了，Google 除了项目之外，还创建过 Google Code，曾经一度是开源软件最大的代码托管的地方，以及大名鼎鼎的 Google代码夏令营（GSoC），虽然这些举措Google都没有大量的代码贡献，但是它促使世界各地的开发人员能够合作，从而编写更多的代码。

> 如果离开了开源软件，我们今天所看到的互联网将不复存在。    ———— Chris DiBona ，Google开源总监

除此之外，Google也通过诸如[软件自由保护](https://sfconservancy.org/)、[apache软件基金会](https://www.apache.org/foundation/)以及[其它的组织](https://opensource.google.com/community/affiliations)来对开源项目和社区进行赞助。

同时，Google也是开源的受益者，从1998年最初的服务上线，Google的产品和服务都是假设在Linux等开源软件的基础之上的。当时Google是一家广告公司，至少不是一家纯粹的靠软件来盈利的公司，拥有非常多的优秀的计算机科学家和工程师，一如Google自家博客中介绍中所说：“从支撑服务的Linux内核到内部的文化，开源是Google做任何事都绕不过的，深入人心。 ”

## 新站点的思路

负责人在博客上说道：新的站点成立，旨在将Google如何使用、发布和支持开源的所有事情放在一起。站点将以最大的深度和广度的展现Google对于开源的热爱！它不仅包含人们意料之中的：Google的程序、所支持的组织、以及所发布的长长的开源列表，而且还包括了意料之外的：Google是如何“做”开源的幕后。

由此看出，新的站点，成为了Google对待开源的统一入口和展示的地方，也就是Google的开源哲学和方法论的最大呈现。

### 帮助人们找到感兴趣的项目

> 开源意味着让人们更好的协同工作，开发更优秀的软件，让这个世界更加的美好！ ———— Sarah Novotny, 项目经理

Google对于开源项目的态度，向来是“越多越好”，原因是无法实现知道那些项目会引起人们的兴趣，所以Google的开源部门就是帮助公司尽可能多的发布代码。这样的经过了多年以后，回过头来再看，Google已经发布了成千上万个开源项目，且有形形色色的许可协议，这些项目既有大型的产品，如[TensorFlow](https://opensource.google.com/projects/tensorflow)、[Go](https://opensource.google.com/projects/go)、[Kubernetes](https://opensource.google.com/projects/kubernetes) ，也有一些较小的项目，如[钢琴装饰灯](https://opensource.google.com/projects/light-my-piano)、[Neuroglancer](https://opensource.google.com/projects/neuroglancer)、[Periph.io](https://opensource.google.com/projects/periph-io),其中有些是获得Google正式支持的、有些是试验性质的，而有些则只是为了好玩。所有的这些项目，都分散在超过100多个GitHub的组织和Google自托管的git服务上，以至于人们对于Google开源代码的规模和范围是模棱两可的，甚至被错误的低估。

为了给人们提供一个完整的Google开源项目图景，Google创立来[Google开源项目目录](https://opensource.google.com/projects/)，在未来Google的开源项目部，会逐渐的将这个目录完善并对没个项目进行更为细致的描述，比如会举例说明，Google内部是如何使用的。

我们以[Kubernetes](https://opensource.google.com/projects/kubernetes)的描述页为例，见识一下Google的用心之处，打开这个页面，在上面的条幅上展示了项目的名称和站点域名，在正文的左侧，分了三个章节，分别是：

* Kubernetes的功能概要描述，所解决的问题，Kubernetes最初的灵感来源，以及简短的发展历史
* Kubernetes 在Google内部是被如何使用的
* 代码仓库，以及最为典型的GitHub质量评估：星星数量和被fork的次数。

而正文的右侧，则是一些归类、标签，以及所使用的编程语言，便于分门别类的查找。

这对于开发者而言，无疑会大大的提高查找自己感兴趣的项目的效率；而对于互联网或企业来说，研究Google怎么使用，会少走很多很多的弯路。是的，Google为这个世界贡献了很多分散的开源项目，有了这个权威的索引，让我们重新认识Google的开源项目的宏大，目前在编的项目超过2000多个。

### Google是如何做开源的

开源从来就不仅仅是将代码开放这么简单，它还至少包括了社区和流程。参与到开源项目和社区，对于Google这样体量的公司是件非常具有挑战性的事情，在2014年，Google帮忙组件了[TODo Group](http://todogroup.org/)，这是一个众多商业公司组成论坛，讨论参与开源的最佳实践和协作。经过多年的累计，从讨论中收获很多灵感，借着发布新站点的机会，Google还一同发布了内部文档：[Google 是如何做开源的](https://opensource.google.com/docs/)。

关于此文档，绝对值得业界借鉴，比如：

* Google发布一款新的开源项目[遵循那些流程](https://opensource.google.com/docs/releasing/)
* 如何为其它开源项目[提交补丁](https://opensource.google.com/docs/patching/)
* Google是如何[管理引入第三方的开源项目以及如何使用](https://opensource.google.com/docs/thirdparty/)
* Google 为何仅仅使用[某些特定的许可协议的项目](https://opensource.google.com/docs/using/license/)
* 为什么Googl需要将所有接受到的补丁都是[遵循许可协议](https://opensource.google.com/docs/cla/policy/)

罗马从来就不是一天建成的，上述的这些规则也好，流程也罢，都是多年的经验积累，甚至有的是付出教训后学到的经验。这些未必适合所有人，（开源本身就是有很多的选择）所以这些文档并非是“how-to”指南，但是相信对于有心人是有很大的参考价值的。

## 结语

Google 似乎正在改变自己在业内的高冷形象，从 Kubernetes 的社区运营，再到参与RedHat Summit，乃至这次新站点的建立，都在应验着开放战略，试图扳回在云计算市场的失利。比如Spanner的服务、以及免费为开发者提供资源等具体的产品和服务，都是长远战略下走的一步棋。但我们始终认为Google的信条，以及他对开源独特的理解，所以宁愿相信他的情怀：Google 开源项目部不仅仅是让Google的软件变得更好——他们更加热衷于通过开源改变世界。

让我们祝愿Google新的开源站点，百尺竿头更进一步！让所有的开发者、运维人员受益。
