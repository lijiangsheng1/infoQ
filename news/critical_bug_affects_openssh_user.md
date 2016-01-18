#OpenSSH新曝出严重Bug，影响广泛。
## 摘要：


--------------------------------------------------
据最新的Bug报告，OpenSSH的版本从5.4到7.1均有此一严重的漏洞，基于这些版本的OpenSSH用户需及时的给这些系统打补丁。注意，此bug会同时影响到OpenSSH的特定OpenBSD版本以及相关的移植版本。

这个新发现的漏洞是由一个功能叫做`roaming`所引起的，而这个功能主要是用于SSH连接的断开续连的，这当然会影响到用户的。但是SSH的服务端从来就没有实现过此功能，但是SSH的客户端则会受到被恶意主机利用的潜在危机。该漏洞能够允许让恶意服务器主机能够访问客户端所在的系统的内存，而在客户端的内存中则可能就包含了用于访问私有主机的用户密钥。


漏洞的修复者Damien Miller特别[提示](https://lists.mindrot.org/pipermail/openssh-unix-dev/2016-January/034680.html)：
>>
服务器主机的认证密钥是防止由中间人利用的，所以此次的信息泄露仅限于那些恶意的或已经被攻破的服务器。

** 重要提示，没有打过补丁的客户端是非常脆弱的，因为这个特性默认情况下是开启的。 ** 更加糟糕的是，`UseRoaming`属性并不常常在配置文件中出现，所以通过简单的扫描SSH配置文件，不能轻易的下结论说此系统就是没有问题的。

修复此漏洞的补丁已经释出，并整合到了最新的版本中，而且移植版本OpenSSH 7.1p2也已[发布](https://lists.mindrot.org/pipermail/openssh-unix-dev/2016-January/034680.html)。若用户不想在自己的系统中升级OpenSSH的话，使用下面几种配置中任意一种，它们均可以阻止有漏洞的代码的执行：

* 在全局配置文件中（通常是`/etc/ssh/ssh_config`）增加配置` “UseRoaming no” `
* 在用户的配置文件（通常是`~/.ssh/config`）增加配置`“UseRoaming no”`
* 在调用SSH命令行中加入参数`–oUseRoaming=no`

此Bug的发现要归功于Qualys安全咨询团队，也感谢他们的及时报告。这里提醒的是7.1p2的发布还包含了其它一些bug的修复，所以建议尽可能快的升级程序。关于漏洞的更多细节，请移步参考[CVE-2016-0777](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-0777)和[CVE-2016-0778](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-0778)。Qualys公司将他们的安全顾问经验分享在了[Seclists](http://seclists.org/oss-sec/2016/q1/97)上了。

查看英文原文：[Critical Bug Affects OpenSSH Users](http://www.infoq.com/news/2016/01/openssh-roaming)
