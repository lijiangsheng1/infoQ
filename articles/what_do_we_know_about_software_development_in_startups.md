#关于创业公司的软件开发我们知道多少？ 

## 摘要：

在本文中，作者们讨论了在创业公司内的软件工程实践，提供了与他们实际相关的工程实践的软件实战经验。他们还讨论了敏捷、进化和机会主义的过程管理。

--------------------------------------------------
[![Image of magazine](http://cdn.infoq.com/statics_s2_20151015-0307/resource/articles/what-do-we-know-about-software-development-in-startups/en/resources/1ieee-software-new.jpg)](http://www.computer.org/web/computingnow/software)本文最初是发表在[IEEE Software](http://www.computer.org/web/computingnow/software)上，[IEEE Software](http://www.computer.org/web/computingnow/software)是一家提供关于技术前瞻问题的权威性的，得到同行一致认可的杂志。目的是为了满足企业日渐所运行的可靠、灵活的提出的挑战，面向IT经理和技术领导者，提供专业的、国内领先的解决方案。

创业公司是指新创立的公司，或者是在技术和市场上没有什么历史的公司。单就美国而言，每个月就有476,000家公司成立，[^1]创造的就业岗位接近全国的20%。[^2]为此，创业公司可谓是经济环境中非常重要的元素之一。然后，创业公司的环境是多变的、也是不可预测的、甚至是混乱的，这就迫使创业者要迅速行动、快速失败、更快的学习来寻找利基市场和可持续的收入。60%的创业公司在第一个五年不回存活下来。75%的由风险投资公司所投资的创业公司会失败。[^3]大多数是因为创业公司的高风险、错失了市场的机会或者其它什么原因。对于由于项目周期延长而导致的高失败率至今还没有研究表明到底占有多大的比例。我们尝试收集和调查来自相关创业公司的所有已知的软件工程实践，以及通过分析来准确而可靠的证明这点。[^4]我们认为这是迈入更大的未知领域的第一步，这个未知领域就是进入创业公司中的软件工程实践的世界。

##话说什么是创业公司？
在过去，术语“startup”是有很多个意思的。看下现在的研究人员和相关人员所采用的解释（表一有完整的列表），一个startup是指一个小型的寻求新的业务机会的公司，使用并不怎么出名的解决方案来努力的去解决一些问题，而且所在的市场也极不稳定。那些新创立的公司未必就可定义为一个创业公司。通过研究表明高度的不确定性和快速的发展是创业公司的两大特征。我们通过使用系统映射学习方法来检索和评估实证证据（见边栏）。

##创业公司的软件开发
“完成比完美重要”以及“快速移动且要突破一些事情”，当你进入到创业公司的工作区域时会看到这样的箴言。这些箴言背后所代表的内容是来自超过200多个创业公司工作的实践。我们筛查了这些内容，认为研究他们之间的差距和未来的开发是有必要的。

###流程管理是敏捷的、进化的、机会主义的
在创业公司中流程管理代表了用于管理产品开发的所有工程活动。因为灵活性对于创业公司来说能够使用频繁的变化至关重要，敏捷方法论被认为是最可行的流程－他们鼓励变化、允许开发去适应业务的策略[^5]。以增量和迭代的方式快速发布可以缩短从创意构思到生产部署的时间。其中一个敏捷的变体就是精益方法[^6]，此方法倡导识别软件业务中风险最大的部分，且据系统的测试提供最小化的可行办法，以及在下一代产品迭代时的修改计划。在此方面，原型是缩短上市时间必不可少的。为了能够更好的设计原型，在第一阶段需要实现“软编码”的进化工作流程，直到找到最优解为止。尽管在开发中用来鼓励快速的开发原型使用了多种方法论，但是创业公司没有一个是按照某种方法论严格执行的。然而创业公司的不确定和快速变化的性质驱使他们寻找最小化的流程管理来实现短期的目标，以快节奏的学习过程来适应用户，从而解决市场的不确定性。

###表一

|    特征   |    描述   | 
|:------:|:------:|
|资源匮乏| 经济、人力、以及物理资源都严重缺乏。 |
|极速响应| 创业公司可以快速的响应来自市场、技术和产品的变化（相比于大多数的已有的公司） |  
|  创新  | 在高度竞争的生态环境中，创业公司需要专注且要探索高度创新的市场定位。  |
|不确定    | 创业公司要处理高度不确定的生态，在不同的方面：市场、产品功能、竞争对手、人力、以及财务。  |
|快速进化    | 成功的创业公司目标是快速的增长和扩张。  |
| 时间压力   | 环境通常强制创业公司去快速发布以及在压力下工作（日程、演示、投资者的要求等）。  |
| 依赖第三方   | 因为缺乏资源，创业公司严重依赖于外部的解决方案来构建他们的产品：外部API、开源软件、外包、COTS等等。  |
|小型团队    |创业公司通常是几个独立的人开干的。   |
| 单一的产品   |仅有单一的产品或服务来吸引用户。   |
| 缺乏经验的团队   |一个不错的开发团队由少于5年工作经验的人们和刚刚走出校门的大学生组成。   |
| 新公司   | 公司是最近才刚刚创建。  |
|完善的组织    | 创业公司通常是以创始人为中心，且每个人在公司都肩负着很大的责任，无须由上至下的管理。  |
|高风险    | 创业公司的失败率非常之高。  |
| 不能自持   | 尤其是在早期阶段，创业公司需要外部的资金来支持他们的活动（风险投资、天使投资、个人资助等等）。  |
|少工作经验    |最初是没有任何企业文化的。   |

###软件开发是由扮演设计者角色的客户所驱动的

创业公司正在经受着能够快速的证明他们所正在开发的解决方案是真正可解决某些问题的压力[^7]。他们要不断的优化问题／解决方案去适应需求。为了实现这个目标，创业公司必须去找到第一个客户的真实需求，只能通过定义一组最小化的功能需求来检查业务的猜测[^8]。

多数的人们都承认客户／用户在根据他们的主要需求来诱导和排优先级的过程的重要性。然而，这些所谓的以市场为驱动的这些个需求亦要求变化。举例来说，创业公司可以利用以用户故事的形式的场景来识别需求并为每个故事预估工作量。然而，打磨一个不请自来的需求也是要花费一番功夫的。需求的获取办法正在走向测试问题以及在进入市场之前做到理解真实的需求（所以叫做客户开发过程）。[^7]

在创业公司的环境中，通常是客户主导需求，那么开发者就得准备好每天都来应对变化。当功能不断的更新或去除时，能够运用架构和设计模式来将一些特性模块化和尽可能的独立就显得非常的重要。因此，采用容易扩展的设计的架构实践和框架能够在产品和市场都不确定的情况下做到动态的调整。[^9]这些都需要前期的一些努力，可以防止产品复杂性的增长。

科学的证据也指出了经常做代码重构是有好处的。如果是由于用户的突然增长而必须去立即扩展的话，重新实现整个系统是代价极大而且风险也大。因此需要一些品质上的保证，从而为用户提供最大化的价值。持久的老客户承认通过焦点小组尽早的采用可以为发现较大的缺陷提供一个省时且高效的方法。但是对于轻松访问的自动化测试框架和更加实用的用户界面测试的方法的解决方案来说还是稀缺。

###团队是开发的催化剂
时间的压力和资源的匮乏让创业公司智能选择一种松散的组织结构，而不是传统企业的管理层级[^10]。

授权给团队成员代表着这是主要的用来提高效率和成功的可行方法。[^11]团队必须能够做到快速的从试验和错误中学习和吸收从而适应新的紧急措施。开发创新的产品需要有创意－一种能够应用新角色的能力，每天都要面对新的挑战，加班更是家常便饭。

的确，在一家创业公司的起步阶段，需要有专业的知识来弥补资源匮乏的情况。另外，拥有类似业务领域的过去的经验以及优秀企业的特点（勇气、激情、兑现承诺、领导力）对于创业的技能都是非常重要的部分。

然而，架构的确是也会隐藏一些重要的活动，诸如共享知识、团队协作，这尤其是在公司快速成长时表现的会更加的明显。在这种情况下，对于促进非正式的沟通和团队成员之间的密切互动，团队成员的搭配就显得非常的关键了。

###公司接受产品和管理人员的变动
创业公司拥有能够采用最新技术和开发工具的优点，还毋需担心过去历史遗留的经验。[^12]但是选择一种技术需要考虑到特定领域或产品方面的需求，这些新的技术或开发工具处于早期阶段时往往有着意想不到的问题。

通常情况下，创业公司的雇员喜用技术在产品和管理中去应对快速的变化。[^13]比如一般用途的基础设施，诸如配置管理、问题报告、追踪和规划系统、日程和通知系统等。轻松实现的工具，诸如白板以及可以掌控快速的信息变化的技术，创业公司很少去做培训和为维护买单。为了缓减资源匮乏的压力，创业公司经常在必要时会选择使用开放源代码软件解决方案，开源解决方案能够让创业者们免费利用那些不断发展的大型的资源池。

创业公司急于寻找利益增长点和获得投资，从而得到进一步的发展。这也就意味着软件质量并非是他们主要关心的。为了能够快速的验证产品，他们倾向于利用特定的敏捷或精益方法。[^14]

有证据表明工程活动必须是试验性的，以在开发的工作流中允许更大的灵活性和更快的反应。在创业公司中的决策者们面临的是难以预测的不确定性；原因和结果之间的关系在回顾中只能可以被感知，而不是其他。[^15]采取严格的方法论去控制开发的活动显然是不可行的，因为不管经过多长时间的分析，都不可能找出所有的风险和准确的预测开发产品需要什么样的实践。

另外一方面，灵活性和快速反应的设计可以收集用户的反馈，以为决策者提供更多的观点和方案。开发者需要自由的来快速的选择一些活动，一旦发现结果是错误的就立即停止，修正方法，然后从过去的失败中吸取教训。与精益创业所倡导的是一致的，我们期望创业公司选择来自常见的敏捷实践的方法论和技术试验的文化，而且是需要的；要去完全的接受失败，或者甚至要优选更快的学习过程。

据通用的实践报告，下面所列出是赶上快速发展的技术和市场浪潮的那些方法：

* 根据市场需求使用众所周知的框架来快速的适应产品的变更；
* 通过已有的组件来使用进化的原型和实验； 
* 持久的客户承认成立专门的团队来作早期的采用者；
* 持续的价值交付，专注于从事那些为付费用户服务的核心功能;
* 团队的授权会影响到最终到结果；
* 使用量化来快速的学习用户的反馈和需求；
* 使用容易实现的工具来促进产品的开发，且要掌控快节奏的、不断变化的信息。

现在的创业公司都是在实践中应用最为前沿的新技术。不断增长的创业现象打开了未知的机会以及给研究这些带来了很大的挑战。“创业者们”在处理高度不确定的实践中需要更多的交流背景和观点以确定可靠的结果。

##参考
[^1]: R.W. Fairlie, “Kauffman Index of Entrepreneurial Activity,” Kauffman Foundation, 2014.

[^2]: R.W. Fairlie, “State of Entrepreneurship Address,” Kauffman Foundation, 2014.

[^3]: C. Nobel, “Why Companies Fail, and How Their Founders Can Bounce Back,” Harvard Business School, 2011.
[^4]:  N. Paternoster et al., “Software Development in Startup Companies: A Systematic Mapping Study,” Information and Software Technology, 2014; DOI: 10.1016/j. infsof.2014.04.014
[^5]: G. Coleman and R. O’Connor, “An Investigation into Software Development Process Formation in Software Start-ups,” J. Enterprise Information Management, vol. 21, no. 6, 2008, pp. 633–648.
[^6]: E. Ries, The Lean Startup: How Today’s Entrepreneurs Use Continuous Innovation to Create Radically Successful Businesses, Crown Business, 2011.
[^7]: S. Blank, “Why the Lean Start-Up Changes Everything,” Harvard Business Rev., vol. 91, no. 5, 2013, p. 64.
[^8]: S.-C. Li, “The Role of Value Proposition and Value Co-Production in New Internet Startups: How New Venture e-Businesses Achieve Competitive Advantage,” Portland Int’l Center for Management of Engineering and Technology (PICMET), 2007, pp. 1126 –1132.
[^9]: S. Yogendra, “Aligning Business and Technology Strategies: A Comparison of Established and Start-up Business Contexts,” Proc. Int’l Eng. Management Conf. (IEMC), 2002, pp. 2–7.
[^10]: Y.-W. Yu et al., “Entrepreneurial Success for High-Tech Start-ups: Case Study of Taiwan High-Tech Companies,” Proc. 6th Int’l Conf. Innovative Mobile and Internet Services in Ubiquitous Computing, 2012, pp. 933–937.
[^11]: E. Carmel, “Time-to-Completion in Software Package Startups,” Proc. 27th Hawaii Int’l Conf. System Sciences, 1994, pp. 498–507.
[^12]: S.M. Sutton, “The Role of Process in Software Start-ups,” IEEE Software, vol. 17, no. 4, 2000, pp. 33–39.
[^13]: M. Crowne, “Why Software Product Startups Fail and What to Do about It,” Proc. Int’l Eng. Management Conf. (IEMC), 2002, pp. 338–343.
[^14]: S.W. Ambler, “Lessons in Agility from Internet-Based Development,” IEEE Software, vol. 19, no. 2, 2002, 66–73.
[^15]: C.F. Kurtz and D.J. Snowden, “The New Dynamics of Strategy: Sense-Making in a Complex and Complicated World,” IBM Systems J., vol. 42, no. 3, 2003, pp. 462–483.


##验证内容的证据

用来在某些特定领域内的结构化的经验证据的系统映射理论。[^16]我们确认了43家工作室，调查了来自不同方面的创业公司以及他们的软件开发流程。在此领域我们还评估证据的力度，通过评估研究的相关性和严谨性来实现。（参考下图）[^17]严谨性是指关于设计、有效性的威胁、以及结果的精度和完整性。相关性是指现实环境中的执行力以及传输结果到执行人员的潜力。

我们的严谨性和相关性的评估表明，对于创业公司的现象的实证研究还处于很不成熟的阶段。只有少数－10/43映射的研究－提供了传达并达到可靠的结果给执行人员（扇形A）。同样的，有10家所研究的结果是－提供了不够严谨的和相关（扇形C）。更多的研究表明，（23家）表现出适度的相关性，但是严谨程度更低（扇形B）。通过此次观察，我们认为在缺乏资源为主要特征的环境下进行研究充满了挑战。研究人员需要更多的努力去和创业公司进行合作研究。

![image of chat](http://cdn.infoq.com/statics_s2_20151015-0307/resource/articles/what-do-we-know-about-software-development-in-startups/en/resources/2fig1.png)
##参考
[^16]: K. Petersen et al., “Systematic Mapping Studies in Software Engineering,” Proc. 12th Int’l Conf. Evaluation and Assessment in Software Eng. (EASE), 2007, pp. 1–10.

[^17]: M. Ivarsson and T. Gorschek, “A Method for Evaluating Rigor and Industrial Relevance of Technology Evaluations,” Empirical Software Eng., vol. 16, no. 3, 2010, pp. 365–395.

## 关于作者

Carmine Giardino：是一名博尔扎诺自由大学的一名在读博士生。他的研究兴趣包括创业公司的软件开发，专注于企业战略和开发活动之间的一致性研究。可通过[cgiardino@unibz.it](mailto:cgiardino@unibz.it)联系他。

Michael Unterkalmseiner ：是一名布莱金厄技术研究所（BTH）的软件工程的在读博士，他的研究兴趣包括开发和测试中协作所需要的、决策支持的信息检索、以及软件仓库挖掘。Unterkalmseiner 同样是在BTH获得的计算机工程的硕士学位。可通过[mun@bth.se](mailto:mun@bth.se)来联系他。

Nicolo Paternoster：是来自www.woodwallets.io的一名创业者。他的研究兴趣有比特币服务开发和创客空间开发。Paternoster拿到了布莱金厄技术研究所和查诺－博尔扎诺自由大学的软件工程硕士学位。可通过[hi@adva.io](mailto:hi@adva.io)联系到他。

Tony Gorschek：是布莱金厄技术研究所（BTH）和查尔莫斯的一名教授，他的研究领域有需求工程、技术和产品管理、过程评估和改进、以及实践创新。Gorschek从BTH获得的博士学位，可通过[tgo@bth.se](mailto:tgo@bth.se)联系他。

Pekka Abrahamsson：是查诺－博尔扎诺自由大学的一名全职计算机科学教授，他的研究领域有软件工程经验、敏捷开发、创业和云计算。Abrahamsson是在芬兰奥卢大学获得的博士学位，可通过电子邮件[pekka.abrahamsson@unibz.it](mailto:pekka.abrahamsson@unibz.it)联系到他。


[![Image of magazine](http://cdn.infoq.com/statics_s2_20151015-0307/resource/articles/what-do-we-know-about-software-development-in-startups/en/resources/1ieee-software-new.jpg)](http://www.computer.org/web/computingnow/software)本文最初是发表在[IEEE Software](http://www.computer.org/web/computingnow/software)上，[IEEE Software](http://www.computer.org/web/computingnow/software)是一家提供关于技术前瞻问题的权威性的，得到同行一致认可的杂志。目的是为了满足企业日渐所运行的可靠、灵活的提出的挑战，面向IT经理和技术领导者，提供专业的、国内领先的解决方案。


查看英文原文：[What Do We Know about Software Development in Startups?](http://www.infoq.com/articles/what-do-we-know-about-software-development-in-startups)
