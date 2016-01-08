#Docker 1.9 对网络、存储和集群进行了改进 

## 摘要：
Docker公司在这个月巴塞罗那举办的DockerCon EU上发布了Docker引擎1.9版本。此次新版本的发布，正如Docker公司在月初所声明的那样，包含了网络和卷管理的变化，Docker Swarm可用于生产环境了，以及对于Docker Compose、Docker Toolbox、和Docker Registry等组件的诸多改进。

--------------------------------------------------

Docker公司在这个月巴塞罗那举办的[DockerCon EU](http://europe-2015.dockercon.com/)上发布了[Docker引擎1.9](https://blog.docker.com/2015/11/docker-1-9-production-ready-swarm-multi-host-networking/)版本。此次新版本的发布，正如Docker公司在月初所声明的那样，包含了网络和卷管理的变化，[Docker Swarm](https://www.docker.com/docker-swarm)可用于生产环境了，以及对于[Docker Compose](https://www.docker.com/docker-compose)、[Docker Toolbox](https://www.docker.com/products/overview#/docker_toolbox)、和[Docker Registry](https://www.docker.com/docker-registry)等组件的诸多改进。

在6月份的时候以试验版发布了针对[网络的改进](https://blog.docker.com/2015/06/networking-receives-an-upgrade/)的版本，Docker现在则认为他们的[多主机网络](http://blog.docker.com/2015/11/docker-multi-host-networking-ga/)已经成熟可用于生产环境了，并因此而将此特性纳入了新发布的[Docker引擎1.9](https://github.com/docker/docker/tree/release/v1.9)版本。来自Docker公司的Ben Firshman在其公司的博客中如此说道：

>>网络的改进包括能够让用户跨多主机的创建虚拟网络。容器可以挂接这些处于任何位置的网络，为用户提供完全可控的网络拓扑结构，且做到了任意的容器之间的互联互通。当然不仅仅是这些了，我们还提供了将网络以插件的方式换出的强大功能，允许用户集成想要集成的任意网络，还毋需改动用户的应用程序。

在此版本中Docker还重新设计了卷的系统，允许用户跨整个Docker引擎的集群来管理持久存储。另外，Docker还声明了[Docker Swarm](http://blog.docker.com/2015/11/swarm-1-0/)已经准备好为生产环境服务了，所以在此环境下新的卷系统是可用的。在DockerCon EU会议上，Docker做了如何部署上万个容器到集群中的不同的演示，而且保持[Docker Swarm环境的稳定和正常的功能以及速度](http://blog.docker.com/2015/11/scale-testing-docker-swarm-30000-containers/)。来自Docker公司的软件工程师，Andrea Luzzardi说道：```“在我们的测试中，我们运行在1000个节点的EC2中，启动了30000台容器，且能够保持调度容器在0.5秒之内”```。

在会议的第一天，来自Docker的高级工程经理Arnaud Porterie和软件工程师Jessie Frazelle一起作了主题为[Docker引擎的最新进展](http://www.slideshare.net/icecrime/the-latest-on-docker-engine)的分享，Porterie和Frazelle对Docker公司的过去、现在、以及未来作了一番描述，Porterie重点介绍了Docker背后的开源社区的力量支撑，以及接受来自pull request的高度比率。

>>所有Docker引擎的代码有61%的贡献并非是Docker公司的雇员。有2162个pull request，我们合并了1815（约80％）。如果你从来没有为开源贡献过什么，Docker是你开始的最佳实践之地。

Frazelle则展示了新的Dockerfile描述，例如‘ARG’用于添加构建时间的参数，‘STOPSIGNAL‘用于当用户要停止容器时可自己定制要发送的信号。Docker现在支持通过卷来做扩展，关于此方面的例子有来自ClusterHQ的[Flocker插件](https://docs.clusterhq.com/en/1.5.0/install/docker-plugin.html)。

总结这次分享，Porterie给出了一些关于Docker引擎未来发展的线索，聚焦于分布式的重构、支持更多的平台如Windows Server 2016、拆分功能。最后Porterie评论说：```"目前Docker引擎和Docker Swarm有很多重叠的地方，我们会决定使用Docker引擎来作为通用的基础"```。


查看英文原文：[Docker 1.0 Brings Improvements on Networking,Storage and Clustering](http://www.infoq.com/news/2015/11/docker-1.9)
