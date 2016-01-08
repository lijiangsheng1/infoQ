#Google容器引擎（GKE）发布 

## 摘要：
Google云计算近日在其博客中发表声明，旗下Google容器引擎（GKE）正式可用。Google声称GKE可以用于生产环境的使用，且承诺SLA运行时间为99.5%。GKE基于开源项目Kubernetes构建，运行在Google的云计算平台上，由Google的工程师来进行维护。

--------------------------------------------------

Google云计算近日在其博客中发表声明，[旗下Google容器引擎（GKE）正式可用](http://googlecloudplatform.blogspot.com.es/2015/08/Google-Container-Engine-is-Generally-Available.html)。Google声称GTK可以用于生产环境的使用，且承诺SLA运行时间为99.5%。


[GKE](https://cloud.google.com/container-engine/)是针对运行中的Docker容器进行集群管理和编排的系统。GKE基于开源项目[Kubernetes](https://github.com/kubernetes/kubernetes)构建，运行在Google的云计算平台上，由Google的工程师来进行维护。GKE基于在一个JSON配置文件声明中定义的要求来调度集群中的容器和对容器进行自动化的管理。

Google的产品经理Craig McLuckie声称Kubernetes项目给部署带来更大的灵活性，并指出若有需要的话将负载迁移出来到其它的云计算供应商中是非常容易的。

>>红帽、微软、IBM、Mirantis OpenStack、以及VMware（此列表仍在增长中）均在他们的平台中[整合Kubernetes](http://www.infoq.com/news/2014/07/google-kubernetes)，用户可随时将自己的负载迁出，或者是采用多家云供应商，都是较容易的。

>>GKE的底层基于Kubernetes的代码，而且我们针对多数供应商提供[K8s](http://vmturbo.com/about-virtualization/virtualization/forget-k9-its-time-for-k8-k8s-that-is-a-kubernetes-primer-part-i/)的支持，所以将托管在GKE上的应用程序移到其它地方是没有什么障碍的。这就是项目的总体目标。人们选择我们的基础设施完全是基于基础设施的优劣，而不是因为那些人为的锁定。

Google最初并没有使用的Docker容器，在Docker流行起来之前，Google就按照自己的方法使用了近10年的Linux容器。但是McLuckie此前就明确了，Docker已经是代表了事实上的容器引擎格式标准，而且Google会参与到标准化的工作中来。
就竞争对手和GKE的核心优势，InfoQ询问了McLuckie，以下是McLuckie的回答：

>>我不会对竞争对手的技术栈某些特定的功能进行评价，但是我要声明Kubernetes是一款开源项目，为多个云计算平台所构建。它是由构建[Brog](http://www.infoq.com/news/2015/04/google-borg)和[Omega](http://research.google.com/pubs/pub41684.html)同批工程师所开发。它的目的是将Google 10年的生产环境中使用容器的经验传授给任何想要使用的人们。不像其它项目那样已经被采用为现代PaaS技术的底层方案，以及被采用为某些Linux发行版标准的一部分。而这也是Google将之捐赠给Linux基金会的原因，以确保其真正为社区所有、由广泛的民众来主导、没有各种政治斗争的工程技术社区。


查看英文原文：[Google Container Engien Generally Available](http://www.infoq.com/news/2015/10/google-container-engine-ga)
