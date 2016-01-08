#亚马逊EC2容器服务最新升级，专注于自动化、可配置和可用性 

## 摘要：
亚马逊Web服务近期对其产品亚马逊EC2容器服务（ECS）进行了升级，其中包括ECS命令行接口、支持Docker Compose、允许额外Docker配置的任务定义、更新了ECS调度器新增了对可用区域的感知支持。

--------------------------------------------------
亚马逊Web服务近期对其产品[亚马逊EC2容器服务](https://aws.amazon.com/ecs/)（ECS）进行了[升级](https://aws.amazon.com/blogs/aws/ec2-container-service-update-container-registry-ecs-cli-az-aware-scheduling-and-more/)，其中包括ECS命令行接口、支持Docker Compose、允许额外Docker配置的任务定义、更新了ECS调度器新增了对可用区域的敏感支持。还声明了正在进行的一项服务－亚马逊EC2容器注册（亚马逊 ECR），且会在今年的稍晚些时候正式发布。

此次更新的亚马逊[ECS命令行接口](http://docs.aws.amazon.com/cli/latest/reference/ecs/index.html)（ECS CLI）是专门针对亚马逊EC2容器服务的命令行接口，能够提供高级别的命令，如从本地开发环境('[ecs-cli up](http://docs.aws.amazon.com/AmazonECS/latest/developerguide/ECS_CLI_reference.html#cmd-ecs-cli-up)','[ecs-cli scale](http://docs.aws.amazon.com/AmazonECS/latest/developerguide/ECS_CLI_reference.html#d0e14496)','[ecl-cli ps](http://docs.aws.amazon.com/AmazonECS/latest/developerguide/ECS_CLI_reference.html#cmd-ecs-cli-ps)'，分别来使用)来进行可编程的创建、集群和任务的更新和监控等。亚马逊ECS CLI现在还支持了[Docker Compose](https://docs.docker.com/compose/)（通过命令'[ecs-cli compose](http://docs.aws.amazon.com/AmazonECS/latest/developerguide/ECS_CLI_reference.html#cmd-ecs-cli-compose)'），Docker Compose是一款用于定义和运行多容器应用的非常流行的开源工具。此命令可让开发者用来创建和测试Docker Compose－－定义本地环境，然后将定义好的推送到生产环境中的ECS。

可以按照[亚马逊ECS开发者指南](http://docs.aws.amazon.com/AmazonECS/latest/developerguide/ECS_CLI_installation.html)的说明去下载ECS CLI。根据其Github上的项目问题反馈页面来看，还有许多主要功能是有比较严重的缺陷的。例如缺乏对[JSON 数组](https://github.com/aws/amazon-ecs-cli/issues/3)对支持、如果没有定义 '[HostPath](https://github.com/aws/amazon-ecs-cli/issues/11)'对话挂载卷就会出问题、以及对[私有Docker注册认证](https://github.com/aws/amazon-ecs-cli/issues/24)没有支持等。

AWS计算博客上有[ECS任务定义](http://docs.aws.amazon.com/AmazonECS/latest/developerguide/task_defintions.html)的文章，在EC2实例中对一个应用指定容器如何调度在一起，现在支持更多额外的Docker属性，包括[Docker标签](https://docs.docker.com/userguide/labels-custom-metadata/)、[工作目录](https://docs.docker.com/reference/builder/#workdir)、禁用网络、[特权执行](https://docs.docker.com/reference/run/)、只读根文件系统、DNS服务、DNS搜索域、ulimits、日志配置、额外的主机（添加到/etc/hosts的主机），以及针对[多层次安全](https://en.wikipedia.org/wiki/Multilevel_security)（MLS）系统如[SElinux](https://en.wikipedia.org/wiki/Security-Enhanced_Linux)的安全属性。

亚马逊[ECS服务调度器](http://docs.aws.amazon.com/AmazonECS/latest/developerguide/scheduling_tasks.html)可启用任务定义的调度，举例来说 ，执行一个长期运行的（微）服务应用，而且还启用了‘可用区域感知’。此特性确保启动新的任务到ECS集群时，可以在多个可用区域之间进行平衡，这可以改进应用级别的容错，例如，可减少由于单个可用域的故障运行在相同实例的任务同时失效的风险。

亚马逊还宣布了他们会在今年稍后发布[亚马逊EC2容器注册](https://aws.amazon.com/ecr/)（亚马逊ECR），亚马逊计算博客上谈到，一个容器的注册对于基于Docker的生态系统的任何生产部署都是非常重要的组件。因为存放容器镜像的地方，持续交付的构建流程用的到（甚至时本地的Docker工具），Docker集群／调度运行时也会检索它，如亚马逊ECS、[Docker Swarm](https://docs.docker.com/swarm/)、或者是[Kubernetes](http://kubernetes.io/)。

尽管目前运维人员可以将他们自己的Docker注册放在亚马逊ECS（或者是使用商业提供的，如[Docker企业Hub]（http://www.docker.com/enterprise/hub/）、[CoreOS的Quay.io](https://quay.io/)）上，亚马逊曾在其博客上[说明](https://aws.amazon.com/blogs/aws/category/ec2-container-service/)ECR服务将会持久的存储Docker镜像到S3上，并提供镜像的加密和中转，能够和[亚马逊认证和访问管理]（https://aws.amazon.com/iam/）(IAM)集成以简化授权和提供细粒度的访问。亚马逊也曾说到和多个专注持续交付的合作伙伴一起合作，包括Shippable、CloudBees、CodeShip、Wercker，他们将集成到亚马逊ECS和ECR中来，专注于自动构建和部署Docker镜像。

更多关于亚马逊ECS的更新信息可访问[AWS官方博客](https://aws.amazon.com/blogs/aws/ec2-container-service-update-container-registry-ecs-cli-az-aware-scheduling-and-more/)，而且在美国拉斯维加斯举办的刚刚结束的AWS re:Invent大会上也有很多相关亚马逊ECS的视频，请访问[AWS计算博客](https://aws.amazon.com/blogs/compute/amazon-ec2-container-service-at-aws-reinvent-wrap-up/)了解更多详情。


查看英文原文：[Amazon EC2 Container Service Updates Relseased,Focusing Automation,Configuration & Availability](http://www.infoq.com/news/2015/10/ecs-update)
