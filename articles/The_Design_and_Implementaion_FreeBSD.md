#FreeBSD操作系统设计与实现，内容回顾与作者采访 

## 摘要：

FreeBSD操作系统设计与实现，历经人们的期盼而终于完成，它是FreeBSD内核的权威指南。第二版涵盖了从FreeBSD 5 到11之间的所有主要更新，根据发行注记，相比于第一版大范围的修改了三分之一的内容，而且还有三分之一的内容是新增加的。

--------------------------------------------------

Pearson/Addison-Wesley Professional 出版的[《FreeBSD操作系统设计与实现》](http://www.informit.com/store/design-and-implementation-of-the-freebsd-operating-9780321968975)历经人们的期盼而终于完成，它是FreeBSD内核的权威指南。第二版涵盖了从FreeBSD 5 到11之间的所有主要更新，根据发行注记，相比于第一版大范围的修改了三分之一的内容，而且还有三分之一的内容是新增加的。

第二版要明显的比第一版增加了很多内容，光页数都超过900多页，而且覆盖了FreeBSD的诸如虚拟化，沙箱，NFSv4，以及ZFS支持等等很多新的特性。

书的第一章介绍了FreeBSD的发展历史，第二章简要的概括了FreeBSD内核的所有组件，剩下的章节即是根据第二章的结构引导读者进入每个题目的细节。

此书采用的是按照FreeBSD的技术架构由内而外的来讲述的，从内核的服务开始，继而是进程和内容管理，然后是I/O和设备，文件系统，IPC（进程间通信），网络协议，最后是系统的启动与关闭。内容丰富，知识密集，以清晰明了的方式讲述技术话题，书中采用了大量的伪代码，示意图，表格来说明主要的观点，每一章均是以日常见到的主题开始介绍，然后深入扩展到细节。

尽管此书深入到FreeBSD的底层细节，但仍然提供了很多操作系统设计和概念的深刻洞见，这不仅对于FreeBSD的开发者有吸引力，任何对现代操作系统的思考和讨论有兴趣的人都是有益处的。

InfoQ采访了本书的作者之一[Marshall Kirk McKusick](https://en.wikipedia.org/wiki/Marshall_Kirk_McKusick)，

InfoQ:FreeBSD操作系统设计与实现描述了FreeBSD内部的运作机理，而且提供了大量翔实的资料，您此书的目标读者是哪些人？人们能够通过阅读此书能够学习到关于FreeBSD的什么内容？

```
Marshall: 我们的书的目标是哪些工作在FreeBSD下的专业人士，应用程序开发者可以学到如何有效的利用接口和系统交互；系统程序员可以学到如何扩展、加强系统；没有FreeBSD内核经验的系统管理员们可以学习到如何维护、调试和配置系统；技术和销售支持的个人参与者可以学习到系统具备哪些能力以及有哪些局限。

我们的书提供了FreeBSD如何实现它的基本服务的广泛的概述。这对哪些需要学习FreeBSD是如何提供服务的人们非常的有帮助。能够从本书中受益的人们包括操作系统实现者，系统程序员，UNIX应用程序开发者，系统管理与，以及对FreeBSD充满好奇的用户。本书针对的是拥有至少一年的使用类Unix系统的人们，懂一些C语言是非常有帮助的，但不是必须的。读者需要了解基本的算法（搜索、排序、哈希）和数据结构（链表、队列、数组）。

本书讲述了FreeBSD内核背后的机理。从介绍内核和服务开始，其中包含了用于并发控制的锁。接下来，就是进程的细节描述，包括诸如调度，信号等进程管理任务。概述了安全的框架和策略，包括Capsicum 沙箱和FreeBSD jail，Jail是一个允许在同一个系统中创建隔离的虚拟主机的程序，以内核和进程的内存管理的描述结束了进程的管理。然后转到内核的I/O，通过介绍I/O的框架，服用I/O的基础设施细节，以及本地和远程文件系统的支持。然后描述了如何配置、操作字符设备和批量数据传输设备，例如磁盘，以及如何管理虚拟设备从而支持Xen和bhyve虚拟化的。也涵盖了三个文件系统的设计和实现，它们分别是：快速文件系统(FFS),Zettabyte文件系统（ZFS），和网络文件系统（NFS）。接下来是进程间通信（IPC/套接字）接口，通过涵盖了网络的分层和实现进行了详细的描述，网络包括了路由，转发以及安全的TCP/IP协议。最后，讲述了内核的启动过程，本书更加的强调代码的组织，数据结构的表示，以及算法本身，而不是过一遍内核的代码。它没有包含机器的某个特定部分，例如设备驱动的实现。

```

InfoQ: 您认为FreeBSD在其它的类Unix操作系统中是一个什么样的地位？

```
Marshall: FreeBSD是三大主要发行版中最为流行的系统(另外两个分别是OpenBSD和NetBSD)。FreeBSD大范围的应用于世界上很多公司的核心基础设施，包括NetFlix，WhataApp，Yahoo！，Juniper网络，EMC/Isilon。另外苹果公司的Darwin使用的也是FreeBSD，也就是Mac OS X的基础操作系统。也由于它可以构建一个非常小的系统，所以能够在嵌入式系统中的应用逐渐增多。
开源界主要替代FreeBSD的还是Linux。FreeBSD的许可条款允许修改和改进系统而无需再发行，这样使得FreeBSD的许可更加的友好，无论是企业还是个人用户。Linux的许可条款要求所有的更改和改进内核进行源代码可以以最低的成本再发布。因此，若企业需要控制发行版的知识产权，那么使用FreeBSD来构建他们的产品就是不错的选择。

```

InfoQ: FreeBSD在过去相当长的一段时间里是最为流行的BSD系统，你认为导致项目如此成功的主要因素是什么？

```
Marshall: 从1993年成立伊始，FreeBSD项目的目标就是能够为一些企业和个人提供易用和易安装的发行版。

另外一个让FreeBSD成功的原因是FreeBSD不像其他开源项目那样设有永久的掌控者(例如Linux中Linus Torvolds和他的忠实的副手)，FreeBSD的系统治理是自我组织型的，允许受到鼓舞的人们上升到关键角色，且设置了开发者轮流掌控的机制。

在外围，有5000到6000名开发者，他们每个人都为系统的某个部分工作，例如，维护FreeBSD内核，持续开发FreeBSD 1000个核心工具，撰写FreeBSD文档，移植其它开源软件到FreeBSD中等等。开发者可以访问FreeBSD的仓库，但是没有更改的权限。他们若想提交，则必须和级别更高的提交者代为提交，或者是将问题以文件对形式报告给提交者，方可为系统添加代码。

比外围更近一层的是比开发者更高级别的提交者，目前有300到400名提交者，和开发者一样，他们大多数也是为系统的某个部分工作。和开发者不同的是，他们具有更改属于自己的系统部分，并提交到代码仓库。所有的非同寻常的变更都须有一个或多个其他的提交者审核后才能正式到进入到源码仓库。多数的提交者除了自己的本职工作以及审核之外，均会帮助多个开发者提交代码。

由开发者晋升为提交者的建议是由现有的提交者来做的，绝大多数的情况是提名开发者晋升的提交者，他们往往原来就是在一起共事过的，晋升的描述和评估，以过去的工作和当前的工作为准，然后发送给核心团队等待批准。

处于项目中心的是核心团队。核心团队由9人组成，每2年一次选举出来的。核心团队的候选人来自提交者，且由提交者选举。核心团队扮演着源代码最后的守护者的角色，他们会监控已经提交的内容，以及在两个或多个提交者就如何解决特定问题无法达成共识的情况下解决他们的冲突。核心团队还有一项职责是批准开发者晋升为提交者，(在罕见情况下)暂时或永久的将一些人从提交者组中清除。被清除的原因多数是不再活跃(超过一年的时间对系统没有任何的更改)。
```

InfoQ: 是什么让FreeBSD成为独特的，或者说，你个人意愿，为什么选择FreeBSD而不是其它BSD系统？

```
Marshall: 不像其它的BSD系统或者是通常的开源项目，FreeBSD对于每个大版本的维护最少周期为5年，在整个支持期间提供bug修复和安全更新。在这加大的支持期间，哪些基于某个版本开发自己产品的公司就无须为其自己所构建的产品失去支持而担心不已。

```
InfoQ: FreeBSD在过去几年中增加的最为引人注目的特性有哪些？

```
Marshall: FreeBSD最近新增的一个引人注目的特性是：Capsicum 接口，允许来历不明不明的代码在沙箱中运行，Capsicum允许具有安全影响的应用程序有非常紧密的边界，从而确保应用不能访问到，修改或盗取任何未授权到信息。

另外一个引人注目的特性是为FreeBSD添加了非常重要的ZFS文件系统，ZFS文件系统来自Open Solaris。不像Linux因为许可的冲突不允许引入ZFS，FreeBSD将ZFS完全整入内核，并且交付ZFS的全部功能集以及性能。

```

InfoQ: 在2012年对FreeBSD基金会的总监Dru Lavigne的[采访](http://www.unixmen.com/dru-lavigne-talks-freebsd-interview/)中,他说：“FreeBSD一直很幸运的是具有吸引安全研究经费和与学术界在安全领域的合作的能力。”这对FreeBSD过去几年产生了什么样的影响？

```
Marshall: 我们刚才提到的Capsicum项目，就是来自剑桥大学（UK）的研究项目。这完全是研究员们使用FreeBSD作为他们的开发平台的功劳，简直是天作之合，今天由FreeBSD所提供的产品接口，辅助库以及支持的程序均非常的适应他们的研究。真如Dru所指出的，FreeBSD基金会筹集资金来将研究原型转化为产品，这些转换工作离不开这些发掘，掏腰包和管理的人们。

```
InfoQ: 你认为FreeBSD能够为学习关于操作系统提供一个很好的参考吗？如果是的话，作为学习工具它能提供何种优势？

```
Marshall: 三位作者均倡导以FreeBSD作为教学工具。我们开发教学计划，课程笔记，以及实验室试验，用于教授高年级的本科生或者是第一、两年的研究生课程，这些我们开发的课程我们都发布在www.teachbsd.com网站上了，关于此项目我们才刚刚开始做，希望在一、两后有更多丰富的内容。

FreeBSD基金会最近开始了一个项目，将FreeBSD引入高中计算机科学课程。虽然这个项目才刚刚开始,愿景是希望能够提高高中学生对计算机技术的兴趣，尤其是FreeBSD。

```

InfoQ: 哪里是FreeBSD所引导的方向？其未来有何愿景？

```
Marshall: 项目的RoadMap由开发者们来驱动，这一般是在每年至少举办两次的FreeBSD开发者峰会上引入新的想法，开发者峰会分别是BSDCan(在加拿大的渥太华)和EruoBSD(在欧盟国家轮流)研讨会。当然，它也有来自FreeBSD用户社区的反馈，这一般是来自于每年3-4次的FreeBSD供应商峰会。

传统的FreeBSD发行主要是针对服务器和嵌入式系统的。[PC-BSD](http://www.pcbsd.org/)的目标用户则是桌面用户，它基于当前的FreeBSD发行版，从移植集中将一些软件包整合在一起(桌面、浏览器、邮件客户端等)，打造为一个简单易用且轻松安装的桌面(笔记本)系统。

```

此采访基于 ‘FreeBSD操作系统设计与实现’, 第二版一书，作者：Marshall Kirk McKusick, George V. Neville-Neil ， Robert N.M. Watson, Pearson/Addison-Wesley Professional出版, 2014年9月, ISBN 978–0–321–96897–5. 更多信息请访问[出版商网站](http://www.informit.com/store/design-and-implementation-of-the-freebsd-operating-9780321968975)

在2015年9月，出版商又发行了McKuscik新的视频教程：“[FreeBSD开源操作系统介绍在线课程](http://www.informit.com/store/introduction-to-the-freebsd-open-source-operating-system-9780134305868)”。

## 关于作者
![Image of author 1](http://cdn.infoq.com/statics_s2_20150916-0334/resource/articles/freebsd-design-implementation-review/en/resources/Marshall.jpg)Marshall Kirk McKusick 长期从事于Unix和BSD相关的写作、咨询和教授学生的工作，在加利福利亚伯克利分校期间完成了4.2BSD的快速文件系统。他还是伯克利计算系统研究小组的一名科学家，负责开发和发布4.3BSD和4.4BSD，他是FreeBSD基金会的董事会成员，FreeBSD的长期贡献者，USENIX协会的两届主席，他还是 ACM, IEEE, 和 AAAS的成员。

![Image of george](http://cdn.infoq.com/statics_s2_20150916-0334/resource/articles/freebsd-design-implementation-review/en/resources/61nXC98AYtL._UX250_.jpg)George V. Neville-Neil 安全、网络、操作系统方面的黑客，作家，教师，和咨询师。FreeBSD基金会董事成员，在FreeBSD核心团队工作了4年，2004年起，他为ACM的队列和通信写专栏“Kode Vicious”，他是ACM的从业者委员会副主席，也是Usenix协会，ACM，IEEE和美国科学促进会的成员。

![Image of Robert](http://cdn.infoq.com/statics_s2_20150916-0334/resource/articles/freebsd-design-implementation-review/en/resources/Robert_N_Watson.jpg)Robert N.M. Watson 大学讲师，剑桥大学计算机实验室的安全研究小组中讲授系统，安全以及架构。他负责监督计算机体系结构，编译器，程序分析，操作系统，网络和安全等先进领域的研究。FreeBSD基金会董事成员，在FreeBSD核心团队10年，作为贡献者有15年的历史，他是在Usenix协会和ACM的会员。

查看英文原文：[The Design and Implementaiton of FreeBSD Operating System, Review and Q&A With Author](http://www.infoq.com/articles/freebsd-design-implementation-review)
