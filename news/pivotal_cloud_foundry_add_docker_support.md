#Pivotal Cloud Foundry 新增Docker和Netflix OSS服务的支持 

## 摘要：
今天，Pivotal发布了Pivotal Cloud Foundry（PCF）的升级，PCF是非常流行的用于构建、部署和运行Cloud-native应用的开源平台Cloud Foundry的商业版本。此次1.6版本的发布，给了开发者可以原生访问Spring云平台的Netflix OSS服务的子集、内置.Net应用的支持、对Docker镜像的内测支持、以及集成ALM工具等。

--------------------------------------------------

今天，[Pivotal](http://pivotal.io/)发布了[Pivotal Cloud Foundry](http://pivotal.io/platform)（PCF）的升级，PCF是非常流行的用于构建、部署和运行Cloud-native应用的[开源平台Cloud Foundry](https://www.cloudfoundry.org/)的商业版本。此次1.6版本的发布，给了开发者可以原生访问Spring云平台的Netflix OSS服务的子集、内置.Net应用的支持、对Docker镜像的内测支持、以及集成ALM工具到源码控制和持续集成。InfoQ和Pivotal云平台的总经理兼副总裁James Watters进行了交流，以了解更多的内幕。

开源项目[Cloud Foundry](https://www.cloudfoundry.org/)－过去称之为平台即服务（PaaS），但是现在更加的倾向于cloud-native平台－－[包括](http://docs.cloudfoundry.org/concepts/architecture/)了应用程序在运行时的自我修复、支持更多的开源编程语言和开发框架、部署工具、集中的日志、健康监控、以及应用服务框架等等。Pivotal在[2013](https://gigaom.com/2013/11/12/pivotal-releases-commercial-cloud-foundry/)整合后发布了其第一个商业版的Cloud Foundry。它提供“企业级”的特性，如基于web的管理界面、可以安装到各种流行的基础设施中的软件包、应用服务市场、以及专业的支持。Watters告诉InfoQ，PCF的第一个版本仅能在vSphere环境中运行，但随后的1.x版本就对多个云平台做了支持。PCF现在可以原生的运行在vSphere、OpenStack、AWS、以及CenturyLink等云平台中。此次1.6版本还增加了对微软Azure的支持。

据Watters透露，新版本的PCF聚焦于技术组织来写[12-factor](http://12factor.net/)或者cloud-native的应用。Pivotal过去在Java上做了很多的创新，尤其是[Spring框架](http://spring.io/)。Netflix是构建弹性cloud-native应用的典范，而且和[Pivotal进行合作](http://blog.pivotal.io/pivotal-cloud-foundry/products/spring-cloud-helps-netflix)添加了很多[开源的Netflix服务](http://netflix.github.io/)的支持到项目中，而这个项目就是[Spring云](http://projects.spring.io/spring-cloud/)。基于对[Spring Boot](http://projects.spring.io/spring-boot/)的支持，（现在叫Spring云服务），Watters称PCF是“运行cloud－native的应用是可选的，不行就创建它们”。PCF所提供的Spring云驱动的服务有：

* [配置服务](http://docs.pivotal.io/spring-cloud-services/config-server/index.html)。Cloud Foundry提供基本的轻量级的[环境变量](http://docs.cloudfoundry.org/devguide/deploy-apps/environment-variable.html)来存储共享的配置，但是配置服务可以做的更多，它是基于Git的服务，这就意味着可以跨开发／测试／生产环境中使用，而且可无缝集成到Spring的应用中。
* [服务注册](http://docs.pivotal.io/spring-cloud-services/service-registry/) 。基于Netflix的[Eureka](https://github.com/Netflix/eureka/wiki)项目。它为运行在PCF的Spring应用提供了自动发现功能。开发者再也不用硬编码来处理依赖服务了，开发者可以在运行时使用服务发现来注册和定位服务。
* [断点仪表](http://docs.pivotal.io/spring-cloud-services/circuit-breaker/)。弹性的分布式系统可防止连锁的失效。来自Netflix开源软件的[Hystrix](https://github.com/Netflix/hystrix)就是此断点模式的实际实现。PCF的用户可以用此来应对Spring云服务的失效情况，且可提供失效切换直到有问题的服务恢复正常。

Pivotal在PCF中还对基于Windows的.NET应用提供了官方的支持，[Pivotal发行注记](http://pivotal.io/platform/press-release/go-from-idea-to-production-in-less-than-a-day)中称：

>>由于在这个最新的版本中采用了新一代的运行时交付，使得.NET应用程序现在可以运行在Pivotal Cloud Foundry中了。基于这个为.NET所扩展的支持，企业可以得到由基于Linux和Windows应用的所组成的异质环境的支持。.NET的应用会以原生的姿态运行在Windows Server 2012 R2 Hyper-V的虚拟机中，且PCF可以使用相同的命令来管理这些应用，还有像已有的应用那样活的相同一致的Day 2运维好处。

Watters说道，从用户的角度来看，.NET的应用在PCF中受到一流的待遇，像其它所有支持的语言和框架一样都能够做到本地服务发现、健康管理、伸缩、以及开发工具的支持。然而，Spring 云服务不能够支持.NET的应用，还有运维人员也不能使用[发布管理工具BOSH](http://bosh.cloudfoundry.org/)来部署需要的Windows Server 2012 主机服务器。Watters表示，这些差别很快就会被弥补。

Docker 在现代的平台和维服务讨论中绝对是占主导地位的。Pivotal通过为PCF增加（测试）运行Docker容器的支持来加入这个阵营，Pivotal[描述了](http://pivotal.io/platform/press-release/go-from-idea-to-production-in-less-than-a-day)它是如何工作的基本原理。

>>Docker的应用现在可以使用Pivotal Cloud Foundry平台的功能了，诸如调度、健康管理、负载均衡、企业身份、日志、以及多个云平台的支持等。现在仍处于测试阶段，原生Docker镜像的支持使新的运行时弹性成为可能，且让Pivotal Cloud Foundry能够在今天的市场中利用容器管理系统的优点。用户可以在Pivotal Cloud Foundry中部署应用时使用来自公网的拥有安全的注册处的Docker镜像，比如Docker Hub。

Watters告诉InfoQ，当开发者向PCF推送一个应用时，他们是可以使用注册处位置的链接的，从而下载Docker镜像然后将之部署到平台中的。然而，Watters澄清说，“支持Docker”并不是意味着开发者可以随意的拉下任意的Docker镜像、有状态、以及其它的支持如启动它们、拥有Docker的编排和管理。举例来说，是不可以部署官方的[Cassandra Docker镜像](https://hub.docker.com/_/cassandra/)的，也无法做到开发者绑定的应用作为一个服务抛给PCF。相反，Pivotal可以接受开发者在他们自己的持续集成环境中所构建的Docker镜像，PCF所支持的Docker能满足特定的某些场景。相对于成为一个通用的Docker编排引擎，它提供了一个部署代码用的备用机制。

Pivotal还在PCF中增加了内置的应用程序生命周期管理工具的支持。具体来说，Pivotal和一些老牌的持续集成／开发厂商进行合作，将这些交给最擅长的公司去做。

>>建立在流行的软件项目管理工具－Pivotal Tracker，用户可以集成Gitlab源代码核心仓库、CloudBee Jenkins持续集成、以及JFrog Artifactory二进制artifact管理使之可管理的平台版本。通过提供现代应用交付工具链的构建块，Pivotal鼓励软件企业要充满信心并加速构建和部署微服务和原生云应用。

Github是很多开源项目重要的归属地，但是其本身并不是开源的。Pivotal新的合作伙伴[Gitlab](https://about.gitlab.com/)给Watters带来很多惊喜，其强大的开源软件软代码控制服务能够接受pull request，从而获得新的特性。

谁是Pivotal视为最强大的竞争对手？据Watters透露，还是AWS。云的用户经常认为使用AWS就足矣，甚至都到了非亚马逊就没有原生云应用这么一说。但是，Watters说，“人们要想成功，就不能光是考虑亚马逊”。Watters认为Pivotal一些最优质的客户第一次自己尝试创建平台，随后就会问出“为我的组织做些什么正确的事情？”

查看英文原文：[Pivotal Cloud Foundry Adds Netflix OSS Services,Docker Support](http://www.infoq.com/news/2015/11/pivotal-cloud-foundry-netflix)
