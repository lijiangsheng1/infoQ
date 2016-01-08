# Force12.io 开发了一款Apache Mesos框架－'Microscaling'

## 摘要：

Force12.io日前发布了一款运行在Apache Mesos集群管理器之上的‘ Microscaling’容器原型示例。他们声称，在不同负载的情况下给定模拟的需求，启动和停止’优先级1‘和’优先级2‘的容器要比原来的autoscaling方法更加的快速。InfoQ为此和来自Force12.io的Ross Fairbanks讨论了此框架的目标和方法论。

--------------------------------------------------

[Force12.io](http://force12.io/)日前发布了一款运行在[Apache Mesos](http://mesos.apache.org/)集群管理器之上的‘ [Microscaling](http://blog.force12.io/2015/09/10/force12-on-mesos.html)’容器原型示例。他们声称，在不同负载的情况下给定模拟的需求，启动和停止’优先级1‘和’优先级2‘的容器要比原来的autoscaling方法更加的快速。

能够有效的自动扩展计算机资源是一件非常有[挑战](http://www.infoq.com/articles/auto-scaling-feedback)的事情,尤其是各家企业都具有不同的使用需求和负载类型。举例来说，Netflix曾经讨论过如何在使用传统的[autoscaling](https://aws.amazon.com/autoscaling/)方法之外另辟蹊径，Netflix创建了一名为[‘Scryer'](http://techblog.netflix.com/2013/11/scryer-netflixs-predictive-auto-scaling.html)的项目，此项目利用机器学习技术来假设、预测当前和未来的需求，并预先调整计算平台底层的可用资源。Netflix还谈到过为了更加灵活的扩展性，他们还创建一个新的平台，是基于Mesos的，项目名称为['Titan'](http://www.infoq.com/presentations/netflix-mesos-titan)，而且还创建了一个定制的Mesos框架－['Fenzo'](http://techblog.netflix.com/2015/08/fenzo-oss-scheduler-for-apache-mesos.html)。

Force12.io过去一段时间一直都活跃于这个领域，最近公布了一个基于Mesos的‘autoscaling‘调度器的[]演示程序](http://force12.io/)，他们声称此调度器具备‘microscaling’的能力，而术语‘microscaling’相比于传统的‘autoscaling’所提供的，则粒度更细的和更加及时的扩展。Force2.io的调度器运行在[Apache Mesos](http://mesos.apache.org/)之上，基于Mesosphere的[Marathon](https://github.com/mesosphere/marathon)框架，能够基于模拟（随机）的需求启动和停止‘优先级1’（高优先级）和‘优先级2’（低优先级）的容器。此调度器的实现方法非常的类似于John Wilkes在[QCon 伦敦 2015](http://www.infoq.com/presentations/cluster-management-google)上所公开讨论的Google内部项目['Brog'](http://research.google.com/pubs/pub43438.html)集群管理器。

InfoQ近日采访了Force12.io的首席架构师:[Ross Fairbanks](https://www.linkedin.com/in/rossfairbanks),就其他们在Mesos调度器所作的工作和'Microscaling'的前景进行了讨论。

InfoQ：Ross，非常感谢您今天能够腾出时间接受InfoQ的采访，麻烦您简要的介绍下自己，以及您在Force12.io博客上记录的实验动力何在？

```
Fairbanks:我叫Ross Fairbanks,是Force12.io的首席架构师，Force12.io是一家致力于实时的容器伸缩的初创公司。我的部分背景是曾在零售电商行业呆过，有工作在大型流量站点的经验，这一点导致我对自动伸缩非常的感兴趣，但是在虚拟机(VMs)下实现这点很困难，增加容量的前置时间往往要好几分钟。这就需要诸如迅速扩展而慢慢的缩小这类解决办法。

所以容器的快速启动和关闭的属性是最为吸引我们的。基于容器可以在秒级甚至是亚秒级的时间内增加和缩减容量。所以我们在AWS的EC2容器服务和Apache Mesos上构建了演示环境以展示这一概念。现在我们正在努力开源我们的解决方案，届时大家也可以将之运行在自己的基础设施环境中。

```
InfoQ：我们看到你使用术语‘microscaling’而不是‘autoscaling’。这背后有何原因？

```
Fairbanks:我们试图要和传统的autoscaling区别开来，传统的autoscaling添加和缩减的能力都是以分钟计算的，基于microscaling，能够让用户更加有效的利用现有资源而且伸缩容器仅需要几秒甚至是亚秒。

Microscaling能够很好的适应微服务架构，微服务架构是能够做到不同的流量模式有不同的服务。一个来自零售的例子就是，当市场的邮件发出去之后，搜索服务就会忙起来，但与此相反，而fulfilment系统只有在订单出货后才会忙起来。

我们认为这两项技术是可以在一起工作的，尤其是在公有云环境中。Microscaling可用于快速响应高峰期的需求，通过autoscaling增加的额外的虚拟机的容量来实现。Netflix早就在AWS上使用他们的[Titan](http://www.infoq.com/presentations/netflix-mesos-titan)这么做了，而且他们还开源了他们的Mesos框架[Fenzo](http://techblog.netflix.com/2015/08/fenzo-oss-scheduler-for-apache-mesos.html)。Force12希望能够让更多的企业组织都达到此级别的服务器利用率。Force12亦是平台无关的，我们打算支持所有主流的容器调度器。

```
InfoQ：相比于其它替代方案，什么是您选择构建在Mesos和Marathon之上的原因？

```
Fairbanks:我们视Force12为一个容器调度器，能够和其它的调度器很好的协作，主要方向是Microscaling。Marathon是一个能够支持容错的高级调度器，而且拥有良好的REST应用程序接口，能够让我们很容易的整合它。为了能够让协作调度成为现实，我们认为需要调度的标准，而且这是我们与社区之间通力合作的事情。

```
InfoQ：在Force12.io的博客上提到您对Mesos集群作了特别的配置／调优，这背后的动机是什么？以及这些变更能否适用于实验之外？

```
Fairbanks:我们的Mesos集群是运行在EC2之上的CoreOS实现的。我们使用Fleet来启动Mesos，Marathon和ZooKeeper，我们还使用了Consul来用于服务发现。我们还发布了整个步骤的[代码](https://github.com/force12io/coreos-marathon)，它可以运行在本地的3台Vagrant虚拟机环境中。我们还和Packet.net就此展开合作，而且我们还打算迁移我们的Mesos演示环境到他们的硬件服务器中，从而测试Microscaling在高性能硬件中的极限。

对于调优，我们首先是将Marathon启动任务配置为并行启动，而不是它默认的顺序启动。我们还减少了默认的分配间隔，从1秒降低到100毫秒。其它方面最大的更改是，在我们的CoreOS集群中运行了本地的Docker注册处，我们曾发现不论是在Mesos下还是在ECS中，Docker注册处的选择和位置是一个非常关键的因素，关于此我们在博客[Mesos演示环境](http://blog.force12.io/2015/09/10/force12-on-mesos.html)中作了更加细致的描述。

```
InfoQ：现在许多云供应商均提供容器解决方案（ECS，GKE，Triton等等），你认为你的研究他们会感兴趣吗？

```
Fairbanks:我们认为会的，作为microscaling可以运行在任何的容器集群中，且是以“数据中心操作系统”（DCOS）的方法来实现的。我们认为企业会迁移到“DCOS”，他们将开始更加的关注衡量服务器的利用率，他们会增加这方面的投入，从而让microscaling实现成本的大幅度节省。

```
InfoQ：您对microscaling的未来是怎么看的？它多久可以能够实际的大规模的商用（我们知道亚马逊已经发布了AWS lambda，一个概念上非常类似的产品）？

```
Fairbanks:要让microscaling得到普遍的使用，我们认为首先容器能够在大量的企业中用于生产环境。我们相信这将在接下来的12到18个月就能够实现。其中一些企业会更快的选择容器在生产环境中的使用，通常是因为他们需要那些由微服务架构带来的好处，例如autonomous团队。我们希望和这些早期的采用者展开合作，能够尽快的让microscaling准备好在生产环境中使用。

```
InfoQ：非常感谢你今天抽空接受我们的采访，还有其他和我们InfoQ读者分享的吗？

```
Fairbanks: 我们很快就会发布我们的第一个开源解决方案版本，如果你在Twitter关注我们（我们的Twiteter账号是[@force12io](http://twitter.com/force12io)），你会及时的收到发布的消息。我们真心希望能够获得来自社区的反馈。

```
关于Force12.io团队正在进行的工作的更多细节，请访问其[官方blog](http://blog.force12.io/2015/09/10/force12-on-mesos.html)。Apache Mesos的网站为开发者提供了如何创建[自己的Mesos框架](http://mesos.apache.org/documentation/latest/app-framework-development-guide/)的文档。在Youtube频道[MesosConf 2015大会](https://www.youtube.com/playlist?list=PLVjgeV_avap2arug3vIz8c6l72rvh9poV)上可以找到Mesos相关主题的各种讨论(从入门介绍到高级框架构建)。[MesosCon EU](http://events.linuxfoundation.org/events/mesoscon-europe/program/schedule)大会也将于10月8号－9号在都伯林举行。


查看英文原文：[Force12.io create a 'Microscaling' Framework for Apache Mesos](http://www.infoq.com/news/2015/09/force12io-microscaling-mesos)
