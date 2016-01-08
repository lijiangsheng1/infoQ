# 新的Linux-Only大型机开始支持Chef

## 摘要：

IBM 前一阵子发布了LinuxOne，一个Linux－Only的硬件一体机，其上可以运行Redhat，SUSE，和Ubuntu等Linux发行版，以及在其上增加了诸如Docker，Chef等各种开源工具。此款产品目标是大中型的企业。

--------------------------------------------------

IBM 近期发布了[LinuxOne](http://www-03.ibm.com/press/us/en/pressrelease/47474.wss)这款产品，这是他们大型机战略的一次扩张，其中包括了新的硬件一体机，软件和服务解决方案，其为大中型企业提供了两种不同的Linux系统。

IBM将开启在z系统上运行开源的符合工业级标准的工具和软件之旅。IBM已公布支持[chef](http://www.infoq.com/articles/introduction-chef-development-process)和[docker](http://www.infoq.com/articles/docker-future)。同时还有诸如[Apache Spark](http://www.infoq.com/articles/apache-spark-introduction),[Node.js](https://nodejs.org/),[MongoDB](https://www.mongodb.org/),[MariaDB](https://mariadb.org/)或[PostgreSQL](http://www.postgresql.org/)等开源工具。

来自Chef公司的合作伙伴集成总监，Matt Ray，和Infoq透露了Chef技术支持的路线图：

```
我们将Chef运行在这些大型机上的Linux发行版中，同时支持客户端和服务器端，开始的时候，我们所支持的操作系统有：Redhat 6，7 和SUSE 11sp4，12 ，它们均是zlinux版，这些平台将会和我们现在在x86下的Redhat 6，7下一样，整合进我们的持续集成系统中，并在接下来的每一个版本中如期发布。
```

Chef没有支持zOS系统的版本，并且也没有将来的打算。支持zlinux 大型机意味着：“用户可以跨越所有他们的基础设施而使用一个工具就可以了。不管是运行Linux的x86，Power(同样支持)，zlinux，还是Windows，Salaris，亦或是AIX”。Ray如此总结道。

Chef即将发布具体的文档，目的是为了帮助工程师在大型机能够具体的实现Chef：

```
我们刚刚才开始开发，但是我们将会提供所有支持zLinux平台的文档...如果有任何是zLinux所需要的特殊步骤，我们都会开源并撰写好文档...颇为遗憾的是目前所集成的还没有可用的文档，我们已经和IBM达成一个工作说明，截止到12月份会发布第一个版本。
```

IBM还创建了一个[LinuxOne 开发者云](http://dtsc.dfw.ibm.com/MVSDS/%27HTTPD2.DSN01.PUBLIC.SHTML%28LNXTD%29%27),对开发者社区开放。此云扮演着一个研发引擎的角色，用于创建、测试以及整合新兴的应用程序。任职于IMB媒体关系的Joe Guy Collier是这么介绍的：“这是一个由开发者决定开发什么应用程序的云，但是这些应用可能是新的移动设备或混合的app“。

圣母大学和雪城大学信息研究学院打算免费的使用[提供给开发者访问的虚拟IBM LinuxOne的托管云](http://www.marist.edu/publicaffairs/linuxmainframe2015.html)。作为项目的一部分，IBM还为独立软件提供商(ISVs)创建了特别的云，这些云托管在达拉斯，北京和德国的伯布林根的IBM站点上，此为ISV创建的云提供应用程序厂商的访问，以及免费试用LinuxOne的资源，用来在LinuxOne和在Linux平台下应用程序的移植、测试和基准测试。

查看英文原文：[New Linux-only Mainframes Support chef](http://www.infoq.com/news/2015/09/linuxone-mainframe-chef)
