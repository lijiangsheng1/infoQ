#亚马逊发布Kinesis Firehose 

## 摘要：
近期，准确的说是2015年10月7日，亚马逊发布了一款新的服务，叫做亚马逊Kinesis FireHose。Kinesis FireHose是亚马逊2年前发布的Kinesis服务的后继服务。为了避免产生歧义，旧的Kinesis服务已经被重命名为亚马逊Kinesis流。

--------------------------------------------------
近期，准确的说是2015年10月7日，亚马逊发布了一款新的服务，叫做亚马逊Kinesis FireHose。Kinesis FireHose是亚马逊2年前发布的Kinesis服务的后继服务。为了避免产生歧义，旧的Kinesis服务已经被重命名为亚马逊Kinesis流。

亚马逊Kinesis Firehose是一款托管服务，只需要很少的管理。可让用户传输应用、监控和日志数据到[亚马逊S3](https://aws.amazon.com/s3/)（简单存储服务）或是[亚马逊Redshift](https://aws.amazon.com/redshift/)表，而无须使用定制的代码。

![image](http://cdn.infoq.com/statics_s1_20151020-0055-2/resource/news/2015/11/Kinesis-Firehose-Announcement/en/resources/Firehose2.png)

图片来源：截屏自[YouTube](https://www.youtube.com/watch?v=YQR_5W4XC94)

来自亚马逊Kinesis的总经理，Roger Barga将亚马逊Kinesis Firehose[分解](https://www.youtube.com/watch?v=lkRoQlhWDXA)为以下三个概念：

1. 交付流均被配置以识别目的地，为了那些进行处理的数据流。
2. 记录指的是一个发布者以数据块地形式让交付流可用的数据，数据块的大小可以达到1000KB。
3.  数据生产者，或发布者，将会作为记录到交付流，比如一个web服务器发送的日志数据。

该服务是在数据被持久化的地方，或者是级联的地方，是面向批处理场景的，在摄入之前时间间隔在60秒到15分钟之间。系统管理员控制缓冲大小和缓冲时间，从而确定移动数据的频率。以下图像描述了这些输入参数是如何被管理的。

![image 2](http://cdn.infoq.com/statics_s1_20151020-0055-2/resource/news/2015/11/Kinesis-Firehose-Announcement/en/resources/DataStreams2.png)

图片来源：[亚马逊官方博客](https://aws.amazon.com/blogs/aws/amazon-kinesis-firehose-simple-highly-scalable-data-ingestion/)

在所支持的特性中也包含了压缩和加密，压缩使用的是gzip压缩，加密是通过亚马逊的[KMS](https://aws.amazon.com/kms/)（密钥管理服务）。通过利用中心化的安全服务，也就意味着其它服务也可使用亚马逊的密钥来解密此数据。

像其它的亚马逊服务一样，Kinesis firehose也提供了自动伸缩的能力，但是需要一点系统管理员的参与。它还提供一些高级功能，包括文件轮询、通过Kinesis[代理](http://docs.aws.amazon.com/firehose/latest/dev/writing-with-agents.html)的检查点、以及若一个S3的bucket不可用了，允许数据持久化保留24小时。

Kinesis Firehose的目标是那些没有任何代码和配置经验的系统管理员。但是，在更加高级别的场景中，开发者还是可以利用Kinesis Firehose所提供的高级API将之整合进他们的应用中。API所提供的[操作](https://www.youtube.com/watch?v=lkRoQlhWDXA)有：

* CreateDeliveryStream －通过所提供的用户的数据将要传输的S3 bucket信息来创建一个交付流。
* DeleteDeliveryStream － 删除一个交付流。
* DescribeDeliveryStream － 返回一个交付流的配置信息。
* ListDeliveryStreams －列出AWS账户下所有可用的交付流。
* UpdateDestination － 为一个交付流更新S3 bucket的配置。
* PutRecord － 将一个单独的达到1000KB的纪录数据放入交付流。
* PutRecord Batch － 将一批纪录（500条纪录或50MB）放入交付流。


亚马逊为用户提供了统一的终端，让用户可以使用一套工具来同时管理Kinesis Firehose和流。但是对于熟悉亚马逊Kinesis流的用户来说，这两个服务之间还是有着几个非常重要的区别的。亚马逊按照下面方法进行了[分类](https://www.youtube.com/watch?v=lkRoQlhWDXA)：

* Amazon Kinesis Streams 是针对哪些每个输入纪录都需定制处理负载的服务，再就是一些小的特性，如可允许1秒钟的处理延时、可选择流的处理框架。
* Amazon Kinesis Firehose 是针对哪些无需任何管理的负载的服务，且可使用现有的基于S3或RedShift的分析工具、数据延时可达60s甚至更高。

查看英文原文：[Amazon Release Kinesis FireHose](http://www.infoq.com/news/2015/11/Kinesis-Firehose-Announcement)
