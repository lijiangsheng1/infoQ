# 开源创业的那些事（一）：缘起

## 摘要：

来自 Lucidworks 的联合创始人兼首席技术官 Grant Ingersoll 将给大家讲述如何利用开源项目来构建商业公司的体会和心得。本篇为 Grant 在 OpenSource.com 上建立了《开源创始人》专栏的首篇文章，主要是介绍了自己将会在这个栏目里做些什么样的事情。

--------------------------------------------------

在开源软件界，如果你为代码库贡献了足够多的补丁的话，绝大多数的项目都会将你视为提交者（committer）。同理，我猜测若是你能为 Opensouce.com 写了很多篇[文章](https://opensource.com/users/gsingers)的话，他们为你专门开辟一个专栏的话，我是丝毫一点也不觉得的有什么值得惊奇。我就这是这么一路走过来的，我的专栏名就叫做《开源创始人》，我打算在此专栏开辟新的内容，不再局限于过去的专门的技术话题，虽然它们是我的挚爱－开源的搜素引擎、自然语言处理（NLP）、和机器学习，我会利用此平台撰写针对开源更为广泛的内容，这些内容来自于我作为一家公司的创始人的背景，以及在开源中作贡献这样关键的行为。另外，我还打算对开源创业中的有特色的人物和公司做几期专访，目标是能够带来一些深刻的洞见，不仅仅是在消费开源代码，而是基于开源的生存方式的息息相关的方方面面。

在开始之前，还是有必要做个简单的自我介绍的。在2007年，我和他人合伙创建里[Lucidworks](https://lucidworks.com/)公司，一家基于[ Apache Lucene 和 Solr](https://lucene.apache.org/)及其周边的开源公司，我还是项目[Apache Mashout](http://mahout.apache.org/)的共同创始人，并主导写作了图书 [Taming Text](https://www.manning.com/books/taming-text)（中文版[《驾驭文本》](http://www.broadview.com.cn/?#book/bookdetail/bookDetailAll.jsp?book_id=33cc24a8-842e-4781-b172-ef5e39f971e7&isbn=978-7-121-25230-3)，已由博文视点出版），同时也是开源的搜索、自然语言处理、机器学习的布道师。

![image of openidea](https://opensource.com/sites/default/files/styles/image-full-size/public/images/business/bus_sharing.png)

和大多数上世纪90年代中期毕业的开发者一样，我和开源的故事要追溯到早期使用[Apache Httpd 服务](https://httpd.apache.org/)、[Tomcat](http://tomcat.apache.org/)、以及[Jakarta](http://jakarta.apache.org/)的那些日子。那段时光非常的有意思，尽情的享用来自 [Apache 基金会](http://www.apache.org/)和其它开源社区的恩赐。一直到2004年，其实我一直都未对开源有任何的贡献。当我加入到锡拉丘兹大学的自然语言处理中心时，机会悄然而至，当时我在构建一个跨阿拉伯语和英语的语言搜索引擎（举例来说，输入英语词条，可以返回阿拉伯语的结果。）

经过了大学时代的训练之后，有一天，我的老板对我说，“我们在使用 Lucene，去将它搞明白了。” 于是我的开源之路就这么开始了。那时的 Lucene （版本是1.2）和现在的 Lucene （版本是5.4）比起来简直弱爆了，尚处于蹒跚学步的“婴儿期”，我们需要的很多功能都没有（（对于一个搜索领域的极客来说：）term vectors 和一些语言的位的掌控都没有）。之后的事情就是提交了一些完善功能的补丁、在邮件列表中帮助他人、积极的参与讨论（还要花时间去认识其他的开发者）等等，然后我就被委员会邀请正式的成为了一名提交者。Lucene 后来的发展，我就这么一路走过来了。

在2007年的时候，我们三个提交者外加一名 Lucene 的忠实用户一起创办了一家公司，也就是现在的 Lucidworks，目标是成为搜索界的红帽！我们成立公司之后的第一次会议上我面对面的见到了我的合伙人（Erik Hatcher），尽管我们在社区合作了很多年。同一年，我和他人共同发起了 Mahout 项目，也开始找一些潜在的出版商开始推销我的书－《驾驭文本》。

就这样又过了几年，我从一个全职的写代码的码农渐渐变成了一名管理者，管理着在开源和闭源混合环境下的工程师们。我对诸如 Lucene、Solr 等项目的贡献已经很少了，而且也渐渐的远离了它们，但是我只要有时间还是会去作贡献的，当然，这要在我自己维护的几个开源项目之余进行。而且我们公司的商业模式也做出了[改变](http://opensource.com/business/15/5/3-lessons-running-open-source-company)，从主要是提供咨询和支持转变为销售开放核心的数据平台，平台集成了我们的核心（Solr、Spark）和一些次要的开源项目，以及我们基于这些项目之上作的增值开发。

我本人对于开源的理解也又了很大的改变：对于开源的概念从一名理想主义者转变成为了实用主义者。开源已经从隐藏在地下的骇客们小范围的传播蜕变成为了来自世界各地的开发者们协同完成项目的方式。

虽然我依然相信开源的理想，但同时我也明白了为了能够让开源取得持续的成功，必须要有商业上的投资，以及让一些人和公司能够生活下来。在哪里以及如何获得投资（举例来说，通过基金会、“商业化”的开源、个人贡献），还有相关的商业模式，都是值得去讨论而且有许多丰富的话题去讨论，这就是本专栏要做的事情。现在，非常欢迎你能够加入到我们的讨论当中。我非常期待探索开源除了代码之外的领域，并能够引起大家的讨论！

若你对本专栏有什么想法的话，请将你的建议发送到[open@opensource.com](mailto:open@opensource.com)。

## 关于作者
![Image of author 1](https://opensource.com/sites/default/files/styles/profile_pictures/public/grantingersoll_.jpg) Grant 是[Lucidworks](http://www.lucidworks.com/)的联合创始人兼首席技术官，是由曼宁出版社发行的《驾驭文本》的联合作者之一，也是 Apache Mahout 的共同创始人，而且还是 Apache Lucene 和 Solr 开源项目的长期贡献者。Grant 过去的工作经验包括各种搜索的引擎、用于各个领域和语言的问答和自然语言处理应用。他拥有阿默斯特学院的数学和计算机科学的学士学位，以及雪城大学的计算机科学的硕士学位。在空闲时间，他享受与家人待在一起，业余爱好由骑自行车、攀岩和徒步旅行。

本文由作者[Grant Ingersoll](https://opensource.com/users/gsingers) 发表在Opensource.com上：[Let's talk about how to build a business with open source](https://opensource.com/business/16/2/open-founder)。经授权，在InfoQ中文站翻译共享。本文在[Creative Commons BY-SA 4.0](http://creativecommons.org/licenses/by-sa/4.0/)许可证下发布。
