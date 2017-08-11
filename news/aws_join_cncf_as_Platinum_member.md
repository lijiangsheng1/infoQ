# AWS 选择了 Kubernetes 之路 —— 加入CNCF

## 摘要：

Kubernetes 似乎已经打赢了这场容器编排的战争，成为了用户默认的选择，这句话或许在前两周说起，人们可能不以为然，但是上周微软加入CNCF，这不AWS 也做了最后的决定，以铂金会员身份加入CNCF，并且 还是CNCF 治理委员会成员。接下来就让我们看看详情。

--------------------------------------------------

> 译者注：CNCF 的全写是 Cloud Native Computing Foundation，即云原生计算基金会，本文不特别说明的情况，均使用 CNCF 缩写。

就在微软上周刚刚宣布加入CNCF基金会不久，还未完全尘埃落定之时，AWS 即日宣布[以铂金身份加入云原生计算基金会（CNCF）](https://www.cncf.io/announcement/2017/08/09/amazon-web-services-joins-cloud-native-computing-foundation-platinum-member/)。

AWS 加入[CNCF](https://www.cncf.io/)，也就是意味着要解决[AWS 和 Kubernetes 之间的高阶问题](https://www.geekwire.com/2017/microsoft-launches-new-container-service-joins-cloud-native-group-isolating-aws-kubernetes/)，Kubernetes 是一款开源项目，最初由Google开发，旨在利用Google过去十多年的容器使用经验，来解决容器编排问题，自发布以来非常迅猛，短短两年已经发展成为管理容器化软件开发[事实上的标准](https://www.geekwire.com/2017/independent-two-years-kubernetes-center-cloud-now-comes-hard-part/)。CNCF 基金会则是管理Kubernetes项目的，AWS 成为CNCF 的一分子之后，会花精力和时间来帮助 Kubernetes 项目的茁壮成长，而且也会贡献一些小型的项目，比如让Kubernetes更加的易用。

另外，来自AWS 的 Adrian Cockcroft ，他是AWS 的云架构战略的副总裁，会以治理委员的身份加入CNCF。与历史上的其他标准委员会相比，CNCF算是一个不太正式的标准机构。但是[它对于推进诸如Kubernetes项目的发展至关重要](https://www.geekwire.com/2017/standards-arent-standard-inside-growing-movement-shape-booming-cloud-industry/)，当然也包括一些通用的云计算。

其实，就在一个月以前，AWS 对于自己是否参与到通用的容器编排当中还犹豫不决，Kubernets是可以运行在AWS 之上的，但是，明眼人都很明白，能够在上面运行和积极的支持在之上运行是两码事，尤其是AWS 还会试图说服用户使用自己的容器编排产品。

亚马逊曾经一度推出自己的容器编排产品：[Amazon EC2 容器服务](https://aws.amazon.com/ecs/)，这样就有很多云计算用户和公司越来越担心AWS 之关心自己的产品和服务，是想牢牢的将用户锁定在AWS，让用户不断的投入时间和金钱。然而，Kubernetes 能够让云计算用户轻松的扩展自己的负载到多个云计算供应商中，当然也包括自己本地的服务器。AWS 可能意识到了这一点，认为应该去积极支持（尽管不是全部）。

其实，近期AWS的一些动作已经表明，AWS 有意和 Kubernetes 接近，比如最近的[一份报告说](https://www.geekwire.com/2017/report-amazon-web-services-warming-kubernetes-container-management/)，AWS 意图在Kubernetes之上开发一套容器编排产品，那么加入CNCF 这件事情，让这个想法变得更为真切，有了AWS 的支持，这让所有担心和Kubernets发生抢夺之战的人们松了一口气，也让所有的云供应商如释重负。

 Adrian Cockcroft 在加入感言中是如此说道：**“在AWS 云平台中已经运行多个CNCF 的项目，我们非常高兴加入基金会，以确保我们的用户能够继续在AWS 运行他们的负载。CNCF为诸如Kubernetes、contained、CNI、linkerd等开源项目提供了中立的机构，有了我们的加入，希望能够为社区添砖加瓦，共建云计算原生生态。”**

> 译者注： 开源已经成为公有云巨头的战场，保守的AWS是如此描述自己在开源的活动的：多年以来，Amazon 一直都有在为开源项目做出贡献，其中参与的项目有：Linux、Docker、Apache Hive、Apache Hadoop、Chromium、jQuery、OpenMPI 以及Apache MXNet等等，Amazon 在2013年加入Linux基金会，而且是核心基础设施计划（Core Infrastructure Initiative，CNI）的创始成员之一，对于Linux基金会下属的几个项目都有相应的贡献，它们分别是：Xen Project、Open Container Initiative（OCI）、 以及 TODO Group。


参考资料：

[Amazon Web Services chooses its Kubernetes path, joins Cloud Native Computing Foundation](https://www.geekwire.com/2017/amazon-web-services-chooses-kubernetes-path-joins-cloud-native-computing-foundation/)

[Amazon Web Services Joins Cloud Native Computing Foundation as Platinum Member](https://www.cncf.io/announcement/2017/08/09/amazon-web-services-joins-cloud-native-computing-foundation-platinum-member/)
