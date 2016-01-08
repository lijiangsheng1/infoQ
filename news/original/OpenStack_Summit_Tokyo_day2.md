# OpenStack 峰会2015东京站第二天

## 摘要：
笔者接着带领大家领略OpenStack峰会2015东京站的风采，经过了昨天一整天狂轰滥炸式的洗礼，笔者已经面对各种精彩的主题变得六神无主，详细阅读了[日程表](https://openstacksummitoctober2015tokyo.sched.org/print?iframe=yes&w=i:100;&sidebar=yes&bg=no)之后，笔者最后还是狠心选择了几个主题，比如和OpenStack创业相关的、备受大家关注的项目Magnum、国内OpenStack的生态总结等，就这些主题和大家作详细的分享。至于其它笔者无法分身去参加的主题，还请各位到其官网上看[视频](https://www.openstack.org/summit/tokyo-2015/videos/presentation/day-2-openstack-summit-keynote)。

--------------------------------------------------

在正式和大家分享这些小的主题之前，我们先来看下今天的Keynote，由OpenStack基金会首席运营官Mark Collier主持，相比昨天的Keynote今天则相对要更加的务实一些，Mark Collier先是重申了官方发布的[项目浏览](http://www.openstack.org/software/project-navigator/)，强调了核心项目、外围项目、以及正在孵化中的项目，OpenStack正在向对更多的技术的支持，接下来，Mark Collier称自己喜欢数据分析，它带来了Liberty发布的相关数据分析，他给大家展示了Liberty中的那个项目的提交数量最多，当仁不让的是Neutron，Neutron的使用者从2014年的68%发展到2015年的89%，成为继计算、存储之后迅猛发展的一个项目，背后的原因是SDN和NFV，前者的市场发展超过分析师预期的2倍还多，所有这些的原因都是因为电信运营商们业务的需求，随后，Mark Collier列举了目前全球最大的网络产品／技术供应商全部支持OpenStack。接下来，Mark Collier介绍了Liberty对于基于角色访问控制和可插拔的IP地址管理的改进，以及对NFV的增强，QoS的API等等。

Mark Collier接着请出了Neutron的PTL－kyle Mestery来讲述Neutron的前世今生，包括当前发布的一些特性，最后，由于OpenStack对于容器的支持，给网络带来新的挑战，项目Kuryr由此而生。这里有个小的插曲，就是当Kyle想要给大家演示Kuryr时，不知何故，Demo出现了问题。看来现场演示程序还是存在风险。

接下来的用户故事讲述是NTT，演讲者是NTT Resonant公司的Toshio Nishiyama，他和大家分享了他们运营GOO的故事，当然主要是关于使用OpenStack，为什么使用，目前的使用情况，以及未来的规划等，后来等用户故事如韩国电信供应商SK电信、日本的Rakuten和CyberAgent都是这样的风格，所以笔者在此就略过。不过还是强调下，SK电信是值得借鉴的，包括其使用OpenStack的思路，和厂商合作开发、以及运维方面的创新，演讲视频在[这里](https://www.openstack.org/summit/tokyo-2015/videos/presentation/skts-journey-toward-platform-company-with-5g-network-and-openstack)。

比较有意思的是Rackspace的演讲者，首先他们推出了和Intel合作为开发者免费使用的[1000台机器](http://go.rackspace.com/developercloud)，然后Adrian Otto（来自Rackspace的分布式架构师，也是Magnum项目的PTL）发布Rackspace的容器产品－carina，这里精彩的地方在于Adrian将演示如何使用Carina的过程交给他儿子，看起来不到12岁的小朋友，只需简单的几步就可部署、启动Docker容器和集群。可谓是非凡的创意。

最后是IBM的精彩分享，IBM是如何支持OpenStack的，来自IBM的工程师对OpenStack做了多少贡献，以及IBM Bluebox对于云的定位和理解，最后的疯狂是希望大家举起藏在会场所有人椅子下面的荧光棒，欢迎加入IBM！看来IBM对于OpenStack的人才是多么的求才若渴。

接下来，笔者和大家分享一下自己亲自参加的分会场，而不是昨天那样，给大家做个分类介绍，尽可能的尝试不同的视野给大家。
笔者参加的第一场是[借助OpenStack的成长投资商在亚洲的机会](https://openstacksummitoctober2015tokyo.sched.org/event/54f970f0923080761f521fbc9d582af7?iframe=no&w=i:100;&sidebar=yes&bg=no#.VjDO_xArLwc)，由来自Midokura的Dan Mihai Dumitriu主持，三位来自投资界的一场讨论。大体的意思是基础设施等投资，他们都比较谨慎，因为不像应用市场，可以多投几家，只要有一、两家成功就好。相对作基础设施等门槛高，创业者也少，但还是很看好这方面的机会。

笔者参加的第二场是[发行版：不要再犯“那样”的错误了](https://openstacksummitoctober2015tokyo.sched.org/event/e150d6883fd36ee66c5b4820864e56a8?iframe=no&w=i:100;&sidebar=yes&bg=no#.VjDRuRArLwc)，由BlueBox的CTO－Jesse Proudman分享其创业期间的思考，最后告诫大家不要再重复去做OpenStack的发行版了，其它方向也有很多出路，Jesse是位精彩的演说家，其将自己基于OpenStack创业的心理路程和大家做了分享，包括痛苦的突破。最后终于带领大家将Bluebox走向成功。其中在演讲中提到了ZeroStack的创新，值得大家思考。
笔者参加的第三场是[禅和OpenStack运维团队管理的艺术](https://openstacksummitoctober2015tokyo.sched.org/event/47f3ed41f5f0de27b083079067607d86?iframe=no&w=i:100;&sidebar=yes&bg=no#.VjDSbhArLwc)，来自Rackspace的公有云的两位一线工程师分享了他们管理公有云方面的经验，并简单介绍了RackSpace内部的使用情况，如Hypervisor全部使用的是Xen，对于自动化运维、监控、主机部署等等的干货分享，也提到了他们一些开源的工具。
笔者参加的第四场是[OpenStack Magnum：容器即服务](https://openstacksummitoctober2015tokyo.sched.org/event/c8961541348884b85a05cc8a3c9a5a71?iframe=no&w=i:100;&sidebar=yes&bg=no#.VjDSpxArLwc)，由Magnum的PTL－Adrian Otto给大家带来OpenStack新的服务的介绍，包括简短的历史、特性、支持的集群管理工具、API等，由于Docker容器技术最近等火爆，所以大家都比较关心此项目，最后都提问环节，大家就Mesos、Swarm、Kubernetes的疑问询问了Adrian，甚至问Google参与OpenStack的真实意图。
笔者参加的第五场是[在中国OpenStack社区迎来新的高峰](https://openstacksummitoctober2015tokyo.sched.org/event/305787e971ab36ce7dcb1c5810aa0e9a?iframe=no&w=i:100;&sidebar=yes&bg=no#.VjDSqBArLwc)，这是纯粹的国人分享，分别由来自intel中国的OpenStack市场经理maggie liang、OpenStack中国开源大使叶璐、以及华为云计算的Zhen Zhuang各自分享了OpenStack在中国的情况。首先，Maggie分享了国内的云计算市场情况，政府的支持力度，以及Intel参与投资的几家基于OpenStack的公司的状况；然后叶璐分享了国人参与OpenStack一些数据，包括国内公司在Liberty的代码贡献排名、国内的PTL、各个项目的核心贡献者、国内举办活动的热度等等，给人眼前一亮的感觉；最后Zhen Zhuang分享了华为在OpenStack方面的贡献，包括和Intel联合举办黑客松会议、在各个项目中来自华为的工程师们的贡献排名、最后介绍了华为的OpenStack产品等。

相信最后这场是大家最为感兴趣的，笔者会在明后天，对各种详细的数据和谈话作详细的介绍，敬请期待。


