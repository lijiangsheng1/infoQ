#EC2 容器服务介绍

## 摘要：

亚马逊关于容器的管理和集群服务－ECS的介绍，通过一步步的实例来部署第一个容器集群及其底层的任务和服务。


-----------------------------------------------------------------

[EC2容器服务](https://aws.amazon.com/ecs/details/)(ECS)是亚马逊web服务(AWS)新发布的一款产品。

ECS的目的是让[Docker](http://docker.io/)容器变的更加简单，它提供了一个集群和编排的层，用来控制主机上的容器部署，以及部署之后的集群内的容器的生命周期管理。

ECS是诸如[Docker Swarm](https://docs.docker.com/swarm),[Kubernetes](http://kubernetes.io/),[Mesos](http://mesos.apache.org/)等工具的替代，它们工作在同一个层，除了作为一个服务来提供。这些工具和ECS不同的地方在于，前者需要你自己来部署和管理，而ECS是“作为服务”来提供的。

ECS是基于一种专有的集群技术，而不是通过诸如Docker Swarm,Kubernetes,Mesos等引擎实现的。这可以和[Google容器引擎](https://cloud.google.com/container-engine)(GCE)作一对比，GCE后台使用的就是基于Kubernetes的。


##我们为什么需要容器编排？

由ECS，Swarm，或者Kurbernetes所提供的容器编排这一层，在整个部署和运行基于容器的应用程序的整个蓝图中占有非常重要的位置。

首先，我们为了可扩展性需要容器组成集群。随着我们负载的增长，我们需要增加更多的容器，横向的扩展它们，跨服务器来并行的处理更高的负载。

第二，我们需要组建容器集群来保证健壮性和高可用性。当一台主机或一个容器失效时，我们希望容器可以重新构建，或许是在另外一台健康的主机上重新启动，从而让整个系统不会受到任何的影响。

最后，编排层的工具所提供的一个重要功能就是抽象，让开发者远离具体的底层实现细节。在容器化的世界中，我们毋需关心每个独立的主机，只需要关注我们期望的容器有多少在运行，在‘适当的地方’运行。编排和集群工具为我们做这些，让我们能够轻松的将容器部署到集群中，而且还能够计算出最佳的调度方式，从而决定容器应该运行在哪些主机上。

设计健壮性和高性能分布式集群系统的难度是非常大的。所以诸如Kubernetes和Swarm这样的工具让我们自己毋需去构建集群。ECS借此更进一步，通过简化编排层的设置、运行和管理来实现毋需人工参与。基于此缘故，ECS无疑是哪些使用容器来运行应用的开发者们应该密切关注的项目。

##ECS架构

ECS并非是一个黑匣子的服务，它运行在你的EC2服务实例中，你可以使用SSH登录，像管理其它的EC2服务一样进行管理。

在集群中的EC2服务均会运行着一个ECS代理，ECS代理是一个连接主机到中心的ECS服务的轻量级进程。ECS代理响应主机注册到ECS服务，且掌控所有的请求，用于容器的部署或者是诸如启动／停止容器之类的生命周期事件。顺便说一下，[使用go实现的ECS代理](https://github.com/aws/amazon-ecs-agent)已经开源。

当创建一个新的服务器时，我们既可以选择手动的配置ECS代理，也可以选择使用预构建的已经配置完毕的AMI镜像。

通过亚马逊CTO Werner Vogels的[博客](http://www.allthingsdistributed.com/2015/07/under-the-hood-of-the-amazon-ec2-container-service.html),我们得知集中的服务已经逻辑上分为集群管理和在主机上控制容器部署的调度。这背后的缘由就是让容器的调度成为可插拔式的，所以我们甚至可以使用其它的调度器，例如Mesos或者是其它开发者自定义的调度器。自定义调度器的文档在本文撰写时还在开发当中，但是我们可以阅读[此博客](https://aws.amazon.com/blogs/compute/cluster-management-with-amazon-ecs/)以及参考其[源代码](https://github.com/awslabs/ecs-mesos-scheduler-driver)，这是目前为止最佳的参考实践。

下面的示意图很好的演示了ECS集群的逻辑层次：容器实例包含多个任务，任务包含多个容器，EC2容器实例集群可以分散到多个可用区域中，Elastic Load Balancers可以用于跨任务的动态分布负载。此图可以帮助读者在阅读接下来的内容整理思路。

![first image](http://cdn.infoq.com/statics_s1_20150922-0305u2/resource/articles/intro-aws-ecs/en/resources/devops-1.jpg)
[图片来源](http://www.allthingsdistributed.com/2015/07/under-the-hood-of-the-amazon-ec2-container-service.html)

##服务和任务

在ECS中，Docker负载被描述为任务。

一个任务本质上是定义了一个或多个容器，其中包括你打算运行的容器的名称（和[Docker Hub](https://hub.docker.com/)的名称保持一致），以及在容器实例启动时相应的端口和磁盘卷的映射信息。

当任务运行时，则启动了底层的容器。当所有的容器进程完成使命时，任务也就结束了。任务既可以是很短的也可以是长时间运行的，举例来说，提供一个数据处理任务的短的事件驱动，或者是一个web服务进程。

这里需要提醒一件事情，那就是架构上给定的一个任务，其所有的容器均运行在同一台主机中。如果我们打算定位容器的话，那么就使用在同一个任务下来组织它们的方法来实现。如果我们打算将服务运行在不同的主机，我们则仅需定义多个任务来实现控制即可。初看这似乎是一种约束，但最终它给我们的和[Kubernetes pods](http://kubernetes.io/v1.0/docs/user-guide/pods.html)一样的对容器定位在一定程度的控制能力。

为了说明上述问题，如下面截图所示，我们可以看到定义了一个特定的任务，此任务拥有一个容器，容器托管nginx web服务。

![second image](http://cdn.infoq.com/statics_s1_20150922-0305u2/resource/articles/intro-aws-ecs/en/resources/devops-2-small.jpg)

除了任务之外，服务是ECS概念中排名第二重要的。一个服务是给定一个任务所请求运行的特定的实例数量。举例来说，如果我们有一个如上述所定义的运行nginx web服务容器的任务的话，我们则要定义一个服务，来请求3个或更多的实例组成集群，从而完成web服务的任务。

服务是ECS如何提供弹性的保证。当一个服务启动后，服务就会监控其中的任务是否是活动的，实例的数量是否正确，以及其中容器的数量是否正常。如果任务停止运行了，或者是无响应了，又或者是出现问题了。服务就会请求启动更多的任务，以及必要的话清理任务。

下面截图所示，在集群中一个nginx服务被定义为3个运行的任务。这些任务个个都处于运行状态。

![nigix service](http://cdn.infoq.com/statics_s1_20150922-0305u2/resource/articles/intro-aws-ecs/en/resources/devops-3-small.jpg)

##部署第一个容器

当用户第一次使用终端访问ECS服务时，会看到一个简单的向导。尽管手动的去配置ECS也不是多么繁重的事情，但是第一次的话，使用该向导还是值得尝试的，它能够为你配置好所有－你的EC2服务器，一个合适的安全组，以及一个自动伸缩组，正确的AMI（此AMI内置了ECS代理），等等。这是启动和运行，并获得ECS经验的最快方法。

![getting started](http://cdn.infoq.com/statics_s1_20150922-0305u2/resource/articles/intro-aws-ecs/en/resources/devops-4-small.jpg)

###步骤1 定义任务

首先，作为向导的一部分，我们需要定义任务。这个演示的目的,我们将使用免费的NGINX的Docker镜像。（NGINX是一款开源的web服务软件，已经被社区容器化了，并[上传到了官方hub](https://hub.docker.com/_/nginx/)。）

以为容器指定一个名称开始，例如本示例为*nginx-task*。

![nigix task](http://cdn.infoq.com/statics_s1_20150922-0305u2/resource/articles/intro-aws-ecs/en/resources/devops-5-small.jpg)

接下来，点击*添加容器定义*，即定义nginx容器。	这里主要需提醒的是镜像的名称，务必和Docker hub([ngnix](https://hub.docker.com/_/nginx/))上公开的镜像名称一致。当然，也可以[指定专有镜像](http://docs.aws.amazon.com/AmazonECS/latest/developerguide/private-auth.html)。

内存字段是内存的最大值，以兆字节计算，这是用于分配给运行中的容器的。CPU单元是一个抽象的数字，每个CPU核心有1024个单元，此数字即是要赋予的单元数。

此信息用处非常的大，因为它增加了一定程度的灵活性以及智能的容器调度。ECS将监视那些实例拥有空闲资源，然后智能的分配容器，从而达到实现有效的利用服务器资源的目的。

![task detail](http://cdn.infoq.com/statics_s1_20150922-0305u2/resource/articles/intro-aws-ecs/en/resources/devops-6-small.jpg)

###步骤2 定义服务

第二步，我们需要定义服务，即描述为此任务要在集群中运行多少个实例。

选择创建服务的单选框，为服务命名，本例为nginx-service，然后设置要运行的任务数，本例为3。这就意味着此服务一旦运行起来，就会创建3个任务，每个任务就是一个独立的实例，每个实例中都运行着nginx容器。

至于更加复杂的配置，你可选择Elastic Load Balancer (ELB)，然后在它们被实例化后动态的将服务注册到ELB，并实现集群化。这些在后面有详细的描述。

![define service](http://cdn.infoq.com/statics_s1_20150922-0305u2/resource/articles/intro-aws-ecs/en/resources/devops-7-small.jpg)

###步骤3 创建ECS集群

我们需要创建EC2服务器的集群，这些服务器是用来运行容器的。此演示环境使用3个t2.micro实例即可实现预料的效果。这也就意味着1个任务和1个容器将分布到这3台服务器的每一个上。我们当然也可以实现在集群中使用实例多于任务的配置，或者使用这些服务器来运行不同的任务，但是目前还未能实现在同一台服务器中运行给定任务的多个实例。

选择你首要的密钥对，然后点击后面的按钮以创建[IAM角色](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html)，IAM角色非常重要，有了它，集群中的主机就可访问中央ECS服务了。

![create ecs cluster](http://cdn.infoq.com/statics_s1_20150922-0305u2/resource/articles/intro-aws-ecs/en/resources/devops-8-small.jpg)

###步骤4 创建栈

向导的最后一步是展示汇总任务、服务、和集群的配置。

页面如下所示会展示所生成的JSON代码，这些代码同样可以用于命令行，如果有人习惯于使用命令行的话，或者是打算自动创建它们的集群的话。

![create stack](http://cdn.infoq.com/statics_s1_20150922-0305u2/resource/articles/intro-aws-ecs/en/resources/devops-9-small.jpg)
在创建过程中，你会看到使用Cloud Formation来构建栈。构建栈可能要花上2到3分钟的时间。

![wait](http://cdn.infoq.com/statics_s1_20150922-0305u2/resource/articles/intro-aws-ecs/en/resources/devops-10-small.jpg)

###步骤5 回顾栈和NGINX服务

现在若是访问EC2的面板，我们可以看到已经创建好的服务器，且是处于运行状态的。向导已经帮助我们创建了跨可用区域的主机以演示弹性的好处。
![running task](http://cdn.infoq.com/statics_s2_20150922-0305u1/resource/articles/intro-aws-ecs/en/resources/devops-11-small.jpg)

然后回到ECS面板，就可以检查服务了，当然我们希望看到的是它处于准备好的状态，且拥有3个任务。

记住，在创建实例的过程要花费几分钟的时间，从hub拉下容器镜像启动也要花费几分钟的时间，以及服务达到可用状态也会花费一些时间，所以，不用担心这整个过程会稍有些慢。

![review stack](http://cdn.infoq.com/statics_s1_20150922-0305u2/resource/articles/intro-aws-ecs/en/resources/2devops-13-small.jpg)

深入服务中某个任务的细节，我们会看到任务处于RUNNING（运行）状态。

![running statc](http://cdn.infoq.com/statics_s1_20150922-0305u2/resource/articles/intro-aws-ecs/en/resources/1devops-14-small.jpg)

展开*nginx-container*。在外部链接下方，我们可以看到一个HTTP链接，指向任务内的容器。

点击此链接，我们可以看到的是Nginx容器所提供的web欢迎页面。

![access nigix](http://cdn.infoq.com/statics_s1_20150922-0305u2/resource/articles/intro-aws-ecs/en/resources/1devops-15-small.jpg)

此时，我们完成了将NGINX容器部署到ECS的步骤，而且可通过web浏览器访问NGINX服务。现在你可以考虑整理下思路和对概念的验证了。

##后续步骤
在建立了一个简单的容器之后，我们接下来为了将应用部署到生产环境，需要做一些更加高级的配置。
###ELB负载均衡
在上述的例子中，我们使用浏览器直接链接到三个容器中的一个，实现对NGINX的访问。这不能够做到健壮性，理论上当容器宕机，或者是重新启动到不同的服务器上，那么原来指定的静态IP地址就不在有效了。

我们可以将服务注册到[EC2 Elastic Load Blance](https://aws.amazon.com/elasticloadbalancing/)（ELB）以实现动态的地址。作为底层的任务不管如何的启动、停止以及在EC2实例池中如何的移动，ELB都可以通过服务保持最新，能够将相应的流量路由到正确的地址。

要配置负载均衡，我们首先需要在EC2的面板中创建一个ELB。然后重新创建服务，在服务创建的过程中将ELB添加进来，如下面截图所示：

![elb loadblance](http://cdn.infoq.com/statics_s1_20150922-0305u2/resource/articles/intro-aws-ecs/en/resources/devops-16-small.jpg)

###自动伸缩

ECS也可以整合[EC2 autoscaling](https://aws.amazon.com/autoscaling/)，而且也是在面临增加的负载时扩充集群的首选方法。

Autoscaling的工作要依赖于对诸如CPU，内存和IO的计量监控的，而且添加节点或删除节点是在打破一定的条件时候进行的。

实例化后的新的节点会自动注册到ECS集群中，然后才有资格成为未来部署容器的实例。

这很实用，但是目前ECS还没有实现扩充任务数量或者是增长容器集群的Hook。但我们仍然能在新的容器启动后加入到新的规模的集群中受益，我们可以通过GUI或[API](https://aws.amazon.com/blogs/compute/scaling-amazon-ecs-services-automatically-using-amazon-cloudwatch-and-aws-lambda/)来引入新的容器到集群，并能在更大规模的集群中分发负载。

###容器链接

当在任务中定义容器时，是可以使用[Docker原生的容器链接](https://docs.docker.com/userguide/dockerlinks)来实现它们之间彼此的互连互通。

这样就不在需要静态的端口映射或者是多容器环境中的服务发现了，让部署分布式的微服务更加的轻松。

###AWS 命令行工具
虽然上面的演练是基于UI控制台，但[ECS完全整合到了AWS命令行中](http://docs.aws.amazon.com/AmazonECS/latest/developerguide/ECS_AWSCLI.html) 。

###故障排查

若发生了问题，你可以通过SSH直接访问集群的节点，以进行调试。

为了能够使用SSH登陆到节点，你需要在安全组中打开22端口，因为通过向导所创建的节点默认不会打开此端口。

登陆到服务器节点后，你就可以查看ECS代理的日志文件:/var/log/ecs了。

你也可以运行标准的Docker命令，例如，*docker images* 和 *docker ps* ，来参看服务器上的镜像和容器的状态。

##总结

本文的目的是对ECS做一介绍，且讲述了一个实际演示环境的例子，即部署你的第一个容器集群。

ECS是一款新的产品。很多功能还不是很健全，但是它目前足够的稳定。我们在我们的测试环境中创建了超过100+个节点的集群，试验了容器和节点的失效切换，测试了自动伸缩、负载均衡、运行服务，均表现良好。现在我们打算为一些客户提供ECS到它们的生产环境。

ECS以及和它等同的Googel Container Engine对于容器生态系统来说都是非常重要的。基于容器开发代码和部署变得更为容易，在其上运行诸如Kubernetes或Mesos的编排层，对于普通用户来说这是进入成熟的标记。ECS为容器提供了一个简单的、可访问的、稳定的、类似PaaS平台的产品，这非常的令人兴奋，尽管它现在还处于整个进化过程的早期阶段。


##关于作者
![image of author](http://cdn.infoq.com/statics_s1_20150922-0305u2/resource/articles/intro-aws-ecs/en/resources/BenjaminWootton.jpg)Benjamin Wootton是[Contino](http://www.contino.co.uk/)的联合创始人和首席顾问，Contino是一家英国的咨询公司，主要是为一些企业提供DevOps，持续交付工具等方面的实践和方法。


查看英文原文：[Introdcution to EC2 Container Service](http://www.infoq.com/articles/intro-aws-ecs)
