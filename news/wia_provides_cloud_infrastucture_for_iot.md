#Wia为物联网提供云基础设施 

## 摘要：


--------------------------------------------------
[Wia](http://www.wia.io/)的目标是为[物联网](http://www.infoq.com/iot)（IoT）解决方案的开发者们提供可扩展、强大后端的云平台。据Wia的创始人兼CEO Conall Laverty声称，Wia将允许创建完全成熟的，生产就绪的解决方案，而无需担心服务器管理，数据复制和存储。InfoQ就此采访了Laverty。

Wia平台所提供的主要特性有：

* 设备管理，包括设备的创建、恢复和删除等。
* 事件和日志掌控，包括发布一个事件／日志以及订阅／取消订阅到事件／日志。
* 分析，可以实时的跟踪任何数据点。
* 发布事件。

Wia还提供了用户和组织的管理和认证。所有的Wia的特性不仅可以通过其提供的[REST API](http://docs.wia.io/)访问，还可以通过其web门户访问。事件和日志还可使用[MQTT协议](http://mqtt.org/)将之流化。MQTT是构建在授权给一个”小的代码足迹“的TCP/IP之上的一个轻量级的消息协议，且是专门针对在带宽有限的网络中使用。官方针对[Node.js](https://github.com/wiaio/wia-nodejs-sdk)和[iOS](https://github.com/wiaio/wia-ios-sdk)提供了开源库的支持，目的是让访问Wia的REST API更加的容易。

Wia云平台面临着主流的云服务提供商的竞争，如亚马逊Web服务，最近发布了的[AWS IoT](http://www.infoq.com/news/2015/12/aws-iot)产品也已可用，以及IBM，有产品[IBM IoT基础平台](http://www.infoq.com/news/2015/12/ibm-iot-watson)。InfoQ就Wia的产品和其面临的形势采访了Conall Laverty。


** Wia对于物联网解决方案主要是解决程序员的何种问题？什么是专门针对IoT的云平台所能提供的，有何相关的特性？ **
>>
Wia的目标是通过开发一个实时的物联网平台解决复杂性和降低用户的成本。我们始终坚信，双向的通信很重要，所以我们围绕MQTT构建了我们的平台。此协议不仅能够提供发送传感器数据，对于控制执行器也很优越。

** Wia和相关的服务提供商该如何比较？如[AWS IoT](http://www.infoq.com/news/2015/12/aws-iot)或[IBM IoT基础平台](http://www.infoq.com/news/2015/12/ibm-iot-watson) 。**
>>
Wia所提供的是一个全栈式、完全外置的平台。和竞争对手不一样的地方在于，我们为开发者提供了他们所需要的全部的软件，从设备应用程序、云端点的连接、到构建他们自己的控制面板的程序库、乃至移动app的经验。

** 以您的直觉判断物联网演进的方向是什么？下一代物联网的关键技术是什么？
>>
物联网目前在横向上已经较为完善了，我们认为当回落到纵向上和一些关键的问题得到解决后会有更多有意思的事情发生，蓝牙4.2看起来非常值得期待。TCP／IP和mesh一起使用将是一次完美的组合，可创建低成本的、范围更广的物联网网络。

Wia提供了一免费的套餐，对设备数量没有限制，且每月的请求可达250,000。

查看英文原文：[Wia Provides Cloud Infrastructure for IoT](http://www.infoq.com/news/2016/01/wia-iot-cloud-platform)
