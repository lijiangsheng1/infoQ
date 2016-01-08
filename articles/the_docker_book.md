#"The Docker Book" 内容回顾与作者采访 

## 摘要：
“the Docker book”，作者James Turnbull，是一本为任何想学习Docker的人所撰写的一本手册，它会带着读者从第一次安装，通过简单的例子解释Docker的一些概念，一直到稍复杂的场景中让读者领略真实世界如何使用Docker的各种奇思妙想。值此机会，听听作者对于本书和Docker的布道。

--------------------------------------------------
“[the Docker book](http://www.dockerbook.com/)”，作者[James Turnbull](http://www.jamesturnbull.net/)，是一本为任何想学习[Docker](https://www.docker.com/)的人所撰写的一本手册，它会带着读者从第一次安装，通过简单的例子解释Docker的一些概念，一直到稍复杂的场景中让读者领略真实世界如何使用Docker的各种奇思妙想。

本书从描述Docker是什么以及其目的为何开始。它也描述了所有主要的Docker概念，以[镜像](https://docs.docker.com/userguide/dockerimages/)、[容器](https://docs.docker.com/userguide/usingdocker/)和注册处作为开端。镜像是基础的构建块，对于此James是描述为“容器的'源代码'”：高度的可移植性且易于更新。容器是“运行时”组件：一个基于镜像对包含自我的环境。镜像和容器在Docker中是可以分离的，分别为独立的部分。注册处是一种镜像管理、存储以及分享的机制。注册处所对于Docker镜像的角色就像是Github和社交对于源代码的角色。

在学习完基本的概念之后，读者就可开始学习Docker的安装了，书中讲述了如何在各种Linux发行版、Windows以及MacOSX下安装Docker。James列出了几种管理Docker的用户界面工具，但是它们表现不尽如人意，所以[命令行](https://docs.docker.com/reference/commandline/cli)才是王道。当你阅读完本书，你就能够掌握大多数Docker的各种命令、子命令的用法。

一旦读者将Docker成功的安装到自己的系统，James就会教授关于如何使用命令行和Docker来进行交互。通过一些基本的场景James向读者展示了如何创建容器([docker run](https://docs.docker.com/reference/commandline/cli/#run))，如何检查容器([docker inspect](https://docs.docker.com/reference/commandline/cli/#inspect))，或者是查看内部运行着什么([docker ps](https://docs.docker.com/reference/commandline/cli/#ps))。

接下来是学习如何创建镜像以及创建完成后将它们存储到仓库中。再重复一次，Docker仓库可以被类比于是Git仓库：Docker仓库存放Docker镜像；Git仓库存放源代码。创建镜像的方法有两种：使用[docker commit](https://docs.docker.com/reference/commandline/cli/#commit) 和Dockerfiles。因为镜像使用了[分层的格式](https://docs.docker.com/terms/layer/),构建在Union文件系统之上，Docker使用了提交的暗喻来创建新的镜像层。镜像层类似于源代码控制工具中的新版本。的确是，正如读者所真正理解的那样，Docker借鉴了源代码控制的理念。

使用[docker commit](https://docs.docker.com/reference/commandline/cli/#commit) 来创建镜像，就是创建了一个新的层，即改变了一个已经创建好的容器。所以James建议创建镜像的方式是使用[Dockerfiles](https://docs.docker.com/reference/builder/)。James在此花了一些篇幅来解释Dockerfiles，因为其对于Docker来说绝对是核心概念。在此读者可以不仅可以学习到Dockerfile的格式，还有运行时执行的工作流。例如，给出了每个创建镜像层的Dockerfile指令，Docker的时光机器功能可以随时回到镜像的任何历史的状态。同样，如果一个指令失败，你可以运行最后成功的那个指令的镜像，然后开始调试。这是Docker所提供的强大的功能之一，它彻底更改了服务器的构建方式。

一旦准备好了Dockerfile且完成了镜像的构建，就是该将镜像推送到Docker注册处了。James解释了如何使用Docker自身的[DockerHub](https://registry.hub.docker.com/)，以及如何集成GitHub或BitBucket来提供自动化的镜像构建。自动化构建，过去叫做可信的构建，是一种当你向GitHub或BitBucket提交了代码的时候，自动的开始构建镜像然后将镜像上传到DockerHub的工作流。James还提到了在刚开始写作本书的时候，提及了相关的注册处[Qury](https://quay.io/)和[Orchard](https://www.orchardup.com/)，以及如果需要的话，如何构建自己的注册处。但是这个世界变化太快，在本书出版后，CoreOS[收购](http://blog.devtable.com/2014/08/quayio-joins-forces-with-coreos.html)了Qury，Docker公司[收购](https://www.orchardup.com/blog/orchard-is-joining-docker)了Orchard。James对这些相关的事件做了一些补充。

James Turnbull花了很多篇幅来阐述Docker如何应用于实际案例中的想法。他的第一个案例是持续集成，使用Jenkins来运行多配置的构建任务。然后是一个使用Docker来构建和配置一个[Jekyll](http://jekyllrb.com/)站点。之后构建了一个基于Node.js和完全复制的Redis后端的web应用程序。每个案例的流程是很类似的，最有趣的地方莫过于Docker可以用于任何地方。主机服务器出了执行Docker之外不做任何其它事情。通过这些案例也阐述了卷和Docker网络的一些内容。

当将一台容器停止运行时，其上面所有的变更都会被丢弃，（译者注：相比于镜像）除非将这些变更作了提交，在原来镜像的基础上创建一层。这对于处理应用程序的数据并不适合。Docker解决此问题的方法是使用卷，通过Union文件系统来提供持久化的存储。James利用上述中的案例向大家展示了现实环境中Docker的使用卷是非常关键的。

接下来James介绍了容器网络的各种属性。在书中首先提到的是将容器的端口映射到主机的本地网络。稍后讨论了Docker的[内部网络特性](https://docs.docker.com/articles/networking/)。一旦安装了Docker，Docker就会在主机中创建一个名为docker0的虚拟网桥，它是连接主机和所有容器的虚拟设备。通过此方法可以让用户创建一个虚拟子网，相比于直接使用IP，James指出了此种方法的两个缺陷：在应用程序配置中需将网络硬编码；容器重启后其IP会发生变化。

本书讨论网络的部分，最后谈到的是容器的[链接](https://docs.docker.com/userguide/dockerlinks/#docker-container-linking)。一个链接是指在两个链接之间创建的一种父子关系，允许作为父的容器使用端口来和作为子的容器中没有被其它容器使用的端口通信。这就提供了一个高度安全的方式，这些端口都不会暴露给主机。不过，聪明的读者一定能够从这个描述中想到了，那就是链接只能在同一主机上的两台容器之间工作。

单个容器的能力是有限的，很明显，要提供更加复杂的服务，就需要工具来协调所有的容器。James为此写了一章内容，介绍了[Fig](http://www.fig.sh/index.html)和[Consul](http://www.consul.io/)，前者是为多容器服务的编排工具，后者是一个高度弹性服务的发现工具，并展示了在更加复杂的环境中如何使用它们。

在书中将Docker的应用程序接口专门的列出了一章，重点讲述了[远程应用程序接口](https://docs.docker.com/reference/api/docker_remote_api/)。远程API（应用程序接口，下同，译者注）是一个REST的接口，提供了和命令行类似的功能，是Docker管理和配置自动化的不二选择。但讲述API不是本书的核心内容，所以作者仅仅是走马观花的介绍了一下。虽然仅仅是粗略的介绍，但是对于本书已经足够用了。它们提供了一种和Docker通信的另外一个渠道，但是它们提供的是和本书其它章节一样的概念和功能。

本书所期望的读者要基本熟悉Linux，基本的命令行shell，软件包（yum和apt），服务管理，以及基本的网络知识。无论是开发者还是运维背景的任何人都可以阅读本书，即使是Windows背景，照着例子做也不会遇到很大的困难。本书有很完整的代码清单，在适当的时候，书中就会指出相关的包括[实例代码](https://github.com/jamtur01/dockerbook-code)的Github仓库。

本书所描述的案例表明了为何现在Docker是如此的盛行。鉴于本书是一本介绍Docker本身的书，案例仍然是现实环境的简化版。我们仍然要等待Docker在实际生产环境的使用的用户们提供更多的案例。

James Turnbull是一位多产的作家，其一些书是值得称赞的。去年，InfoQ曾对他另外一本书：“The LogStash Book”作了[内容回顾](http://www.infoq.com/articles/review-the-logstash-book)。“The Docker Book” 这本书对于Docker的入门者是非常有价值的。你可以从Docker的[官方文档](https://docs.docker.com/)中获得同样的信息，但是本书有着更好的组织方式，且易读。从另外一个角度讲，对于熟悉技术、又有图书的预算的人来说，这本书值得拥有。


InfoQ借此机会采访了James，让读者们听听他的转移技术阵营的想法。

InfoQ: 当第一次看到关于Docker时，看起来似乎服务的配置管理都不那么重要了，你只需要创建一个Dockerfile，其它就不用管了。也有一些人坦言承认Docker的各种好处，但也警告说这也太夸张了点。请问你对此怎么看？

```
James Turnbull: 使用Docker或者其它工具并不是一个非此即彼的问题。当你使用了一种新的工具你不可能就将旧的工具废弃掉，更何况没有哪种技术是包治百病的灵丹妙药。那些向你提出建议的人，不是在向你兜售一些东西，就是利用恐惧、迟疑、不确定来阻止你使用某些东西。优秀的开发者和系统管理员在工作中总能找到好的工具。如果说Docker和配置管理在他们中间非常的受欢迎。对于基于Docker的应用来说，使用配置管理来构建Docker镜像和维护Docker主机令人惊奇，Docker也不过是你服务管理和应用工具箱中另外一个强大、可爱的工具罢了。

```

InfoQ: 可以确定的一件事情就是Docker和容器技术改变了这个技术阵营，Docker的出现使什么作了主要的范式转变？在Docker没有出现之前是个什么样的情况？

```
James Turnbull: Docker能够让应用程序的构建以及可移植的部署更加的容易。也不是说离了Docker某些特定的应用就无法使用，但是可以确定的是Docker的出现让一些较难的IT任务变得更为简单和容易，比如：更加快速的交付代码、可移植的负载、以及构建应用程序。

```

InfoQ: “The Docker Book”是一本手册类的图书，主要针对的是从基本原理开始学习Docker的初学者，但是，在了解了Docker的机制之后，想要了解整个大局，其基础设施给如何适应这个新的“世界”。当你的读者看完了本书以后，还有什么资源可以进一步利用？

```
James Turnbull: 我期望大家不要将本书仅仅视为一本入门的教材。本书不仅着眼于基础，而且覆盖了在‘实际环境’中使用Docker，如测试、持续集成工作流、以及构建和部署应用和服务，还讲述了‘数据中心’工具的基础，如Fig之于编排，Consul之于服务发现。

本书之外，大家可以参考Docker的文档－[docs.docker.com](http://docs.docker.com/)，以及来自Docker社区的优质资源－Freenode上的IRC频道 #docker，[Docker用户邮件列表](https://groups.google.com/forum/#!forum/docker-user)。

```

InfoQ: Docker并非是唯一的容器技术，甚至一个概念也不是新的。你为什么认为Docker能够引领这一潮流？

```
James Turnbull: Docker让容器更加的容易使用。Docker借鉴了很多已有的技术，没有诸如Solaris Zone或LXC容器等软件卓越的工作就不可能有Docker。但是这些工具对于很多开发者和系统管理员不怎么接地气或者说入门门槛很高。Docker让一切变得简单起来，让一个入门者能够快速的掌握基本知识，就可以为他们的应用程序创建容器。

```

InfoQ: Docker的未来会是什么样子的？

```
James Turnbull: 我认为前途一片光明。Docker的工具和贡献者的生态系统的快速成长着实吃惊。它让整个行业的很多人都开始拥抱它，我们开始看到很多的功能以及集成，它允许人们构建和管理复杂的应用程序。我想你会看到现有的相当一部分的负载，不是全部！但占有相当份额的应用会迁移到Docker容器中运行。

```
## 关于作者
![Image of author 1](http://cdn.infoq.com/statics_s1_20150922-0305u2/resource/articles/docker-book/en/resources/James_Turnbull%20.jpg)James Turnbull 是多本关于开源软件技术书籍的作者，长时间活跃于开源社区，过去写过的书涉及Docker，Logstash，Puppet。他是kickstarter的VP，Docker公司的顾问，James常在一些开源会议上作演讲，包括Velocity, OSCON, [Linux.conf.au](http://linux.conf.au/), FOSDEM, DevOpsDays。他曾任职于澳大利亚Linux协会主席，维多利亚Linux协会前任委员，2008年[Linux.conf.au](http://linux.conf.au/)的财务官，长期服务于[Linux.conf.au](http://linux.conf.au/)和OSCON的程序员社团。

查看英文原文：[“The Docker Book” Review and author Q&A](http://www.infoq.com/articles/docker-book)
