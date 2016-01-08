#使用Kubernetes来管理Docker的扩展 

## 摘要：

Kubernetes是一款开源的项目，管理Linux容器集群，并可将集群作为一个单一的系统来对待。其可跨多主机来管理和运行Docker容器、提供容器的定位、服务发现以及复制控制。

--------------------------------------------------

[Kubernetes](https://github.com/GoogleCloudPlatform/kubernetes)是一款开源的项目，管理Linux容器集群，并可将集群作为一个单一的系统来对待。其可跨多主机来管理和运行Docker容器、提供容器的定位、服务发现以及复制控制。它由Google发起，现在则得到如[微软、红帽、IBM和Docker等](http://www.infoq.com/articles/docker-future)众多厂商的支持。

Google使用容器技术有着[超过十年](http://www.infoq.com/news/2014/06/everything-google-containers)的历史，每周要启动超过2亿台容器。通过Kubernetes，Google分享了他们关于容器的专业经验，即创建大规模运行容器的开放平台。

一旦用户开始使用Docker容器，那么问题就来了，一、如何大规模并在多个容器主机上启动它们，且能够在主机间取得平衡。二、还需要高度抽象出API来定义如何逻辑上组织容器、定义容器池、负载均衡以及相似性。该项目就是为了解决这两个问题而生的。

Kubernetes仍然处于早期阶段，这也就意味着会有很多新的变化进入到项目，目前还仅有较简单的实例，仍需要新的功能加入，但是它平稳发展，得到很多大的公司的支持，前途无量。

## Kubernetes概念

Kubernetes的架构被定义为由一个master服务器和多个minons服务器组成。命令行工具连接到master服务器的API端点，其可以管理和编排所有的minons服务器，Docker容器接收来自master服务器的指令并运行容器。

 * Master：Kubernetes API 服务所在，多Master的配置仍在开发中。
 * Minons：每个安装由Kubelet服务的Docker主机，Kubelet服务用于接收来自Master的指令，且管理运行容器的主机。
 * [Pod](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/pods.md)：定义了一组绑在一起的容器，可以部署在同一Minons，例如一个数据库或者是web服务器。
 * [Replication controller](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/replication-controller.md)：定义了需要运行多少个Pod或者容器。跨多个minons来调度容器。
 * Service：定义了由容器所发布的可被发现的服务／端口，以及外部代理通信。服务会映射端口到外部可访问的端口，而所映射的端口是跨多个minons的Pod内运行的容器的端口。
 * kubecfg：命令行客户端，连接到master来管理Kubernetes。
 

![architect of kubernetes](http://cdn.infoq.com/statics_s2_20151006-0049u1/resource/articles/scaling-docker-with-kubernetes/en/resources/architecture-large.png)

Kubernetes由状态所定义，而不是进程。当你定义了一个pod时，Kubernetes会尝试确保它会一直运行。如果其中的某个容器挂掉了，Kubernetes会尝试再启动一个新的容器。如果一个复制控制器定义了3份复制，Kubernetes会尝试一直运行这3份，根据需要来启动和停止容器。

本文中所用的例子应用是Jenkins持续集成服务，Jenkins是典型的通过主从服务来建立分布式的工作任务的例子。Jenkins由[jenkins swarm插件](https://wiki.jenkins-ci.org/display/JENKINS/Swarm+Plugin)来配置，运行一个jenkins主服务和多个jenkins从服务，所有的Jenkins服务都以Docker容器的方式跨多个主机运行。swarm从服务在启动时连接到Jenkins主服务，然后就可以运行Jenkins任务了。[例子中使用的配置文件](https://github.com/carlossg/kubernetes-jenkins)在从Github上下载到，至于Docker的镜像，对于Jenkins主服务来说，从[casnchez/jenkins-swarm](https://hub.docker.com/u/csanchez/jenkins-swarm)获取，即加入了swarm插件的官方Jenkins镜像。对于jenkins从服务来说，从[csanchez/jenkins-swarm-slave](https://hub.docker.com/u/csanchez/jenkins-swarm-slave)获取，此仅是在JVM容器中运行了jenkins从服务而已。

##创建Kubernetes集群

Kubernetes提供了多个操作系统和云／虚拟化提供商下创建集群的脚本，有Vagrant（用于本地测试）、Google Compute Engine、Azure、Rackspace等。

本文所实践的例子就是运行在Vagrant之上的本地集群，使用Fedora作为操作系统，遵照的是官方[入门指南](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/vagrant.md)，测试的Kubernetes版本是0.5.4。取代了默认的3个minion（Docker主机），而是使用了2个minion，两台主机就足够可以展示Kubernetes的能力了，三台就有点浪费。

当你[下载了Kubernetes](https://github.com/GoogleCloudPlatform/kubernetes/releases)，然后将至解压后，示例即可在本地的目录下运行。初学者创建集群仅需要一个命令，即`./cluster/kube-up.sh`。

```
$ export KUBERNETES_PROVIDER=vagrant
$ export KUBERNETES_NUM_MINIONS=2
$ ./cluster/kube-up.sh

```

获取示例配置文件：

```
$ git clone https://github.com/carlossg/kubernetes-jenkins.git

```
集群创建的快慢取决于机器的性能和内部的带宽。但是其最终完成不能有任何的错误，而且它仅需要运行一次。

##命令行工具

和Kubernetes交互的命令行工具叫做kubecfg，此脚本位于`cluster/kubecfg.sh`。

为了检验我们刚才创建的两个minons已经启动并运行了，只需运行`kubecfg list minions`命令即可，它的结果会显示Vagrant的两台虚拟机。


```
$ ./cluster/kubecfg.sh list minions
Minion identifier
----------
10.245.2.2
10.245.2.3
```

##Pod

在Kubernetes的术语中，Jenkins主服务被定义为一个[pod](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/pods.md)。在一个pod中可以指定多个容器，这些容器均部署在同一Docker主机中，在一个pod中的容器的优势在于可以共享资源，例如存储[卷](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/volumes.md)，而且使用相同的网络命名空间和IP地址。默认的卷是空的目录，类型为emptyDir，它的生存时间就是pod的生命周期，而并非是指定的容器，所以如果一个容器失效了，但是其持久性的存储仍然在。另外一个卷的类型是hostDir，它是将主机的一个目录挂载到容器中。

在此Jenkins特别的示例中，我们所创建的pod是两个容器，分别是Jenkins主服务和MySQL，前者作为实例，后者作为数据库。然而我们只需要关心jenkins主服务容器即可。

为了创建一个Jenkins pod，我们运行定义了Jenkins容器pod的`kubecfg`，使用Docker镜像csanchez/jenkins-swarm，为了能够访问Jenkins的Web界面和从服务的API，我们将主机的端口8080和50000映射到容器，以及将/var/jenkins_home挂载为卷。读者可从[Github](https://github.com/carlossg/kubernetes-jenkins)下载到示例代码。

Jenkins Web 界面的pod（pod.json）的定义如下：

```
{
  "id": "jenkins",
  "kind": "Pod",
  "apiVersion": "v1beta1",
  "desiredState": {
    "manifest": {
      "version": "v1beta1",
      "id": "jenkins",
      "containers": [
        {
          "name": "jenkins",
          "image": "csanchez/jenkins-swarm:1.565.3.3",
          "ports": [
            {
              "containerPort": 8080,
              "hostPort": 8080
            },
            {
              "containerPort": 50000,
              "hostPort": 50000
            }
          ],
          "volumeMounts": [
            {
              "name": "jenkins-data",
              "mountPath": "/var/jenkins_home"
            }
          ]
        }
      ],
      "volumes": [
        {
          "name": "jenkins-data",
          "source": {
            "emptyDir": {}
          }
        }
      ]
    }
  },
  "labels": { "name": "jenkins"
  }
}

```
然后使用下面命令来创建：

```
$ ./cluster/kubecfg.sh -c kubernetes-jenkins/pod.json create pods

Name                Image(s)                           Host                Labels              Status
----------          ----------                         ----------          ----------          ----------
jenkins             csanchez/jenkins-swarm:1.565.3.3   <unassigned>        name=jenkins        Pending


```
等待一段时间，具体时间到长短，要视你的网络而定，因为它会从Docker Hub上下载Docker镜像到minion，我们可以查看它的状态，以及在那个minion中启动。

```
$ ./cluster/kubecfg.sh list pods
Name                Image(s)                           Host                    Labels              Status
----------          ----------                         ----------              ----------          ----------
jenkins             csanchez/jenkins-swarm:1.565.3.3   10.0.29.247/10.0.29.247   name=jenkins        Running


```
如果我们使用SSH登录到minion中，此minion即是pod被分配到的minion-1或minion-2，我们就可以看到Docker按照所定义的那样启动起来了。其中还包括了用于Kubernetes内部管理的容器（kubernetes/pause和google/cadvisor）。

```
$ vagrant ssh minion-2 -c "docker ps"

CONTAINER ID        IMAGE                              COMMAND                CREATED             STATUS              PORTS                                              NAMES
7f6825a80c8a        google/cadvisor:0.6.2              "/usr/bin/cadvisor"    3 minutes ago       Up 3 minutes                                                           k8s_cadvisor.b0dae998_cadvisormanifes12uqn2ohido76855gdecd9roadm7l0.default.file_cadvisormanifes12uqn2ohido76855gdecd9roadm7l0_28df406a
5c02249c0b3c        csanchez/jenkins-swarm:1.565.3.3   "/usr/local/bin/jenk   3 minutes ago       Up 3 minutes                                                           k8s_jenkins.f87be3b0_jenkins.default.etcd_901e8027-759b-11e4-bfd0-0800279696e1_bf8db75a
ce51fda15f55        kubernetes/pause:go                "/pause"               10 minutes ago      Up 10 minutes                                                          k8s_net.dbcb7509_0d38f5b2-759c-11e4-bfd0-0800279696e1.default.etcd_0d38fa52-759c-11e4-bfd0-0800279696e1_e4e3a40f
e6f00165d7d3        kubernetes/pause:go                "/pause"               13 minutes ago      Up 13 minutes       0.0.0.0:8080->8080/tcp, 0.0.0.0:50000->50000/tcp   k8s_net.9eb4a781_jenkins.default.etcd_901e8027-759b-11e4-bfd0-0800279696e1_7bd4d24e
7129fa5dccab        kubernetes/pause:go                "/pause"               13 minutes ago      Up 13 minutes       0.0.0.0:4194->8080/tcp                             k8s_net.a0f18f6e_cadvisormanifes12uqn2ohido76855gdecd9roadm7l0.default.file_cadvisormanifes12uqn2ohido76855gdecd9roadm7l0_659a7a52


```

还有，我们一旦拿到了容器的ID，就可以通过如`vagrant ssh minion-1 -c "docker logs cec3eab3f4d3"`这样查看容器的日志了。

我们也可以访问Jenkins的Web界面，至于要访问的URL是http://10.245.2.2:8080/还是http://10.0.29.247:8080/，要看用到了那个minion。

##服务发现

Kubernetes支持定义服务，一种为容器使用发现和代理请求到合适的pod的方法。下面示例使用了`service-http.json`文件来创建一个服务，其将id为jenkins指向了贴有标签为name=jenkins的pod。而标签是在如上面pod的定义中所声明的。且将端口8888重定向到容器的8080 。

```
{
  "id": "jenkins",
  "kind": "Service",
  "apiVersion": "v1beta1",
  "port": 8888,
  "containerPort": 8080,
  "selector": {
    "name": "jenkins"
  }
}

```
使用`kubecfg`来创建服务：

```
$ ./cluster/kubecfg.sh -c kubernetes-jenkins/service-http.json create services

Name                Labels              Selector            IP                  Port
----------          ----------          ----------          ----------          ----------
jenkins                                 name=jenkins        10.0.29.247         8888


```
每个服务都会被分配一个唯一的IP地址，且此IP地址会伴随服务的整个生命周期。如果我们有多个pod匹配服务的定义的话，服务就会在所有它们之上提供负载均衡。

服务的另外一个特性是可以为由Kubernetes来运行的容器设置一些环境变量，从而指定了固定的容器，提供了连接到服务容器的能力，这很类似于[Docker容器链接](https://docs.docker.com/userguide/dockerlinks/)，这就可以从任何一个Jenkins的从服务找到Jenkins主服务的办法。

```
JENKINS_PORT='tcp://10.0.29.247:8888'
JENKINS_PORT_8080_TCP='tcp://10.0.29.247:8888'
JENKINS_PORT_8080_TCP_ADDR='10.0.29.247'
JENKINS_PORT_8080_TCP_PORT='8888'
JENKINS_PORT_8080_TCP_PROTO='tcp'
JENKINS_SERVICE_PORT='8888'
SERVICE_HOST='10.0.29.247'

```
在此示例中，我们还需要打开端口50000，这是Jenkins swarm插件所需要的。我们创建另外一个`service-slave.json`文件，这样Kubernetes就可以重定向端口到Jenkins服务容器了。

```
{
  "id": "jenkins-slave",
  "kind": "Service",
  "apiVersion": "v1beta1",
  "port": 50000,
  "containerPort": 50000,
  "selector": {
    "name": "jenkins"
  }
}

```
再次使用`kubecfg`来创建：

```
$ ./cluster/kubecfg.sh -c kubernetes-jenkins/service-slave.json create services

Name                Labels              Selector            IP                  Port
----------          ----------          ----------          ----------          ----------
jenkins-slave                           name=jenkins        10.0.86.28          50000


```
列出所有可用的已经定义的服务，包括一些Kubernetes内部的服务：

```
$ ./cluster/kubecfg.sh list services

Name                Labels              Selector                                  IP                  Port
----------          ----------          ----------                                ----------          ----------
kubernetes-ro                           component=apiserver,provider=kubernetes   10.0.22.155         80
kubernetes                              component=apiserver,provider=kubernetes   10.0.72.49          443
jenkins                                 name=jenkins                              10.0.29.247         8888
jenkins-slave                           name=jenkins                              10.0.86.28          50000

```

##复制控制器

复制控制器允许在多个minion中运行多个pod。Jenkins的从服务以此方式来运行，可以确保会一直有一个从服务的池来运行Jenkins的任务。

创建`replication.json`，所定义的内容如下：

```

{
  "id": "jenkins-slave",
  "apiVersion": "v1beta1",
  "kind": "ReplicationController",
  "desiredState": {
    "replicas": 1,
    "replicaSelector": {
      "name": "jenkins-slave"
    },
    "podTemplate": {
      "desiredState": {
        "manifest": {
          "version": "v1beta1",
          "id": "jenkins-slave",
          "containers": [
            {
              "name": "jenkins-slave",
              "image": "csanchez/jenkins-swarm-slave:1.21",
              "command": [
                "sh", "-c", "/usr/local/bin/jenkins-slave.sh -master http://$JENKINS_SERVICE_HOST:$JENKINS_SERVICE_PORT -tunnel $JENKINS_SLAVE_SERVICE_HOST:$JENKINS_SLAVE_SERVICE_PORT -username jenkins -password jenkins -executors 1"
              ]
            }
          ]
        }
      },
      "labels": {
        "name": "jenkins-slave"
      }
    }
  },
  "labels": {
    "name": "jenkins-slave"
  }
}


```
`podTemplate`一节允许和pod的定义进行一样的配置。在此示例中，我们打算让Jenkins从服务自动的连接到Jenkins主服务，而不是利用Jenkins主服务的多播发现。要实现此想法，我们需要执行`jenkins-slave.sh`命令，指定参数`-master`，从而实现在Kubernetes中让从服务连接到主服务。注意，上述配置文件中，我们使用了Kubernetes所提供的为Jenkins服务定义的环境变量（JENKINS_SERVICE_HOST和JENKINS_SERVICE_PORT）。此方法中镜像的命令覆盖了容器的配置，为的是利用已经下载好的镜像。这也同样可以在pod的定义中去实现。

使用`kubecfg`来创建副本：

```


$ ./cluster/kubecfg.sh -c kubernetes-jenkins/replication.json create replicationControllers

Name                Image(s)                            Selector             Replicas
----------          ----------                          ----------           ----------
jenkins-slave       csanchez/jenkins-swarm-slave:1.21   name=jenkins-slave   1
```
现在执行pod列表，可以看到新的pod已经创建，其数量是由我们刚刚所定义的复制控制器所决定的。

```
$ ./cluster/kubecfg.sh list pods

Name                                   Image(s)                            Host                    Labels               Status
----------                             ----------                          ----------              ----------           ----------
jenkins                                csanchez/jenkins-swarm:1.565.3.3    10.245.2.3/10.245.2.3   name=jenkins         Running
07651754-4f88-11e4-b01e-0800279696e1   csanchez/jenkins-swarm-slave:1.21   10.245.2.2/10.245.2.2   name=jenkins-slave   Pending


```
第一次所运行jenkins-swarm-slave镜像是minion从Docker仓库下载下来的，但是稍后，就取决于你的互联网连接了。Jenkins从服务须自动连接到Jenkins主服务。登录到Jenkins从服务所在的服务器，`docker ps`会显示出所运行的容器，且Docker的日志对于调试容器启动的任何问题都是很有帮助的。

```

$ vagrant ssh minion-1 -c "docker ps"

CONTAINER ID        IMAGE                               COMMAND                CREATED              STATUS              PORTS                    NAMES
870665d50f68        csanchez/jenkins-swarm-slave:1.21   "/usr/local/bin/jenk   About a minute ago   Up About a minute                            k8s_jenkins-slave.74f1dda1_07651754-4f88-11e4-b01e-0800279696e1.default.etcd_11cac207-759f-11e4-bfd0-0800279696e1_9495d10e
cc44aa8743f0        kubernetes/pause:go                 "/pause"               About a minute ago   Up About a minute                            k8s_net.dbcb7509_07651754-4f88-11e4-b01e-0800279696e1.default.etcd_11cac207-759f-11e4-bfd0-0800279696e1_4bf086ee
edff0e535a84        google/cadvisor:0.6.2               "/usr/bin/cadvisor"    27 minutes ago       Up 27 minutes                                k8s_cadvisor.b0dae998_cadvisormanifes12uqn2ohido76855gdecd9roadm7l0.default.file_cadvisormanifes12uqn2ohido76855gdecd9roadm7l0_588941b0
b7e23a7b68d0        kubernetes/pause:go                 "/pause"               27 minutes ago       Up 27 minutes       0.0.0.0:4194->8080/tcp   k8s_net.a0f18f6e_cadvisormanifes12uqn2ohido76855gdecd9roadm7l0.default.file_cadvisormanifes12uqn2ohido76855gdecd9roadm7l0_57a2b4de

```
复制控制器可以自动的调整任何想要的副本数量：

```
$ ./cluster/kubecfg.sh resize jenkins-slave 2


```
再次列出pod的话，可以看到每个副本是运行在哪里的。

```
$ ./cluster/kubecfg.sh list pods
Name                                   Image(s)                            Host                    Labels               Status
----------                             ----------                          ----------              ----------           ----------
07651754-4f88-11e4-b01e-0800279696e1   csanchez/jenkins-swarm-slave:1.21   10.245.2.2/10.245.2.2   name=jenkins-slave   Running
a22e0d59-4f88-11e4-b01e-0800279696e1   csanchez/jenkins-swarm-slave:1.21   10.245.2.3/10.245.2.3   name=jenkins-slave   Pending
jenkins                                csanchez/jenkins-swarm:1.565.3.3    10.245.2.3/10.245.2.3   name=jenkins         Running


```

![image of jenkins](http://cdn.infoq.com/statics_s2_20151006-0049u1/resource/articles/scaling-docker-with-kubernetes/en/resources/220140917%20kubernetes-jenkins.png)
##调度

目前默认的调度是随机的，但是基于资源的调度很快就实现了。在写作本文的时候，基于内存和CPU利用率的调度还有一些没有修复的问题。还有整合[Apache Mesos的调度](https://github.com/mesosphere/kubernetes-mesos)也在紧锣密鼓的进行中。Apache Mesos是一款分布式系统的框架，能够为资源管理提供出API，且是基于整个数据中心或云的环境的调度。

##自愈
使用Kubernetes的一大好处就是其能够自动管理和修复容器。

如果运行Jenkins服务的容器宕机了，无所谓什么原因，举个例子的话，进程是会崩溃的。那么Kubernetes就会得到通知，并会在几秒钟之后创建一个新的容器。

```
$ vagrant ssh minion-2 -c 'docker kill `docker ps | grep csanchez/jenkins-swarm: | sed -e "s/ .*//"`'
51ba3687f4ee


```

```
$ ./cluster/kubecfg.sh list pods
Name                                   Image(s)                            Host                    Labels               Status
----------                             ----------                          ----------              ----------           ----------
jenkins                                csanchez/jenkins-swarm:1.565.3.3    10.245.2.3/10.245.2.3   name=jenkins         Failed
07651754-4f88-11e4-b01e-0800279696e1   csanchez/jenkins-swarm-slave:1.21   10.245.2.2/10.245.2.2   name=jenkins-slave   Running
a22e0d59-4f88-11e4-b01e-0800279696e1   csanchez/jenkins-swarm-slave:1.21   10.245.2.3/10.245.2.3   name=jenkins-slave   Running


```
稍后再执行pod列表，一般不会超过1分钟，会看到如下内容：

```
Name                                   Image(s)                            Host                    Labels               Status
----------                             ----------                          ----------              ----------           ----------
jenkins                                csanchez/jenkins-swarm:1.565.3.3    10.245.2.3/10.245.2.3   name=jenkins         Running
07651754-4f88-11e4-b01e-0800279696e1   csanchez/jenkins-swarm-slave:1.21   10.245.2.2/10.245.2.2   name=jenkins-slave   Running
a22e0d59-4f88-11e4-b01e-0800279696e1   csanchez/jenkins-swarm-slave:1.21   10.245.2.3/10.245.2.3   name=jenkins-slave   Running


```
将Jeknkis的数据目录以卷的形式运行，我们保证了再容器宕机之后仍然能够保留数据，所以不会丢失任何Jenkins的任务或者是已经创建好的数据。而且因为Kubernetes在每个minion都代理了服务，Jenkins从服务会自动连接到Jenkins主服务，而根本无须关心其运行在哪里！而且Jenkins从服务容器宕掉，系统也会自动创建新的容器，服务发现会将之自动加入到Jenkins服务池中。

如果发生了更加严重的情况，比如minion挂掉了，Kubernetes目前还没能提供将现有容器重新调度到其它仍在运行的minion中的能力，它仅仅会显示某个pod失效，如下所示：

```

$ vagrant halt minion-2
==> minion-2: Attempting graceful shutdown of VM...
$ ./cluster/kubecfg.sh list pods
Name                                   Image(s)                            Host                    Labels               Status
----------                             ----------                          ----------              ----------           ----------
jenkins                                csanchez/jenkins-swarm:1.565.3.3    10.245.2.3/10.245.2.3   name=jenkins         Failed
07651754-4f88-11e4-b01e-0800279696e1   csanchez/jenkins-swarm-slave:1.21   10.245.2.2/10.245.2.2   name=jenkins-slave   Running
a22e0d59-4f88-11e4-b01e-0800279696e1   csanchez/jenkins-swarm-slave:1.21   10.245.2.3/10.245.2.3   name=jenkins-slave   Failed

```

##清理	

kubecfg还提供了一些命令涌来停止和删除诸如复制控制器、pod、以及服务等。

要停止复制控制器，设置复制数为0，Jenkins从服务等容器会被终止：

```
$ ./cluster/kubecfg.sh stop jenkins-slave
```
删除它：

```
$ ./cluster/kubecfg.sh rm jenkins-slave

```
删除Jenkins服务Pod，Jenkins主服务的容器会被终止：

```
$ ./cluster/kubecfg.sh delete pods/jenkins
```
删除服务：

```
$ ./cluster/kubecfg.sh delete services/jenkins
$ ./cluster/kubecfg.sh delete services/jenkins-slave
```
##总结

Kubernetes还是一个尚处于早期的项目，但是极有希望来管理Docker的跨服务器部署以及简化执行长时间运行和分布式的Docker容器。通过抽象基础设施概念，定义状态而不是进程，它提供了集群的简单定义，包括脱离管理的自我修复能力。简而言之，Kubernetes让Docker的管理更加的轻松。

## 关于作者
![Image of author 1](http://cdn.infoq.com/statics_s2_20151006-0049u1/resource/articles/scaling-docker-with-kubernetes/en/resources/CarlosSanchez.jpg)Carlos Sanchez在自动化，软件开发质量，QA以及运维等方面有超过10年的经验，范围涉及从构建工具、持续集成到部署自动化，DevOps最佳实践，再到持续交付。他曾经为财富500强的公司实施过解决方案，在多家美国的创业公司工作过，最近的任职的公司叫做MaestroDev，这也是他一手创建的公司。Carlos曾经在世界各地的各种技术会议上作演讲，包括JavaOne， EclipseCON， ApacheCON， JavaZone，Fosdem 以及 PuppetConf。非常积极的参与开源，他是Apache软件基金会的成员，同时也是其它一些开源团体的成员，为很多个开源项目做个贡献，这里举几个例子，有Apache Maven，Fog 以及 Puppet。


查看英文原文：[Scaling Docker with Kubernetes](http://www.infoq.com/articles/scaling-docker-with-kubernetes)
