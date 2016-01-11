#Clair安全加固Docker镜像 

## 摘要：


--------------------------------------------------

[Clair](https://coreos.com/blog/vulnerability-analysis-for-containers/)是[CoreOS](https://coreos.com/)最近发布的一款[开源容器漏洞扫描器](https://github.com/coreos/clair)。此工具会对Docker镜像的操作系统和其所安装的软件进行交叉检查，以匹配已知的不安全的软件版本。这些已知漏洞来自操作系统中立的通用漏洞披露([CVE](https://cve.mitre.org/))数据库。目前支持的操作系统有[红帽](http://rhn.redhat.com/errata)、[Ubuntu](http://launchpad.net/ubuntu-cve-tracker)、以及[Debian](http://security-tracker.debian.org/tracker)。

通过从镜像的文件系统提取静态的信息以及保存[镜像的不同版本之间的相异的](https://docs.docker.com/engine/introduction/understanding-docker/#how-does-a-docker-image-work)部分列表，可以有效的缩短分析时间，而且还毋需是实际运行中的存在潜在漏洞的容器。所有的镜像都依赖于一个漏洞较少的镜像，这样可以快速的识别漏洞，这样归功于[使用了图的存储](https://www.youtube.com/watch?v=PA3oBAgjnkU)，从而无需重新分析镜像。

CoreOS[使用Clair来分析镜像](http://blog.quay.io/security-scanning-beta/)，即那些由用户上传到[Quay.io](https://quay.io/)的镜像，Quay.io是一个类似于DockerHub的容器仓库。[上传到Quay.io上的镜像大多数被发现有漏洞存在](https://docs.google.com/presentation/d/1toUKgqLyy1b-pZlDgxONLduiLmt2yaLR0GliBB7b3L0/pub?start=false&loop=false&slide=id.gccb9ce283_0_158)，甚至是一些高危的如Heartbleed（80%）或Ghost（67%）。今年早些时候由[DockerHub](https://hub.docker.com/)发布的一份报告称[至少有30%的官方镜像和40%的上传镜像存在高危漏洞](http://www.infoq.com/news/2015/05/Docker-Image-Vulnerabilities)。Docker同时也发布了[Nautilus项目](https://blog.docker.com/2015/11/dockercon-eu-2015-docker-universal-control-plane/)，这是Docker自己的漏洞扫描和发现工具。在[DockerCon EU 2015](http://europe-2015.dockercon.com/)会议上，又发布了一些[其它的新特性](http://www.infoq.com/news/2015/11/docker-security-containers)。目前Nautilus还没有开源，仅在DockerHub内部使用。

在这个市场内还有一些容器的安全漏洞扫描软件，比如IBM的[Vulnerability Advisor](https://developer.ibm.com/bluemix/2015/07/02/vulnerability-advisor/)或者是[FlawCheck](https://www.flawcheck.com/features/container-inspection/)。它们之间的主要区别就是所有权不同，以IBM为例，仅适用于托管在IBM[Bluemix云平台中的](http://www.ibm.com/cloud-computing/bluemix/)镜像。IBM的解决方案还提供了一些[基本的安全规则](https://developer.ibm.com/bluemix/wp-content/uploads/sites/20/2015/06/policy.jpg)（举例：“密码将在90天后过期”），会生成一份类似于静态代码分析的警报。

当然，这些工具均是探测潜在的风险漏洞的存在，而并不是真正在使用中去验证的。同样，它们也无法在运行中的实例中发现，比如在运行时安装的有风险的漏洞，就无法探测出来。

Clair提供了[JSON API](https://github.com/coreos/clair/blob/master/docs/API.md)且可以在本地去检测容器镜像，例如可作为持续集成或持续交付流程的一部分。

以下这段初始化的操作（默认配置）以及在启动Clair的本地服务：


```
$ git clone https://github.com/coreos/clair.git       
# 从Clair的Github仓库克隆代码

$ cp clair/config.example.yaml clair/config/config.yaml  
# 创建一个初始化的配置文件，基于默认的设置。

$ docker pull quay.io/coreos/clair:latest         
# 下载安装有Clair的CoreOS容器镜像

$ docker run -p 6060:6060 -p 6061:6061 -v clair:$PWD/clair/config:ro quay.io/coreos/clair:latest --config=/config/config.yaml 
# 启动服务－确保获取漏洞初始化列表完成 (消息 "updater: update finished")                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 
```
如果流程中生成了[用于部署的只读的Docker镜像](http://www.infoq.com/articles/five-qualities-application-delivery-immutable-infrastructure)，然后将漏洞扫描作为安全测试的一部分来包含进来，那么久有可能将流程中断。举例来说，[（称用于分析的镜像为“tmpimage”），如下](https://github.com/coreos/clair/tree/master/contrib/analyze-local-images)：

```
$ go get -u github.com/coreos/clair/contrib/analyze-local-images 
# 需要安装go

$ $GOPATH/bin/analyze-local-images tmpimage                      
# analyze-local-images 是一个封装过的脚本，其可以分析所有的镜像层

```

上述的例子会找到镜像中任何层的高危或紧急级别的漏洞。它也可以通过提取每层的其它级别的漏洞，[然后提交给Clair的API](https://github.com/coreos/clair/issues/5)。

某单层的漏洞的完整列表（任何级别的，从可忽略的到关键的）都可用于稍后的分析中，举例如下：


```
$ curl -s -H "Content-Type: application/json" -X POST -d \
'{
    "ID": "39bb80489af75406073b5364c9c326134015140e1f7976a370a8bd446889e6f8",
    "Path": "/tmp/docker/layers/39bb80489af75406073b5364c9c326134015140e1f7976a370a8bd446889e6f8.tar"
}' \
127.0.0.1:6060/v1/layers
# 为Clair提交镜像层来分析并存储到DB中
$ curl -s "127.0.0.1:6060/v1/layers/39bb80489af75406073b5364c9c326134015140e1f7976a370a8bd446889e6f8/vulnerabilities?minimumPriority=Negligible" | python -m json.tool > all_vulnerabilities.json
# 检索在该层中发现的所有漏洞

```

CoreOS最近在[Tectonic](https://tectonic.com/)中还发布了[分布式可信任计算（DTC）](https://tectonic.com/trusted-computing/)，Tectonic是他们的[容器即服务提供商](http://www.infoq.com/news/2015/05/tectonic)，DTC建立了一个全栈道安全链，从应用层，到镜像，到操作系统，乃至底层的硬件。



查看英文原文：[Clair Helps Secure Docker Images](http://www.infoq.com/news/2015/12/clair-docker-vulnerabilities)
