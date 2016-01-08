#Mirantis 发布其旗舰产品 7.0

## 摘要：
日前，Mirantis发布了其OpenStack产品：Mirantis OpenStack 7.0,此版本基于OpenStack Kilo,能够适应更加复杂的环境，增强了对VMware NSX-v 软件定义网络的支持，以及对大数据集群并行部署的支持。

--------------------------------------------------

日前，[Mirantis](https://www.mirantis.com/)发布了其产品-[Mirantis OpenStack 7.0](https://www.mirantis.com/products/mirantis-openstack-software/what-is-new-in-7-0/),此版本基于的OpenStack版本是[kilo](http://www.openstack.org/software/kilo/)，主要的更新是，可以适应更加复杂的环境和负载，增强了对VMware NSX 软件定义网络的支持，以及对大数据集群并行部署的支持。


其产品中所基于上游的OpenStack版本是OpenStack基金会在今年4月份在加拿大的峰会上发布的版本－OpenStack Kilo。它是历史上OpenStack的第11个版本。其主要引进的组件有[Ironic](https://wiki.openstack.org/wiki/Ironic)和[Murano](https://wiki.openstack.org/wiki/Murano)，前者是一款裸金属部署的服务，后者是应用程序目录的服务。Kilo也对原有的核心项目进行了改进，如核心程序Nova，Cinder，Neutron等等，更多细节，请参考其官方的[发行注记](https://wiki.openstack.org/wiki/ReleaseNotes/Kilo)和[官方报道](http://www.openstack.org/software/kilo/press-release/)。

在短短的5个月之后，Mirantis就整合进其最新的版本，不可谓不大胆，不过是有充分多理由的，在整个Kilo版的开发中，Mirantis所[修复bug的数量按照公司排名它是第一](http://stackalytics.com/?metric=resolved-bugs&release=kilo)，根据其[blog](https://www.mirantis.com/blog/mirantis-openstack-7-0-enhances-resilience-at-scale/)记录，也对Kilo版作了大量的测试，覆盖了Murano，Sahara，Ceph等项目。对稳定性和安全性有所改进和加强。

此外，Mirantis还反向移植了OpenStack Liberty的代码，对于增强的Kilo版，按照组件有下面特性：

* Cinder：可以将卷给多个虚拟机，可扩展和加密的卷。
* Neutron：使用分布式虚拟路由(DVR)扩展了南北流量。
* Glance： 管理员可以停用镜像。
* Keystone： 多层次的租户完美无缝构建混合云。
* Horizon： 从某主机迁移实例时会标记此实例为维护。
* Sahara： 可并行的部署多个Hadoop和Spark集群。

Murano应用目录，增加了支持vCenter和Windows的应用、增强的角色访问控制、以及可插拔的基础设施编排等。另外，在支持的应用中，其中很大的一个亮点是对Docker的集群管理[Kubernetes](http://kubernetes.io/)的整合和支持。

在商业的合作上，Mirantis在此版本加大了和各家硬件厂商的兼容认证,详情见[认证的驱动列表](https://www.mirantis.com/partners/unlocked-partner-catalog/)；整合、认证了更多的Fuel的插件，[完整插件列表](https://www.mirantis.com/products/openstack-drivers-and-plugins/fuel-plugins/)；整合了VMware网络产品，如VMware NSX-v 和VMware分布式交换机（VDS）；和HortonWorks进行合作，在大数据的方面和HortonWorks HDP 进行了相互测试和增强的开发。

Mirantis OpenStack的管理部署工具的上游版本是[Fuel](https://www.fuel-infra.org/)，此次Mirantis OpenStack 7.0是基于上游的Fuel7.0版本，相对于其6.1版本，7.0也有很多的改进，如网络模版支持、回滚一个节点到过去的某个状态、配置主机名、管理网络绑定支持等等，其[发行注记](https://docs.mirantis.com/openstack/fuel/fuel-7.0/release-notes.html)非常详细的描写了Fuel7.0的变化，以及修复的Bug描述。

这里有一个[YouTube视频](https://youtu.be/DPYNK68toRY)，生动的说明了这一产品点主要更新和特性支持。从[这里](https://www.mirantis.com/products/mirantis-openstack-software/what-is-new-in-7-0/)可以下载和试用Mirantis OpenStack 7.0。




