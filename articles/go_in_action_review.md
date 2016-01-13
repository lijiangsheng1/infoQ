#《Go语言实战》内容回顾与作者采访 

## 摘要：
Go语言实战是曼宁新出版的一本技术书籍，目标是提供一个全面介绍Go语言的教程。内容包括语法介绍和内部实现，以及最常见的用法。InforQ借机采访做本书的作者：William Kennedy。

--------------------------------------------------
[Go语言实战](https://www.manning.com/books/go-in-action) 是曼宁新出版的一本技术书籍，目标是提供一个全面介绍Go语言的教程。内容包括语法介绍和内部实现，以及最常见的用法。InforQ借机采访做本书的作者：William Kennedy。

一如曼宁的“实战”系列，Go语言实战秉承了以精简的体积容纳第一手的信息和深入语言内部的洞见。作者对于本书的定位是，拥有一定编程经验但原来并没有Go的基础的中级开发者。

从而，本书的作者们热衷于提供非常清晰的且对每个概念的细节解释，所介绍的内容确保读者能够拥有必要的信息以全面的理解到位。关于此一个极为妥当的例子就是关于讨论Go的内建数据类型－数组、切片和映射－在那里读者不仅可以学习到如何使用它们，而且可了解它们是如何实现的，以及什么样的情形下使用何种类型，举例来说，什么时候切片或者什么时候用到切片的切片。对于有经验的Go的开发者，此书亦有颇大的吸引力，当然这在书中的最后几个章节才有所体现，最后覆盖了一些高级的主题如常见的并发模式、剖析、调试、以及性能调优。

本书有9章的内容，它们分别是：

* 解释Go是什么，且提供了短小但完整的程序（章节1和2）；
* 介绍了包管理的概念，探讨了项目的组织方式，以及Go所提供的工具（章节3）；
* 描述了一些Go内置的数据类型的细节，以及Go的类系统，包括接口和类型嵌入，Go对于C++虚拟和非虚拟继承的另外一种方法。类型嵌入可以看作是自动化成份或委托的形式，嵌入的类型接口会自动通过嵌入类型抛出。接口提供了运行时的多态。（章节4）；
* 探索了Go的并发原语：goroutines，即允许在[轻量级进程](https://en.wikipedia.org/wiki/Light-weight_process)内部执行一个函数；频道，即支持类型安全、在协程之间进行同步通信。除了goroutines和频道之外，Go还支持内存共享和传统的锁原语。此外，一些高级的并发模式有基于频道实现的看门狗，用来管理池的资源和掌管池中的工作者（章节6和7）；
* 介绍了Go的标准库，聚焦于三个包：`log`、`json`、和`io`（章节8）；
* 向读者展示了使用测试和基准工具，在文档中如何添加示例代码然后用它们来做测试（章节9）。

Go语言实战包涵了超过100个的代码实例，其中很多是从标准库中提取出来的，所以用户可以理解为此书提供了实际的例子，即Go是如何解决常见问题的。

InfoQ采访了《Go语言实战》的主要作者，William Kennedy。

InfoQ: 您能解释下写作此书的主要动机是什么吗？有此必要吗？

>>
我早些时候写的[博客](http://goinggo.net/)就是作为Go的初学者学习的地方。我尝试去做到读者并不是超出基础知识水平的。当我被邀请参与此书的写作时，我将之视为能够在更大范围内继续我的认知。在本书写作时，市面上只有两本书出版了，而且它们正在变的过时。我在当初学习Go的时候读过这两本书，所以自我感觉以我的风格写就的书可以带来完全不同的视角。

>>
2年过去了，我认为素材很好的覆盖了一些不同的格式和书籍。我认为[Donovan和Kernighan的Go编程语言](http://www.gopl.io/)和《Go语言实战》是今天学习Go语言的机制、实现、规范最好的两本书。


InfoQ: 您的书的目标读者是有一些编程经验的中级开发者，当他们阅读此书时您有什么建议？什么是他们应该期望的？什么不应该期望？

>>
这很难回答，但是最为重要的事情就是任何开始要学习Go的人应该持一种全新的眼光去看待Go。你学习Go就应该去按照此语言的所设计的思路去写代码。约定俗成的东西至关重要，这没什么好说的。如果你能做到由语言团队和社区所共同遵守的约定俗成的去写代码，就会事半功倍。如果你非得对着干，也可能让程序运行起来，但是会错过很多语言中一些让人惊叹的东西。

InfoQ:Go通常被描述为一种可编程的语言，您能总结下促进此种编程的方法吗？Go的主要特征定义是什么？
 
>>
其核心理念很简单。编写精简的让人容易阅读的代码。当事情变得简单，Bug也会变少，更多的人可以参与进来，随之而来的就是优化。你看到Go的语法是天生简约的，而不是给人惊异。来自外部的语言不是天方夜谭也不会去尝试，来自内部创新的软件的语言则打破常规，为程序员建立了尽可能简单而不是复杂的新局面。毕竟生产力才是程序员的一切。	

InfoQ:高度支持并发是Go的重要特性之一，其拥抱CSP范式和goroutines。麻烦您描述下此模式给程序员们带来的好处？和其它相关的并发模式比较起来呢？例如actors。
 
>>
频道是由Go引进的一项新的并发编程的工具。频道提供了一种编排goroutines以执行工作流的方法。也提供对goroutines的友好机制以及Go运行时的调度方法。我认为actor机制也能够在Go和频道下很好的工作。
>>
Go并不能让撰写并发软件变得简单，我认为太多的人们过度的解读了goroutines和频道。毕竟它们只是工具，需要去用心学习并能够正确的使用它们的。我知道频道让很多人来关注Go语言，但是让人深入或使用Go还得看接口和composition以及语言的简单性。

InfoQ:Go最近作了[替代大量的Python脚本](https://www.reddit.com/r/golang/comments/2aup1g/why_are_people_ditching_python_for_go/)的工作。你认为这将会是一个主要的方向嘛？是Go的哪些特性让这种替代成为可能？
 
>>
我曾经花了两年的时间作语言的教学工作，并有幸接触的是一线的公司。我在我的班里教的编程语言有Python、Ruby、Java和C。我认为越来越多的被采用才是高效程序员所使用的语言。任何人都可以使用Go来写代码，但是写出高质量代码需要走好长的路。能够有效的整合才是高效的表现。

InfoQ:Go摒弃了继承和类型层次的想法，即我们众所周知的OOP。然而，Go依然掌控着类型的组成和接口，看起来蛮有效果。您如何描述这一编程范式？在您个人使用Go的经验中，有没有感到，从另外的地方派生出的类型会更有帮助？
 
>>
我认为Go的最大的优点是隐藏在接口之后机制和嵌入的部分，再加上编译器的设计让程序员更加简单、高效的使用。Go是一门面向对象编程的语言，然而这并非是你去花所有时间去关注的部分。Go允许程序员利用已有的类型来重复使用和扩展它们。Go允许直观的对接口编程且类型安全。此[视频](https://www.youtube.com/watch?v=gRpUfjTwSOo)或许可以帮助你了解这点。
>>
来自composition的观点，此[博客](http://www.goinggo.net/2015/09/composition-with-go.html)讲述了更多的细节。
>>
我希望能够有时间在书中写一些关于composition的实例，在下个版本我会加入。

InfoQ:一个语言的成功与否，工具占据着很重要的位置。在您的书中，您聚焦于语言和它的标准库，关于Go的可用的工具您持何种看法？
 
>>
Go提供的工具是惊人的。语言团队提供了你需要的调试和分析程序的一切。而且社区还构建了对语言团队本身已经提供的进行了扩展的工具。这里有一些你可以浏览到的主题：[testing](https://github.com/ardanlabs/gotraining/tree/master/topics/testing)、[Benchmarking](https://github.com/ardanlabs/gotraining/tree/master/topics/benchmarking)、[memory trace](https://github.com/ardanlabs/gotraining/tree/master/topics/memory_trace)、[schedule tracing](https://github.com/ardanlabs/gotraining/tree/master/topics/sched_trace)、[stack trace](https://github.com/ardanlabs/gotraining/tree/master/topics/stack_trace)。


InfoQ:新近出现了一些语言呈竞争状态，它们有：Go、Rust、D、Scala等。您认为Go能从它们中间脱颖而出吗？
 
>>竞争是不存在的。每一种语言解决不同的问题，且它们是可以共存的，甚至是在同一技术栈中。我喜欢Rust，而且它颇具潜力。我认为语言的语法不一是人们需要花时间去切换的主要原因。我会学习Rust这门语言的。

在[官方站点](https://www.manning.com/books/go-in-action)购买此书时使用代码“goiaiq”，可获得38%的优惠折扣。

您可以下载Go语言实战的[代码示例](http://cdn.infoq.com/statics_s1_20151208-0036_1/resource/articles/go-in-action-review/en/resources/Excerpt_Kennedy4.doc)，从而获得此书的第一印象。

## 关于作者
![Image of author 1](http://cdn.infoq.com/statics_s1_20151203-0208/resource/articles/go-in-action-review/en/resources/Kennedy.jpg)William Kennedy是来自佛罗里达州的迈阿密一家叫做Ardan Studios公司的管理合伙人，Ardan Studios是一家做移动、web应用和系统开发的公司，他是Go语言实战的作者之一，博客GoingGo.net的作者，是迈阿密的Go和MangoDB小型线下聚会的组织者，Bill通过Ardan Labs，他新投资的科技公司，醉心于Go的教育与传播，Bill也经常在一些研讨会上发表演讲，无论是在本地还是通过Hangout。他经常会找一些热衷于Go的知识、博客、编码技能的个体或团队切磋。@goinggodotnet

阅读英文原文：[Go in Action - Review  and  Q&A with Author](http://www.infoq.com/articles/go-in-action-review)

