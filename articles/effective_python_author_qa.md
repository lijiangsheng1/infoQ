#专访《Effective Python》作者Brett Slatkin 

## 摘要：

InfoQ近日采访了Brett Slatkin－－来自Google的高级软件工程师，《Effective Python》一书的作者。

--------------------------------------------------

InfoQ就Brett Slatkin最近完成的新书－[《Effective Python》](http://www.informit.com/effpy)以及新推出的[Effective Python在线课程](http://www.informit.com/effpy)作了采访。其中在线视频的基础教程包括了6个不同的方面，无所谓是否和书一起使用。

 * 课程1: 使用表达式和语句：在课程1中，你会学习到如何以Python行者的风格撰写程序，所使用的方法会影响到你将来编写的每一段程序。
 * 课程2: 使用解析器和生成器：在课程2中，你会学习如何使用解析器和生成器来处理和创建序列。
 * 课程3: 使用函数：课程3涵盖了Python函数的撰写和调用的多种独特的功能。
 * 课程4: 使用类：课程4聚焦于如何正确的使用Python的面向对象编程，同时避免一些常见的陷阱。
 * 课程5: 并发和并行：课程5为你提供了Python内置函数的洞见，即编写的程序能够同时干很多事情。
 * 课程6: 让程序更加的完善：在课程的最后一节，你可以学习到最佳的技术，从而让你的程序在生产环境运行时做到无懈可击。

InfoQ: 初学者应该如何阅读此书？

```
Brett Slatkin: 阅读此书最好的办法就是查看目录，然后看有哪些内容能够吸引到你。 条目是按组来编排的，但是你不需要按照指定的顺序去阅读。你可以根据自己的兴趣随意的挑选章节。这就是阅读本书的最好的方法。我曾从几个读者那里听到过他们喜欢从自己已经知道的内容下手；我也曾从一些高级程序员那里听到我的一些建议让他们在某些方面重新思考，这是件好事；我还从很多的中级程序员那里听到我的一些观点让他们意识到自己原来所做的很多地方都错了。很幸运的是，这些结果都导致读者对书中的更多条目产生了兴趣。另外要注意的是，通过所有的方式来阅读内容非常的重要。深入理解Python绝非只言片语就能够涵盖。许多条目都提供了能够激励读者的例子，这些例子解释了为什么我给出的建议是相关的。在你获得好的部分之前不要停止阅读！

```

InfoQ: 你认为他们应该什么时候开始整合这些提示的学习？

```
Brett Slatkin: 马上！读者所读到的内容都是经过实践可用的。书中的多数内容本身就可自圆其说。如果书中有的内容需要另外的项来阐释的话，我会明确的引用它作为建议，引导读者进行更多的研究。在你成为一个好的Python程序员之前毋须完全读完本书。

```

InfoQ: 有一定经验的Python程序员应如何阅读此书？

```
Brett Slatkin: 我说过对于高级程序员来说，阅读此书应持怀疑态度且保持开放的心态。大多数我所撰写的内容其实很明显的是针对高级程序员的。应该只有很少一部分内容会有争议。本书是我个人10年的Python编程中所学到的最佳实践。在这10年中我很幸运的是曾经和一帮优秀的Python程序员一起共事。如果你发现其中一些内容，你严重不同意，或许是你需要重新审视你的Python编码风格了，又或者是你确实找到了错误！请将错误报告发送到[这里](https://github.com/bslatkin/effectivepython/issues)(非常的感谢能够给我指出错误)。

```

InfoQ: 你对Python和其它流行的语言相比又何看法？如果你给一些打算成为程序员的人提供一些建议，会和那些非程序员但是他们的日常工作又需要他们去学习编程的建议有所不同吗？

```
Brett Slatkin: Python是一门优秀的语言，因为它不仅适合初学者学习如何编程，也适合科学家们为超级计算编程（等等）。Python的应用范围非常的广泛，而且它的社区融合了很多个学科的内容，其多样性的强大之处是其它语言无法比拟的。如果人们从开始就使用Python的话，可以走的很远，甚至都不需要去学习其它的语言。但是话讲回来，我认为对于工作来说你需使用最好的工具。对于系统编程来说我非常感叹于Go的强大威力。在整个工作中，我仍然使用Java和C++，因为它们能很好的针对特定的问题领域。对于iOS开发来说Swift是最好的、游戏开发中C#尤其的擅长、若你不懂JavaScript你就无法开发web应用。当然，你必须学些函数式编程（如Lisp和OCaml）来扩展你的视野。我认为所有的程序员都应该立志精通多门语言，且根据需要随时切换它们。你永远不会知道你接下来将会用到什么样的技能。

```
InfoQ: 新手们应该从Python的2.x还是3.x开始他们的学习之旅？

```
Brett Slatkin: 现在如NumPy，SciPy，Django，以及其它的社区软件包都支持Python 3了。我建议初学者从Python 3开始，而不是Python 2。在版本3中，许多原来不够完善的地方都得到了弥补，这能够让新手更加的容易理解。基于Python 3还有一个好处就是遵循模式：“做正确的事”。这会鼓励那些仍然在使用Python 2（例如，工作中使用）的新的程序员们在Python 2的环境中应用Python 3的最佳实践。这是我在我的书中普遍使用的办法。对于Python 2和3最大重叠的事项提供建议，我会清晰的标注某些情况仅能在Python 3下工作，我也会提供在Python 2中实现同样目的的表达方式。

```

再次感谢Breet腾出时间接受InfoQ的采访。

## 关于受访者
![Image of author 1](http://cdn.infoq.com/statics_s2_20150922-0305u1/resource/articles/effective-python/en/resources/1brett-slatkin.jpg)Brett Slatkin是Google的一名高级软件工程师，他是谷歌消费者调查工程主管和发起人之一，他曾在Google App Engine的Python基础设施部门工作过，他是PubSubHubbub协议的创作人之一。九年前他开始尝试使用Python来管理Google庞大的服务器群。

查看英文原文：[Author Q&A with Brett Slatkin on Effective Python](http://www.infoq.com/articles/effective-python)
