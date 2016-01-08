#扩展有状态的服务 

## 摘要：
来自Twitter的分布式系统工程师，Caitie McCaffrey，在Strange Loop会议上讨论了有状态服务的优点，以及如何扩展它们，有状态的服务相比于无状态的服务，在业界大家知道的要少的多。其中优点包括数据定位、高可用、强并发模式。McCaffrey还给出了有状态的实际案例。

--------------------------------------------------

来自Twitter的分布式系统工程师，[Caitie McCaffrey](https://twitter.com/caitie)，在[Strange Loop会议](http://thestrangeloop.com/)上[总结](https://www.youtube.com/watch?v=H0i_bXKwujQ)了有状态服务的优点，以及如何扩展它们，有状态的服务相比于[无状态的服务](https://en.wikipedia.org/wiki/Service_statelessness_principle)，在业界大家知道的要少的多。其中优点包括数据定位（可通过函数传递范例来实现）、高可用、强并发模式。McCaffrey还给出了有状态的实际案例和少量的踩过的坑。

数据局部性是指每个请求都会被路由到（“运送到”）可以操作数据的机器上。当一个请求做到时第一次命中了数据存储，之后处理数据的请求离开了服务，在将来来自内存中的数据可以让类似的请求更快的找到同样的服务。结果就是低延时的好处，毋需再去访问数据存储。这就是“函数传递范例”，是有状态服务和无状态服务区别的关键所在。

有状态的服务通常会导致强一致性的模式。根据CAP理论（一致性、可用性、容忍网络分区），基本上说构建一个满足三种所有属性是几乎不可能的。这里有一个非常容易理解的有关于CAP概念的[问答](https://henryr.github.io/cap-faq/)。然而没有那个分布式系统能够避免“P”（问答中的＃10），现实世界是要么选择可用性胜过一致性，这称之为AP；要么选择一致性胜过可用性，这称之为CP。有状态的服务可以构建一种粘性的链接，也就是说客户端的请求总是会被路由到原来为之提供服务的服务器主机上。以此方式实现的服务，可以增加AP系统的一致性力度。这些强的模式包括有[线性随机访问内存](https://en.wikipedia.org/wiki/PRAM_consistency)和读你所写（Read your Write）。第一种实现是所有的请求所看到的写入都来自一个有序的请求，由它们自己所发出的。第二种实现是一旦请求要写，它就会读区更新后的值，且永远不会再理会旧的值。

Werner Vogels[在他的文章中总结了这些内容：](http://www.allthingsdistributed.com/2008/12/eventually_consistent.html)

>>无论是否是读你所写、会话以及单调的一致性，这些的实现通常都依赖于“无粘性”都客户端到服务器，为它们执行分布式的协议。如果这每次都是同一台服务器的话，相对能够容易保证读你所写和monotonic读取。这就对负载均衡和容错稍有难度，但是它是一个较简单的解决方案。使用粘性的会话，可以更加明确以及提供抛出的客户推理的水平。

McCaffrey谈到业界通常聚焦于无状态的服务是为了[实现可扩展性](http://blog.rackspace.com/coding-in-the-cloud-rule-3-use-a-stateless-design-whenever-possible/)而忽略了有状态的服务， Eric Evans在他的书[领域驱动开发](http://www.amazon.com/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215)中写道：

>>当在某域中的某个重要的进程或转换不是天生的负责一个实体或值的对象时，为模式增加一操作作为独立的接口来声明一个服务。定义接口是模型预言中的一个术语，还要确保操作的名称是无处不在的语言的一部分。将服务成为无状态的。

无状态的服务很容易的通过给后端添加服务器和前端的负载均衡实现横向的扩展。此类应用拥有叫做“数据运送范例”的方式，就是数据被请求时是来自后端的数据存储为请求提供，在未来的请求中，若相同的数据被请求时，是不会去关心这些请求是从哪个服务实例来的，因为服务实例是无状态的。

此模式会放之四海而皆准吗？McCaffrey谈到在“通信频繁”的应用中简直是一种浪费，因为这些应用要在服务端与客户端之间频繁的通信，而且在此类应用中有状态的服务显然是一种更好的选择。Kai Wähner[同意并列举了有状态服务的优点：](https://www.voxxed.com/blog/2015/01/good-microservices-architectures-death-enterprise-service-bus-part-one/)

* 当状态是共享的跨调用时，开发是容易的；
* 不需要额外的持久存储；
* 通常，为低延时优化。


粘性连接可以使用持久性的连接来实现，但是会带来负载在后端分布不均的问题，这就会导致客户端捆绑到服务器，而有些服务器不能得到充分利用，而有些服务器却负载过多。其中一个减轻此种[后端压力](http://mechanical-sympathy.blogspot.in/2012/05/apply-back-pressure-when-overloaded.html)的方法就是一旦达到某个阀值就拒绝再来的请求。非粘性的服务还可以通过路由的逻辑来实现，这可以使得任何的客户端通过获得正确的路由来找到任何的服务器。此实现会带来两个问题，路由到集群成员（谁在我的集群中？）和工作分布（谁来做？）。集群成员可以是静态的也可以是动态的。后者可以通过使用[gossip协议](https://en.wikipedia.org/wiki/Gossip_protocol)和[共识](https://en.wikipedia.org/wiki/Consensus_%28computer_science%29)系统来实现。工作分布则有更多的实现机制－随机替代、[一致性哈希](https://en.wikipedia.org/wiki/Consistent_hashing)、以及[分布式哈希表]。


McCaffrey谈到了三个有状态服务的真实案例：

* [Scuba](https://research.facebook.com/publications/456106467831449/scuba-diving-into-data-at-facebook/)，一个Facebook所使用的内存数据库，用于代码分析、bug报告、调试性能等。单个的请求会分散到多个后端服务器，然后将响应收集起来，最后决定如何将经过量化的响应完整的返回。
* 优步的[Ringpop](https://github.com/uber/ringpop-node)，一个应用层的切片库，也提供了请求转发。
* [Orleans](http://research.microsoft.com/en-us/projects/orleans/) ，来自[微软研究所](http://research.microsoft.com/en-us/default.aspx)的基于行为的分布式系统编程[模型](http://research.microsoft.com/pubs/210931/Orleans-MSR-TR-2014-41.pdf)。

有状态的模式其实在[MMO](https://en.wikipedia.org/wiki/Massively_multiplayer_online_game)的开发世界中是[见惯不怪的](https://gameserverarchitecture.com/2015/11/presentation-building-scalable-stateful-services/)，近期有很多其它领域的也在[大量的采用这些模式](https://twitter.com/boulderDanH/status/655839187170496512)，上面的例子就是明证。

在采访快结束的时候，McCaffrey讨论了通过从进程的生命周期解藕内存的生命周期，[Facebook是如何管理Scuba的快速重启的](https://research.facebook.com/publications/553456231437505/fast-database-restarts-at-facebook/)。在Scuba所在的机器重启后，会花费很长的时间去从磁盘读入数据。要解决此问题就是将这些基于内存的数据从将要宕机的机器中复制到一个共享的地方，当节点恢复后再复制回来。

McCaffrey在他的演讲中列出了一些构建有状态服务的陷阱，其中包括没有绑定的数据结构导致的内存问题、类似长期的垃圾回收暂停和重载状态时出现的内存管理问题等。状态重载会在恢复和部署新代码时发生，这两者都会像第一次从数据库中获取数据那样付出高昂的代价。

查看英文原文：[Scaling Stateful Services](http://www.infoq.com/news/2015/11/scaling-stateful-services)
