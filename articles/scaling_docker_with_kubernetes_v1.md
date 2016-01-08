#使用Kubernetes V1来管理Docker的扩展 

## 摘要：
在本文读者会看到Kubernetes V1的Jenkins实例，运行在Google容器引擎（和本地的Vagrant）之上。Kubernetes V1带来企业级的能力，诸如自我修复、服务发现、动态DNS、资源配额、集中的日志记录、网络隔离等等，简而言之，Kubernetes V1让Docker的管理更加容易。

--------------------------------------------------

[Kubernetes](https://github.com/GoogleCloudPlatform/kubernetes)是一款开源的项目，管理Linux容器集群，并可将集群作为一个单一的系统来对待。其可跨多主机来管理和运行Docker容器、提供容器的定位、服务发现以及复制控制。它由Google发起，现在则得到如[微软、红帽、IBM和Docker等](http://www.infoq.com/articles/docker-future)众多厂商的支持。

Google使用容器技术有着[超过十年](http://www.infoq.com/news/2014/06/everything-google-containers)的历史，每周要启动超过2亿台容器。通过Kubernetes，Google分享了他们关于容器的专业经验，即创建大规模运行容器的开放平台。

一旦用户开始使用Docker容器，那么问题就来了，一、如何大规模并在多个容器主机上启动它们，且能够在主机间取得平衡。二、还需要高度抽象出API来定义如何逻辑上组织容器、定义容器池、负载均衡以及相似性。该项目就是为了解决这两个问题而生的。

## Kubernetes概念

Kubernetes的架构被定义为由一个master服务器和多个minons服务器组成。命令行工具连接到master服务器的API端点，其可以管理和编排所有的minons服务器，Docker容器接收来自master服务器的指令并运行容器。

 * [命名空间](https://github.com/kubernetes/kubernetes/blob/release-1.0/docs/admin/namespaces.md)：基于它们自身的配额和网络的集群分区。
 * [节点](https://github.com/kubernetes/kubernetes/blob/release-1.0/docs/admin/node.md)：每个安装由Kubelet服务的Docker主机，Kubelet服务用于接收来自Master的指令，且管理运行容器的主机（原来叫做minions）。
 * [Pod](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/pods.md)：定义了一组绑在一起的容器，可以部署在同一节点，例如一个数据库或者是web服务器。
 * [Replication controller](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/replication-controller.md)：定义了需要运行多少个Pod或者容器。跨多个minons来调度容器。
 * [Service](https://github.com/kubernetes/kubernetes/blob/release-1.0/docs/user-guide/services.md)：定义了由容器所发布的可被发现的服务／端口，以及外部代理通信。服务会映射端口到外部可访问的端口，而所映射的端口是跨多个节点的Pod内运行的容器的端口。
 * kubectl：命令行客户端，连接到master来管理Kubernetes。
 

![architect of kubernetes](http://cdn.infoq.com/statics_s1_20151020-0055-2u1/resource/articles/scaling-docker-kubernetes-v1/en/resources/jenkins.jpg)

Kubernetes由状态所定义，而不是进程。当你定义了一个pod时，Kubernetes会尝试确保它会一直运行。如果其中的某个容器挂掉了，Kubernetes会尝试再启动一个新的容器。如果一个复制控制器定义了3份复制，Kubernetes会尝试一直运行这3份，根据需要来启动和停止容器。

本文中所用的例子应用是Jenkins持续集成服务，Jenkins是典型的通过主从服务来建立分布式的工作任务的例子。Jenkins由[jenkins swarm插件](https://wiki.jenkins-ci.org/display/JENKINS/Swarm+Plugin)来配置，运行一个jenkins主服务和多个jenkins从服务，所有的Jenkins服务都以Docker容器的方式跨多个主机运行。swarm从服务在启动时连接到Jenkins主服务，然后就可以运行Jenkins任务了。[例子中使用的配置文件](https://github.com/carlossg/kubernetes-jenkins)在从Github上下载到，至于Docker的镜像，对于Jenkins主服务来说，从[casnchez/jenkins-swarm](https://hub.docker.com/u/csanchez/jenkins-swarm)获取，即加入了swarm插件的官方Jenkins镜像。对于jenkins从服务来说，从[csanchez/jenkins-swarm-slave](https://hub.docker.com/u/csanchez/jenkins-swarm-slave)获取，此仅是在JVM容器中运行了jenkins从服务而已。

##新特性
版本1.0的发布带来稳定的API，以及管理大型集群的功能，包括DNS、负载均衡、扩展、应用程序级别的健康检测、服务账户、以及使用命名空间来隔离应用。API和命令行现在可以支持远程执行、跨多个主机的日志收集、以及资源监控。支持了更多的基于网络的卷，它们有Google计算引擎的持久磁盘、AWS伸缩块存储、NFS、[Flocker](https://clusterhq.com/flocker)、[GlusterFS](http://www.gluster.org/)。

版本1.1在1.0的基础上有增加了一些新的特性，包括正常终止pod、支持Docker1.8、自动横向扩展、以及在Kubernetes集群中使用Pod来调度短时间运行的任务（相对长时间运行的任务）的新的[任务](https://github.com/kubernetes/kubernetes/blob/release-1.1/docs/user-guide/jobs.md)对象。

##创建Kubernetes集群

Kubernetes提供了多个操作系统和云／虚拟化提供商下创建集群的脚本，有Vagrant（用于本地测试）、Google Compute Engine、Azure、Rackspace等。 [Google容器引擎(GKE)](https://cloud.google.com/container-engine)提供了Kubernetes集群即服务的支持。接下来我们会以本地的Vagrant虚拟机和Google容器引擎下来创建一个集群，至于选择哪个就看读者本身的喜好了，尽管GKE提供了更多的关于网络和持久存储方面的特性。这些例子也同样可以运行在任何其它的供应商平台下，当然需要少许的改动，我们也会在相应的章节有所描述。

### Vagrant
本文所实践的例子就是运行在Vagrant之上的本地集群，使用Fedora作为操作系统，遵照的是官方[入门指南](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/vagrant.md)，测试的Kubernetes版本是1.0.6。取代了默认的3台节点（Docker主机），而是使用了2个minion，两台主机就足够可以展示Kubernetes的能力了，三台就有点浪费。

当你[下载了Kubernetes](https://github.com/GoogleCloudPlatform/kubernetes/releases)，然后将至解压后，示例即可在本地的目录下运行。初学者创建集群仅需要一个命令，即`./cluster/kube-up.sh`。

```
$ export KUBERNETES_PROVIDER=vagrant
$ export KUBERNETES_NUM_MINIONS=2
$ ./cluster/kube-up.sh

```
集群创建的快慢取决于机器的性能和内部的带宽。但是其最终完成不能有任何的错误，而且它仅需要运行一次。

和Kubernetes交互的命令行工具叫做kubectl。Kubernetes的发布软件包中包含了一个便利的工具－```cluster/kubectl.sh```，但是命令行可以[独立安装](http://kubernetes.io/v1.0/docs/getting-started-guides/aws/kubectl.html)，而且也可以使用由kubeup.sh所创建的配置文件```~/.kube/config```。

确保kubectl在环境变量PATH中，因为在接下来的章节中将用到。要检查集群是启动并运行的，使用```kubectl get nodes```。

```
$ kubectl get nodes

NAME         LABELS                              STATUS
10.245.1.3   kubernetes.io/hostname=10.245.1.3   Ready
10.245.1.4   kubernetes.io/hostname=10.245.1.4   Ready```

###google 容器引擎 

按照[Google云平台站点上的步骤](https://cloud.google.com/container-engine/docs/before-you-begin)注册[Google容器引擎](https://cloud.google.com/container-engine/docs/)，启用容器引擎API，[安装gcloud工具](https://cloud.google.com/sdk/#Quick_Start)，然后使用```gcloud init```配置Google云平台。

一旦你成功登陆后，首先要更新kubectl工具，设置一些默认值，然后[创建Kubernetes集群](https://cloud.google.com/container-engine/docs/clusters/operations)。确保使用你的正确的Google云项目ID。

```
$ gcloud components update kubectl
$ gcloud config set project prefab-backbone-109611
$ gcloud config set compute/zone us-central1-f

$ gcloud container clusters create kubernetes-jenkins
Creating cluster kubernetes-jenkins...done.
Created [https://container.googleapis.com/v1/projects/prefab-backbone-109611/zones/us-central1-f/clusters/kubernetes-jenkins].
kubeconfig entry generated for kubernetes-jenkins.
NAME                ZONE           MASTER_VERSION  MASTER_IP        MACHINE_TYPE   STATUS
kubernetes-jenkins  us-central1-f  1.0.6           107.178.220.228  n1-standard-1  RUNNING
```

设置刚刚创建的集群的默认值，并为```kubectl```获取证书。

```

$ gcloud config set container/cluster kubernetes-jenkins
$ gcloud container clusters get-credentials kubernetes-jenkins

```

运行```kubectl```获取节点信息，正确的输出应是集群中有三台节点。

```
$ kubectl get nodes
NAME                                        LABELS                                                             STATUS
gke-kubernetes-jenkins-e46fdaa5-node-5gvr   kubernetes.io/hostname=gke-kubernetes-jenkins-e46fdaa5-node-5gvr   Ready
gke-kubernetes-jenkins-e46fdaa5-node-chiv   kubernetes.io/hostname=gke-kubernetes-jenkins-e46fdaa5-node-chiv   Ready
gke-kubernetes-jenkins-e46fdaa5-node-mb7s   kubernetes.io/hostname=gke-kubernetes-jenkins-e46fdaa5-node-mb7s   Ready
```

###集群信息
在集群启动后，我们就可以访问API端点或者是```kube-ui```的界面。

```
$ kubectl cluster-info
Kubernetes master is running at https://107.178.220.228
KubeDNS is running at https://107.178.220.228/api/v1/proxy/namespaces/kube-system/services/kube-dns
KubeUI is running at https://107.178.220.228/api/v1/proxy/namespaces/kube-system/services/kube-ui
Heapster is running at https://107.178.220.228/api/v1/proxy/namespaces/kube-system/services/monitoring-heapster
```
###代码实例
 

从[Github](https://github.com/carlossg/kubernetes-jenkins)获取示例配置文件：

```
$ git clone --branch infoq-kubernetes-1.0 https://github.com/carlossg/kubernetes-jenkins.git

```

##命名空间

[命名空间](https://github.com/kubernetes/kubernetes/blob/release-1.0/docs/user-guide/namespaces.md)可以跨多个用户和应用来隔离资源。

```
$ kubectl get namespaces
NAME LABELS STATUS
default <none> Active
kube-system <none> Active
```
命名空间可以关联到[资源配额](http://kubernetes.io/v1.0/docs/admin/resource-quota.html)，用来限制所使用的cpu、内存、以及一些各种类型（Pod、服务、复制控制器等）的资源。在下面的例子中，使用了默认的命名空间，但是可以自行创建命名空间来隔离资源，也有一些运行的服务通过```kube-system```命名空间提供端点给Kubernetes系统资源。

```
$ kubectl get endpoints --all-namespaces
NAMESPACE     NAME                  ENDPOINTS
default       jenkins               <none>
default       kubernetes            107.178.220.228:443
kube-system   kube-dns              10.172.2.3:53,10.172.2.3:53
kube-system   kube-ui               10.172.0.5:8080
kube-system   monitoring-heapster   10.172.0.6:8082
```


##Pod

在一个pod中可以指定多个容器，这些容器均部署在同一Docker主机中，在一个pod中的容器的优势在于可以共享资源，例如存储[卷](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/volumes.md)，而且使用相同的网络命名空间和IP地址。

在此Jenkins的实例中，我们有一个pod来运行Jenkins主服务，但是这是一个试验性质的，[pod在调度失效、节点失效、缺少资源、或者是节点维护无法存活](http://kubernetes.io/v1.0/docs/user-guide/pods.html#durability-of-pods-or-lack-thereof)。假如发生了作为pod运行Jenkins主服务的节点宕掉了，容器永远不会去重新启动它。基于此原因，我们将会在下面的例子中将Jenkins主服务以复制控制器的方式运行，基于一个实例。

##复制控制器

复制控制器允许跨多个节点运行多个pod，正如上面所提到的，Jenkins主服务会以一个复制控制器来运行到一个存活的节点上。当Jenkins Slaves使用复制控制器来确保一直会有slave的池来运行Jenkins任务。

###持久卷
Kubernetes支持多种后端的存储卷

* emptyDir
* hostPath
* gcePersistentDisk
* awsElasticBlockStore
* nfs
* iscsi
* glusterfs
* rbd
* gitRepo
* secret
* persistentVolumeClaim

卷在默认情况下均是空的目录，类型为```emptydir```，其生命周期是以pod的生命周期为准的，所以即使是容器宕掉了，持久存储仍在。其它的卷类型是```hostpath```，此是一种在容器内部直接挂在其所在主机服务器上的存储的一种方式。

```secret```的卷是用于哪些较敏感的信息，诸如用于pod的密码。密文可以保存在Kubernetes API中，pod使用的时候将其挂载为文件，而且会在内存中以tmpfs的形式作备份。

[持久卷](https://github.com/kubernetes/kubernetes/blob/release-1.0/docs/user-guide/persistent-volumes.md)是实现了用户所“要求”的持久化的存储（诸如```gcePersistent```或```iscsi```卷）而且还无须知道特定云环境的细节，在pod中使用```persistentVolumeClaim```就可以挂载。

在一个典型的Kubernetes安装中，后端的卷是可用于网络的，所以数据是可以挂载到任何的节点上的，从而pod可以调度它们。

在Vagrant的试验环境中，我们使用了一个简单的```hostDir```，这样做的弊端就是pod从一个节点移到另外一个节点时，数据不会跟着做迁移。

当使用Google容器引擎时，我们需要创建一个GCE的磁盘，这会用于主的Jenkins pod，存放Jenkins的数据。

```
gcloud compute disks create --size 20GB jenkins-data-disk
```
##Jenkins主复制控制器

为了创建一个Jenkins主pod，我们运行kubectl及其Jenkins容器复制控制器的定义，使用的Docker镜像是```csanchez/jenkins-swarm```，端口是8080和50000，映射到容器，这样就可以访问Jenkins的Web用户界面和从服务的API了，以及挂载卷到路径```/var/jenkins_home```。

```livenessProbe```的配置属性在自我修复一节有所涉及，当然你也可以在[GitHub上的例子](https://github.com/carlossg/kubernetes-jenkins/tree/infoq-kubernetes-1.0)中找到。

Vagrant环境的定义（jenkins-master-vagrant.yml）如下所示：

```
 apiVersion: "v1"
  kind: "ReplicationController"
  metadata: 
    name: "jenkins"
    labels: 
      name: "jenkins"
  spec: 
    replicas: 1
    template: 
      metadata: 
        name: "jenkins"
        labels: 
          name: "jenkins"
      spec: 
        containers: 
          - 
            name: "jenkins"
            image: "csanchez/jenkins-swarm:1.625.1-for-volumes"
            ports: 
              - 
                containerPort: 8080
              - 
                containerPort: 50000
            volumeMounts: 
              - 
                name: "jenkins-data"
                mountPath: "/var/jenkins_home"
            livenessProbe:
              httpGet:
                path: /
                port: 8080
              initialDelaySeconds: 60
              timeoutSeconds: 5
        volumes: 
          - 
            name: "jenkins-data"
            hostPath:
              path: "/home/docker/jenkins"

```
对于Google容器引擎中的定义，只需将上述中关于卷的定义```jenkins-data```替换我我们刚才所创建的GCE磁盘即可：

```
volumes: 
      - 
        name: "jenkins-data"
        gcePersistentDisk:
          pdName: jenkins-data-disk
          fsType: ext4
```
创建复制控制器是使用一样的命令：

```
$ kubectl create -f jenkins-master-gke.yml

```


创建完成后，Jenkins复制控制器和Pod会显示在相应的列表中：

```
$ kubectl get replicationcontrollers
CONTROLLER   CONTAINER(S)   IMAGE(S)                                     SELECTOR       REPLICAS
jenkins      jenkins        csanchez/jenkins-swarm:1.625.1-for-volumes   name=jenkins   1

$ kubectl get pods
NAME            READY     STATUS    RESTARTS   AGE
jenkins-gs7h9   0/1       Pending   0          5s
```
可使用```kubectl describe```来获得更多的细节，诸如查看调度到了哪个节点，或者是部署期间出现的错误：

```
$ kubectl describe pods/jenkins-gs7h9
Name:       jenkins-gs7h9
Namespace:      default
Image(s):     csanchez/jenkins-swarm:1.625.1-for-volumes
Node:       gke-kubernetes-jenkins-e46fdaa5-node-chiv/10.240.0.3
Labels:       name=jenkins
Status:       Running
Reason:
Message:
IP:       10.172.1.32
Replication Controllers:  jenkins (1/1 replicas created)
Containers:
  jenkins:
    Image:  csanchez/jenkins-swarm:1.625.1-for-volumes
    Limits:
      cpu:    100m
    State:    Running
      Started:    Sun, 18 Oct 2015 18:41:52 +0200
    Ready:    True
    Restart Count:  0
Conditions:
  Type    Status
  Ready   True
Events:
  FirstSeen             LastSeen            Count   From                            SubobjectPath               Reason      Message
  Tue, 13 Oct 2015 20:36:50 +0200   Tue, 13 Oct 2015 20:36:50 +0200 1   {scheduler }                                            scheduled   Successfully assigned jenkins to gke-kubernetes-jenkins-e46fdaa5-node-5gvr
  Tue, 13 Oct 2015 20:36:59 +0200   Tue, 13 Oct 2015 20:36:59 +0200 1   {kubelet gke-kubernetes-jenkins-e46fdaa5-node-5gvr} implicitly required container POD   pulled      Pod container image "gcr.io/google_containers/pause:0.8.0" already present on machine
  [...]
```
一段时间后，它会下载Docker镜像到节点，我们可以查看它的状态为```Running```：

```
$ kubectl get pods
NAME                  READY     STATUS    RESTARTS   AGE
jenkins-gs7h9         1/1       Running   0          15s
```
Jenkins容器日志可从Kubernetes API来访问：

```

$ kubectl logs jenkins-gs7h9
Running from: /usr/share/jenkins/jenkins.war
webroot: EnvVars.masterEnvVars.get("JENKINS_HOME")
...
INFO: Jenkins is fully up and running

```

##服务
Kubernetes可以定义服务，一种让容器可以彼此发现的方法，代理请求到相应的节点以及做到负载均衡。

每个服务都定义了一些类型字段，这些字段是告诉如何来访问这些服务的。

* ClusterIP:仅用于集群内部的IP，默认；
* NodePort：用于集群IP，但是也会抛出集群中每个节点的服务端口（每个节点的端口都一样）；
* LoadBlancer： 一些云服务提供商会提供对外部负载均衡起的支持（目前有GKE和AWS），使用ClusterIP和NodePort，但是可以要求云服务提供商使用何种负载均衡器来转发服务。

默认情况下，服务只有```ClusterIP```类型，这就意味着只能从集群内部访问到服务。为了能够让外部也可以访问到服务，或是```NodePort```，或是```LodaBlancer```，需要打开其中一个。

每个服务都会被分配一个唯一的IP地址，且此IP的生命周期伴随着服务。如果我们有多个Pod匹配到服务的话，则定义服务的负载均衡到流量到这些Pod。

接下来，我们会创建一个id为jenkins的服务，指配的Pod为标签是```name=jenkins```，正如在jenkins-master复制控制器定义中声明的，以及转发链接到端口8080、Jenkins Web UI、端口50000，均是Jenkins Swarm插件所需要的。

###Vagrant

在Vagrant中运行，我们可以使用```kubectl```来创建一个```NodePort```类型的服务。

```
---
  apiVersion: "v1"
  kind: "Service"
  metadata: 
    name: "jenkins"
  spec: 
    type: "NodePort"
    selector: 
      name: "jenkins"
    ports: 
      - 
        name: "http"
        port: 8080
        protocol: "TCP"
      - 
        name: "slave"
        port: 50000
        protocol: "TCP"

$ kubectl create -f service-vagrant.yml
$ kubectl get services/jenkins
NAME         LABELS                                    SELECTOR       IP(S)          PORT(S)
jenkins      <none>                                    name=jenkins   10.247.0.117   8080/TCP
                                                                                     50000/TCP


```
服务的描述信息会展示节点的那个端口映射到了容器内的8080。

```
$ kubectl describe services/jenkins
Name: jenkins
Namespace: default
Labels: <none>
Selector: name=jenkins
Type: NodePort
IP: 10.247.0.117
Port: http 8080/TCP
NodePort: http 32440/TCP
Endpoints: 10.246.2.2:8080
Port: slave 50000/TCP
NodePort: slave 31241/TCP
Endpoints: 10.246.2.2:50000
Session Affinity: None
No events.

```
我们可以使用我们的Vagrant的任何节点来访问Jenkins的Web UI，在此例中服务的定义```NodePort```为端口32440，所以10.245.1.3:32440或10.245.1.4:32440会转发以连接到正确的容器。

###Goodle容器引擎

在GKE中运行的话，我们可以使用公网IP来创建类生产环境的负载均衡器。

```
---
  apiVersion: "v1"
  kind: "Service"
  metadata: 
    name: "jenkins"
  spec: 
    type: "LoadBalancer"
    selector: 
      name: "jenkins"
    ports: 
      - 
        name: "http"
        port: 80
        targetPort: 8080
        protocol: "TCP"
      - 
        name: "slave"
        port: 50000
        protocol: "TCP"


$ kubectl create -f service-gke.yml
$ kubectl get services/jenkins
NAME      LABELS    SELECTOR       IP(S)            PORT(S)
jenkins   <none>    name=jenkins   10.175.245.100   80/TCP
                                                    50000/TCP```
服务的描述信息会展示给我们负载均衡器的IP（在创建的时候可能会稍花费一点时间），此例中的IP是：104.197.19.100
```
$ kubectl describe services/jenkins
Name:           jenkins
Namespace:      default
Labels:         <none>
Selector:       name=jenkins
Type:           LoadBalancer
IP:         10.175.245.100
LoadBalancer Ingress:   104.197.19.100
Port:           http    80/TCP
NodePort:       http    30080/TCP
Endpoints:      10.172.1.5:8080
Port:           slave   50000/TCP
NodePort:       slave   32081/TCP
Endpoints:      10.172.1.5:50000
Session Affinity:   None
No events.```
我们也可以使用Google 云API来获得关于负载均衡的信息。（在GCE的术语中叫做```forwarding-rule```）
```
$ gcloud compute forwarding-rules list
NAME                             REGION      IP_ADDRESS     IP_PROTOCOL TARGET
afe40deb373e111e5a00442010af0013 us-central1 104.197.19.100 TCP         us-central1/targetPools/afe40deb373e111e5a00442010af0013```
这是如果我们在浏览器中键入IP和端口的话，就可以看到Jenkins web界面在运行了。
###DNS和服务发现
服务的另外一个特性就是可为通过kubernetes运行的一连串容器设置很多环境变量，从而提供连接到服务容器的能力，类似于[Docker容器linked](https://docs.docker.com/userguide/dockerlinks/)的做法。这样可以用于从任何的Jenkins从服务发现主的Jenkins服务。

```
JENKINS_SERVICE_HOST=10.175.245.100
JENKINS_PORT=tcp://10.175.245.100:80
JENKINS_PORT_80_TCP_ADDR=10.175.245.100
JENKINS_SERVICE_PORT=80
JENKINS_SERVICE_PORT_SLAVE=50000
JENKINS_PORT_50000_TCP_PORT=50000
JENKINS_PORT_50000_TCP_ADDR=10.175.245.100
JENKINS_SERVICE_PORT_HTTP=80

```
Kubernetes还支持可选的额外组件[SkyDNS](https://github.com/skynetservices/skydns)，SkyDNS是构建在etcd之上的公告和服务发现的一个分布式服务，可以为[服务创建A记录和SRV纪录](https://github.com/kubernetes/kubernetes/blob/release-1.0/cluster/addons/dns/README.md)。A记录的形式是```my-svc.my-namespace.svc.cluster.local```，SRV是``` records _my-port-name._my-port-protocol.my-svc.my-namespace.svc.cluster.local```。容器均被配置为使用SkyDNS来解析服务名称为服务的IP，```/etc/resolv/conf```被配置为搜索多个后缀，从而让名称解析更加的容易：

```
nameserver 10.175.240.10
nameserver 169.254.169.254
nameserver 10.240.0.1
search default.svc.cluster.local svc.cluster.local cluster.local c.prefab-backbone-109611.internal. 771200841705.google.internal. google.internal.
options ndots:5

```
举个例子，对于我们刚刚创建的jenkins服务来说，下面的名称会被解析：

* ```jenkins, jenkins.default.svc.cluster.local, A record pointing to 10.175.245.100``
* ```_http._tcp.jenkins, _http._tcp.jenkins.default.svc.cluster.local, SRV with value 10 100 80 jenkins.default.svc.cluster.local```
* ```_slave._tcp.jenkins, _slave._tcp.jenkins.default.svc.cluster.local, SRV with value 10 100 50000 jenkins.default.svc.cluster.local```
##Jenkins从服务复制控制器

Jenkins从服务可以以复制控制器来运行从而确保一直会有从服务来运行Jenkins的任务。注意，此步骤可以加深对Kubernetes是如何工作的有所帮助，在这个特殊的Jenkins实例中，使用了[Jenkinks Kubernnetes插件](https://github.com/jenkinsci/kubernetes-plugin)是一个更好的方案，此插件可以自动的根据队列中任务的数量来动态的创建从服务，且可隔离任务的执行。

在```jenkins-slaves.yml```中所定义的：
```
```
---
  apiVersion: "v1"
  kind: "ReplicationController"
  metadata: 
    name: "jenkins-slave"
    labels: 
      name: "jenkins-slave"
  spec: 
    replicas: 1
    template: 
      metadata: 
        name: "jenkins-slave"
        labels: 
          name: "jenkins-slave"
      spec: 
        containers: 
          - 
            name: "jenkins-slave"
            image: "csanchez/jenkins-swarm-slave:2.0-net-tools"
            command: 
              - "/usr/local/bin/jenkins-slave.sh"
              - "-master"
              - "http://jenkins:$(JENKINS_SERVICE_PORT_HTTP)"
              - "-tunnel"
              - "jenkins:$(JENKINS_SERVICE_PORT_SLAVE)"
              - "-username"
              - "jenkins"
              - "-password"
              - "jenkins"
              - "-executors"
              - "1"
            livenessProbe:
              exec:
                command:
                - sh
                - -c
                - "netstat -tan | grep ESTABLISHED"
              initialDelaySeconds: 60
              timeoutSeconds: 1

```

在此例中，我们打算让Jenkis从服务自动的连接到Jenkins主服务，替代了Jenkins所依赖的多播发现。为此我们需要指向swarm插件到在Kubernetes中运行的主机，同时指定http端口（使用```-master```）和从服务端口（使用```-tunnel```）。

我们使用了来自Jenkins服务的定义的一系列值的组合，由SkyDNS所提供的Jenkins主机名，以及Kubernetes注入的环境变量```JENKINS_SERVICE_PORT_HTTP```和```JENKINS_SERVICE_PORT_SLAVE```，在服务名称之后命名，在服务中定义了每个端口（http和从服务）。我们还使用了环境变量```JENKINS_SERVICE_HOST```替代了```jenkins```主机名。被覆盖的镜像命令以此方式来配置容器，重复利用现有的镜像对于服务发现有好处。它也可以在pod的定义下完成。关于属性```livenessProbe```所覆盖的内容在下面的自我修复章节中会提及。

使用```kubectl```来创建复制：

```

$ kubectl create -f jenkins-slaves.yml

```

Pod的列表会展示出新创建的，具体启动的数量要看在复制控制器中所定义的数量，我们的例子是一个：


```
$ kubectl get pods
NAME                  READY     STATUS    RESTARTS   AGE
jenkins-gs7h9         1/1       Running   0          2m
jenkins-slave-svlwi   0/1       Running   0          4s

```
第一次运行```jenkins-swarm-slave```镜像到节点会从Docker的仓库上下载它，然后稍等一会，从服务就会自动连接到Jenkins服务。```kubectl logs```可以用于调试任何的启动问题。

复制控制器可以自动的扩展到想要的数量：

```
$ kubectl scale replicationcontrollers --replicas=2 jenkins-slave
```
再次列出pod就可以看到新增加的复制了：

```
$ kubectl get pods
NAME                  READY     STATUS    RESTARTS   AGE
jenkins-gs7h9         1/1       Running   0          4m
jenkins-slave-svlwi   1/1       Running   0          2m
jenkins-slave-z3qp8   0/1       Running   0          4s

```![jenkins job](http://cdn.infoq.com/statics_s1_20151020-0055-2u1/resource/articles/scaling-docker-kubernetes-v1/en/resources/jenkins-2.jpg)
##回滚更新

Kubernetes还支持回滚更新的概念，在某一刻只有一个pod可更新。基于新的```jenkins-slaves-v2.yml```配置文件定义了新的复制控制器配置，运行下面的命令，此命令是让Kubernetes每10秒更新一次pod。

```
$ kubectl rolling-update jenkins-slave --update-period=10s -f jenkins-slaves-v2.yml
Creating jenkins-slave-v2
At beginning of loop: jenkins-slave replicas: 1, jenkins-slave-v2 replicas: 1
Updating jenkins-slave replicas: 1, jenkins-slave-v2 replicas: 1
At end of loop: jenkins-slave replicas: 1, jenkins-slave-v2 replicas: 1
At beginning of loop: jenkins-slave replicas: 0, jenkins-slave-v2 replicas: 2
Updating jenkins-slave replicas: 0, jenkins-slave-v2 replicas: 2
At end of loop: jenkins-slave replicas: 0, jenkins-slave-v2 replicas: 2
Update succeeded. Deleting jenkins-slave
jenkins-slave-v2

$ kubectl get replicationcontrollers
CONTROLLER         CONTAINER(S)    IMAGE(S)                                     SELECTOR                REPLICAS
jenkins            jenkins         csanchez/jenkins-swarm:1.625.1-for-volumes   name=jenkins            1
jenkins-slave-v2   jenkins-slave   csanchez/jenkins-swarm-slave:2.0             name=jenkins-slave-v2   2

$ kubectl get pods
NAME                     READY     STATUS    RESTARTS   AGE
jenkins-gs7h9            1/1       Running   0          36m
jenkins-slave-v2-7jiyn   1/1       Running   0          52s
jenkins-slave-v2-9gip7   1/1       Running   0          28s

```
在此例中，真正并没有发生什么，除了复制控制器的名称，但是其它的任何参数都是可以更改的（docker镜像、环境等等）。

```

---
  apiVersion: "v1"
  kind: "ReplicationController"
  metadata: 
    name: "jenkins-slave-v2"
    labels: 
      name: "jenkins-slave"
  spec: 
    replicas: 2
    template: 
      metadata: 
        name: "jenkins-slave"
        labels: 
          name: "jenkins-slave-v2"
      spec: 
        containers: 
          - 
            name: "jenkins-slave"
            image: "csanchez/jenkins-swarm-slave:2.0-net-tools"
            command: 
              - "/usr/local/bin/jenkins-slave.sh"
              - "-master"
              - "http://$(JENKINS_SERVICE_HOST):$(JENKINS_SERVICE_PORT_HTTP)"
              - "-tunnel"
              - "$(JENKINS_SERVICE_HOST):$(JENKINS_SERVICE_PORT_SLAVE)"
              - "-username"
              - "jenkins"
              - "-password"
              - "jenkins"
              - "-executors"
              - "1"
            livenessProbe:
              exec:
                command:
                - sh
                - -c
                - "netstat -tan | grep ESTABLISHED"
              initialDelaySeconds: 60
              timeoutSeconds: 1

```
##自我修复
使用Kubernetes的一个好处就是自动管理和恢复容器。如果说运行Jenkins服务的容器宕掉了，无论任何的原因，对于实例来讲就是一个运行的进程崩溃了，Kubernetes会接到通知，然后在几秒钟之后就会再重新创建一个容器。正如我们再前面所提到的，使用复制控制器可以确保即使是节点宕掉了，所定义的复制数量依然会照旧运行。Kubernetes会采取必要的手段来确保在集群中新启动的pod是在不同的节点上的。

应用程序指定的健康检查可以使用[livenessProbe](http://kubernetes.io/v1.0/docs/user-guide/liveness/)来创建，允许作HTTP检查以及在pod中的每一个容器中执行命令。如果失败的话，容器就会被重启。

举例说明，要监控Jenkins是能够服务于HTTP请求的，将下列代码添加到Jenkins主容器的定义中：

```
   livenessProbe:
      httpGet:
        path: /
        port: 8080
      initialDelaySeconds: 60
      timeoutSeconds: 5

```
我们也可以监控我们的从服务是真的连接到了主服务上了。之所以有必要是因为如果Jenkins主服务重启到话，会丢失原来所连接到从服务的，而从服务会持续的尝试连接到原来的主服务，但是会失败，那么我们就需要检查从服务连接到主服务的情况。

```
   livenessProbe:
      exec:
        command:
        - sh
        - -c
        - "netstat -tan | grep ESTABLISHED"
      initialDelaySeconds: 60
      timeoutSeconds: 1

```
###Vagrant

我们将Jenkins主服务的pod终止，Kubernetes会在创建一个。

```
$ kubectl get pods
NAME                  READY     STATUS    RESTARTS   AGE
jenkins-7yuij         1/1       Running   0          8m
jenkins-slave-7dtw1   0/1       Running   0          6s
jenkins-slave-o3kt2   0/1       Running   0          6s

$ kubectl delete pods/jenkins-7yuij
pods/jenkins-7yuij

$ kubectl get pods
NAME                  READY     STATUS    RESTARTS   AGE
jenkins-jqz7z         1/1       Running   0          32s
jenkins-slave-7dtw1   1/1       Running   0          2m
jenkins-slave-o3kt2   1/1       Running   1          2m

```
Jenkins Web 用户界面仍然可以由原来的一些地址访问的到。Kubernetes服务会掌管转发连接到新的pod。运行Jenkins数据目录在卷中，我们保证了即使是容器宕掉仍然能够保持数据，所以我们没有丢失Jenkins任何的任务或已经创建的数据。而且因为Kubernetes代理了每个节点的服务，从服务会自动的重新连接到主服务，还毋需关心它运行在哪里！而且即使是如果从服务的容器宕掉的情况亦发生了，系统会自动创建一个新的容器，而且归功于服务发现的能力，可让其自动的加入的从服务池。###GKE
一旦发生了节点宕掉这种事情，Kubernetes会自动的重新调度pod到不同的地点。我们使用的是手动的将运行Jenkins主服务的节点关闭。

```

$ kubectl describe pods/jenkins-gs7h9 | grep Node
Node:       gke-kubernetes-jenkins-e46fdaa5-node-chiv/10.240.0.3
$ gcloud compute instances list
gcloud compute instances listNAME                                      ZONE          MACHINE_TYPE  PREEMPTIBLE INTERNAL_IP EXTERNAL_IP    STATUS
gke-kubernetes-jenkins-e46fdaa5-node-5gvr us-central1-f n1-standard-1             10.240.0.4  104.154.35.119 RUNNING
gke-kubernetes-jenkins-e46fdaa5-node-chiv us-central1-f n1-standard-1             10.240.0.3  104.154.82.184 RUNNING
gke-kubernetes-jenkins-e46fdaa5-node-mb7s us-central1-f n1-standard-1             10.240.0.2  146.148.81.44  RUNNING

$ gcloud compute instances delete gke-kubernetes-jenkins-e46fdaa5-node-chiv
The following instances will be deleted. Attached disks configured to
be auto-deleted will be deleted unless they are attached to any other
instances. Deleting a disk is irreversible and any data on the disk
will be lost.
 - [gke-kubernetes-jenkins-e46fdaa5-node-chiv] in [us-central1-f]

Do you want to continue (Y/n)? Y
Deleted [https://www.googleapis.com/compute/v1/projects/prefab-backbone-109611/zones/us-central1-f/instances/gke-kubernetes-jenkins-e46fdaa5-node-chiv].

$ gcloud compute instances list
NAME                                      ZONE          MACHINE_TYPE  PREEMPTIBLE INTERNAL_IP EXTERNAL_IP    STATUS
gke-kubernetes-jenkins-e46fdaa5-node-5gvr us-central1-f n1-standard-1             10.240.0.4  104.154.35.119 RUNNING
gke-kubernetes-jenkins-e46fdaa5-node-mb7s us-central1-f n1-standard-1             10.240.0.2  146.148.81.44  RUNNING

```
过一会，Kubernetes知道了运行pod的那个节点宕掉了，它就会在另外一台节点创建一个新的叫做```jenkins-44r3y```的pod。

```
$ kubectl get pods
NAME                     READY     STATUS    RESTARTS   AGE
jenkins-44r3y            1/1       Running   0          21s
jenkins-slave-v2-2z71c   1/1       Running   0          21s
jenkins-slave-v2-7jiyn   1/1       Running   0          5m
$ kubectl describe pods/jenkins-44r3y | grep Node
Node:       gke-kubernetes-jenkins-e46fdaa5-node-5gvr/10.240.0.4
```
接着打开浏览器，使用原来的IP来访问，看到的仍然是一样的Jenkins主服务的用户界面，因为它会自动的转发到运行Jenkins主服务的节点。你所创建的任何jenkins任务都会保留，因为数据存放在Google持久磁盘中，而持久磁盘Kubernetes会自动的挂载到新的容器实例。

注意，稍后一段时间，GKE会意识到其中一个节点宕掉了，就会再启动一个实例，保持我们集群的规模。

```
$ gcloud compute instances list
NAME                                      ZONE          MACHINE_TYPE  PREEMPTIBLE INTERNAL_IP EXTERNAL_IP    STATUS
gke-kubernetes-jenkins-e46fdaa5-node-5gvr us-central1-f n1-standard-1             10.240.0.4  104.154.35.119 RUNNING
gke-kubernetes-jenkins-e46fdaa5-node-chiv us-central1-f n1-standard-1             10.240.0.3  104.154.82.184 RUNNING
gke-kubernetes-jenkins-e46fdaa5-node-mb7s us-central1-f n1-standard-1             10.240.0.2  146.148.81.44  RUNNING
```


##删除

```kubectl```提供了删除复制控制器、pod、和服务定义的命令。

要停止复制控制器，设置复制数为0，这样就会让所有相关联的pod终止。

```
$ kubectl stop rc/jenkins-slave-v2
$ kubectl stop rc/jenkins

```
删除服务：

```
$ kubectl delete services/jenkins

```

##总结
Kubernetes可以跨多个服务器来管理Docker的部署，简化了长期运行的执行任务，以及分布式的Docker容器。通过抽象基础设施概念和基于状态而不是进程工作原理，它提供了集群的简单定义，包括了很多可用性方面的企业级特性，诸如自我修复能力、集中的日志、服务发现、动态DNS、网络隔离、以及资源配额。简而言之，Kubernetes让管理Docker集群更加点容易。


## 关于作者
![Image of author 1](http://cdn.infoq.com/statics_s1_20151020-0055-2u1/resource/articles/scaling-docker-kubernetes-v1/en/resources/Carlos%20sancez.jpeg)Carlos Sanchez在自动化，软件开发质量，QA以及运维等方面有超过10年的经验，范围涉及从构建工具、持续集成到部署自动化，DevOps最佳实践，再到持续交付。他曾经为财富500强的公司实施过解决方案，在多家美国的创业公司工作过，最近的任职的公司叫做MaestroDev，这也是他一手创建的公司。Carlos曾经在世界各地的各种技术会议上作演讲，包括JavaOne， EclipseCON， ApacheCON， JavaZone，Fosdem 以及 PuppetConf。非常积极的参与开源，他是Apache软件基金会的成员，同时也是其它一些开源团体的成员，为很多个开源项目做个贡献，这里举几个例子，有Apache Maven，Fog 以及 Puppet。


查看英文原文：[Scaling Docker with Kubernetes V1](http://www.infoq.com/articles/scaling-docker-kubernetes-v1)
