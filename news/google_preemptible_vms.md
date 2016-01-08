# Google 抢占式虚拟机准备就绪

## 摘要：
在测试版推出了几个月之后，Google发布了作为其Google Compute Engine云的一部分－抢占式虚拟机全面上市。抢占式虚拟机相比于Google所提供的其它虚拟机有着价格上的绝对优势，但是它随时可能被关机，Google只会提前发出30秒的警告。

--------------------------------------------------

在[测试版](http://www.infoq.com/news/2015/05/google-preemptible-vm)推出了几个月之后，Google发布了作为其Google Compute Engine云的一部分－抢占式虚拟机[全面上市](http://googlecloudplatform.blogspot.com.es/2015/09/Compute-Engine-Preemptible-VMs-now-generally-available.html)。抢占式虚拟机相比于Google所提供的其它虚拟机有着[价格上的绝对优势](https://cloud.google.com/compute/pricing#machinetype)，但是它随时可能被关机，Google只会提前发出30秒的警告。

除了随时可能被终止之外，抢占式虚拟机还有更多的[限制](https://cloud.google.com/compute/docs/instances/preemptible):
*它们的最大的连续运行时间为24小时;
*它们可能不总是可用的;
*它们不能够进行在线迁移，而且在维护事件之后也不能重新启动。

必须要注意的是，抢占式实例并不会影响到[收费操作系统])https://cloud.google.com/compute/pricing#premiumoperatingsystems)到价格计算。例如，如果你安装了红帽企业版Linux，且在运行抢占式实例之前运行了35分钟，你就要付一个小时的费用。另外一方面，SUSE和Windows服务器镜像，均是以分钟来计算付费的，最少为10分钟。

来自Google云平台的高级产品经理[Paul Nash](https://www.linkedin.com/in/paulrnash)如是[说](http://www.bio-itworld.com/2015/9/8/google-launches-preemptible-virtual-machines-cycle-broad.aspx):

```
我们在Beta版和正式发布之间所做的主要工作就是优化平衡性以及看它们在生产环境是如何工作的。所以我们不会自动的突然将某个实例分离出来，所以我们能够保持非常低的中断率。
```

根据[ 最初的基准测试](https://www.reddit.com/r/sysadmin/comments/36duq1/introducing_preemptible_vms_a_new_class_of/crryh9t),它的表现为在一个拥有50个实例的池中，大约每5分钟就会有一个实例被终止。而根据另外一篇[早期的报告](https://news.ycombinator.com/item?id=9564122),"一个虚拟机通常的运行时间为10-20分钟"。

在[infoQ的采访中](http://www.infoq.com/news/2015/05/google-preemptible-vm)，Paul Nash 解释说，当一台虚拟机称为抢占式的时候，它只是可能随时被终止，但是它的磁盘却可以永久的保留，所以不会造成数据丢失，而且稍后当抢占资源可用时还可恢复到正常工作。然而，目前还不能做到将抢占式的虚拟机在线迁移到非抢占虚拟机。

在他们的发布长文中，Google还提到了在测试期间，整合了一些框架和产品到Google抢占式虚拟机中，包括[Cycle Computing](http://cyclecomputing.com/),一家提供目标为管理和扩展大型计算负载的产品套件，原来仅支持AWS；以及[Zync]（https://www.zyncrender.com/）,一家提供渲染解决方案的公司。

Google的抢占式虚拟机进入的是和6年前AWS Spot 实例相同的领域，AWS Spot 实例的特点是根据竞价机制而不断变化的价格，根据一些相关的[早期的分析](https://gigaom.com/2013/10/08/bidding-strategies-arbitrage-aws-spot-market-is-where-computing-and-finance-meet/),Spot 实例仅仅比所有的其它AWS 实例价格低5%。目前还没有数据公布关于Google抢占式虚拟机进入这个领域相关的内容，然而，Nash号称“系统已经被大量的使用”有成千上万个任务已经启动。


查看英文原文：[google preemptible vms now out of Beta](http://www.infoq.com/news/2015/09/google-preemptible-vms-available )
