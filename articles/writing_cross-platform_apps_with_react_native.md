#使用React Native来撰写跨平台的App

## 摘要：
本文是来自Twitter的工程师，step-by-step教你如何利用你 React Native 写出原声的 iOS 和 Android 的应用程序来。当然，还有一些关于 React Native 的简单介绍。

--------------------------------------------------
React Native 是一个 JavaScript 的框架，用来撰写实时的、可原生呈现 iOS 和 Android 的应用。其是基于 React的，而 React 是 Facebook 的用于构建用户界面的 JavaScript 库，但是这里不是给浏览器解释的，而是为移动平台。换句话说：如果你是一名 web 开发者，你可以使用熟悉的框架和单一的 JavaScript 代码库，即 React Native来撰写清晰的、高效的移动应用。

我们以前都听说过那些个通用的 app 开发，比如框架 Cordova 和 Titanium，那实际使用 React Native 是一种什么样的情况了呢？在本文中，我们会解释 React Native 到底是什么，以及其是如何工作的，再然后我们以撰写实际的 iOS 和 Android 应用来一探 React Native 究竟。在最后，希望读者能够看到有足够的理由在下一个移动应用中选择使用 React Native。

## 那么什么是 React Native？

在我们深入到开发的经历之前，我们先来探讨下 React Native是什么，并花一些时间来讲述下它是如何工作的。

### 也只是 React

React 是用于构建用户界面，通常是基于 web 的 JavaScript 程序库。由 Facebook 开发并在2013年将其开源，React 已经得到了颇为广泛的使用。但是其使用的范围比较狭窄，它仅是用于渲染用户的应用程序的界面，而不是更大的 MVC 框架。

React 让开发者们纷涌而至的原因有很多，诸如轻量级、骄人的性能、尤其是可以快速的变更数据。这均与它的组件结构密切相关，它也同样鼓励人们去撰写更加模块化的、可重用的代码。

React Native 也只是 React，但是是针对移动设备的。也有一些少许的不一样的地方，比如开发者需要使用```<View>```组件而不是```<div>```，```<Image>```代替```<img>```。开发者的体验多数是一致的。当然，有一些 Objective-C 和 Java 知识是非常有用的，移动开发有其自身的一些颇为棘手的问题（我在多个移动设备上测试过没有？触摸屏的目标是否够大？）。即使是这样，若是开发者曾经有过在浏览器下大 React 经验的话，开发 React Native 会感觉非常的熟悉，并且不会感到不适应。

### 它是真正的原生

关于 React Native 最为让人们称奇的第一件事就是它是”真正的“原生。其它的用于移动设备的 JavaScript 均是以某种包装后的 Web 视角封装了用户的 JavaScripts 代码。他们也许也重新实现了一些本地 UI 的行为，诸如动画之类的，但是用户写的仍然是基于 Web 的应用。

在React中，一个组件能够描述自身的外观；React 处理后再呈现给用户。一个非常清晰的抽象层将两个功能给隔离开来。为了呈现组件给 web，React 使用的是标准的 HTML 标签。这和抽象层是一个道理，即是“桥”的概念，去让 React Native 调用实际的 iOS 和 Android 呈现的 API。在 iOS 中，这意味着 React Native 组件呈现给真正的 UI 视图；在 Android 下，他们也呈现给了本地的视图。

![unknown](http://cdn.infoq.com/statics_s2_20160217-0123u3/resource/articles/react-native-introduction/en/resources/21.jpg)

你将写出看起来差不多就是标准的 JavaScript、CSS、HTML 代码。取代编译为本地代码，React Native 会将你的应用运行在本地平台的 JavaScript 引擎中，毋需屏蔽主要的 UI 线程。你获得了本地的性能、动画、行为，还不用去写 Object－C 或 Java。其它诸如 Cordova 或 Titanium 之类的跨平台应用开发，是无法达到如此级别的本地性能和表现的。

### 更好的开发者体验

相比较于 iOS 和 Android 原生的开发，React Native 提供更好的开发者体验。因为你的程序大多数都是 JavaScript，你可以从 web 开发中汲取大量的经验，比如能够立即“刷新”你的应用来查看你代码的修改。相比于在传统的应用开发中花很长的时间去等待构建的过程，会让人感觉这简直是天赐之物。

另外，React Native 还为开发者提供了智能的错误报告和标准的 JavaSript 调试工具，这些让移动开发更加的顺手。

![brower debug tool](http://cdn.infoq.com/statics_s2_20160217-0123u3/resource/articles/react-native-introduction/en/resources/52.jpg)


## 掌控多平台

React Native 可以平滑的掌控多个平台。绝大多数的 React Native API 都是跨平台的，所以开发者只需要去写 React Native 的组件即可，它可以无缝的运行在 iOS 和 Android 下，脸书声称他们的广告管理应用跨两个平台有[87% 的代码可重用](https://www.youtube.com/watch?v=PAA9O4E1IM4&feature=youtu.be)，还有，我自己所写的 flashcard 的代码没有任何平台有关的代码。

如果开发者打算撰写特定平台的代码，对于 iOS 和 Android 有不同的交互向导，或者干脆点说，开发者想要获得特定平台 API 的独特优势，也是很容易就可以办到的。React Native 允许开发者为每个组件指定特定平台的版本，可以随意集成到其它 React Native 的应用当中。

## 使用 React Native

使用单一的 JavaScript 库就想写出真正的原生的 iOS 和 Android 的应用来，无异于异想天开。那么 React Native 又是如何做到的了呢？

### 上手入门

要开始开发 React Native 应用程序，需要为 iOS 和 Android 的开发安装一些常见的依赖，即使是 React Native。在 React Native [官方站点](https://facebook.github.io/react-native/docs/getting-started.html)上有非常好的指南。设置 React Native 其实蛮简单，如果开发者已经安装了最新版的 Node.js 的话，只需要执行命令 **```npm install -g react-native-cli```** 就可以安装 React Native了。

一旦这些相关的依赖安装完成后，运行 **```react-native init ProjectName```** ，此命令会自动生成开发者开始一个项目所需要的所有样板。

这里有一点需要特别注意：开发 React Native 的话需要使用 OS X 操作系统。开发 iOS 应用，苹果公司强制要求使用 Mac，这一点对于大多数开发人员来说这个限制已经不可避免。如果开发者是专门撰写 Android 应用的话，React Native 还支持 [Windows 和 Linux](https://facebook.github.io/react-native/docs/linux-windows-support.html#content) 平台，不过目前尚处于试验阶段，开发者不妨尝试一下。

### 常见 React 组件

一旦准备好了开发环境，那么就可以开始撰写一些真正的应用程序了。

正如在文章前面所提到的那样，React Native 真的也只是 React，只是有少许不同罢了。React Native 的组件在浏览器中看的话和 React 的组件及其相似，但是基本的构建块已经变了。诸如```<div>```、```<img>```、```<p>```等标签均被替代了，React Native 提供给开发者一些诸如```<Text>```、```<View>```等基本的组件，在下面的例子中，基本的组件使用的是```<ScrollView> ```、```<TouchableHighlight```、以及```<Text>```，所有这些都会映射到 iOS 和 Android 特定的视图，使用它们创建带有触摸控制属性的滚动视图是非常直接的：

```
// iOS & Android

var React = require('react-native');
var { ScrollView, TouchableHighlight, Text } = React;

var TouchDemo = React.createClass({
  render: function() {
    return (
      <ScrollView>
        <TouchableHighlight onPress={() => console.log('pressed')}>
          <Text>Proper Touch Handling</Text>
        </TouchableHighlight>
      </ScrollView>
    );
  },
});
```

如果你没有处理过杂乱无章的 HTML-esque 语法以及 JSX 以前的 JavaScript 的话，这可能对你有一些困惑。React 强烈推荐开发者使用 JSX，那么基于 React Native 的话，其实没有什么可以选择的机会。你渲染的标记是和 JavaScript 所控制的行为共存的。就这一点来说常会引起新接触者强烈的反感，但是我还是强烈建议不妨一试。

因为 React Native 的组件和常见的 React 的组件极为类似，所以切换到 React Native相对是很容易的。

## 样式表

为了让渲染更容易、更加的有效，同样鼓励维护样式代码，React Native 实现了一个严格的 CSS 的子集。这同时也意味着开发者无需去学习特定平台的方法来从而设计视图，当然，开发者还是要花点时间去学习如何使用 React Native 的样式表的。

最大的不同就在于开发者不需要去担心特定的规则，因为样式的继承是被严重削弱过的，而且 React Native 使用的内联样式的语法。

这里是一个如何使用 React Native 来创建样式表的实例：

```
var styles = StyleSheet.create({
  container: {
    flex: 1,
    marginTop: 30
  }
});
```
然后，此种样式是由内联语法所应用的：

```
<View style={styles.container}>
	...
     </View>
```

语法是相当的容易阅读，但是如果开发者是来自于 Web 开发的背景的话，可能会发现有些不妥。（会有一个好的理由让你继续下去的，我保证！）即进一步去阅读关于 CSS，就会发现问题，若是以 React 的方法来解决它们的话，我这里强烈推荐 Christopher Chedeau 演示文稿：[JS 中的 CSS](https://speakerdeck.com/vjeux/react-css-in-js)。

## 设置移动开发环境

React Native 的其中一个比较复杂的部分就是开发环境的设置。当基于 React Native 工作时，开发者针对移动开发需要所有的通常的工具，以及 JavaScript 编辑工具：一个文本编辑器，可能还需要 Chrome 的开发者调试工具。

对于 iOS 来说，这也就意味着需要开着 Xcode，以及 iOS 模拟器。对于 Android 来说，也需要开着的有 Android Studiom、将会用到的命令行工具。最终，开发者还需要运行着的 React Native 包，当然，开发者可以自行决定使用自己喜欢的文本编辑器来编辑 JavaScript 代码。

![java scripts code](http://cdn.infoq.com/statics_s2_20160217-0123u3/resource/articles/react-native-introduction/en/resources/43.jpg)

这么做的后果就是你需要在自己的本地开好多窗口，如此之多的工具，桌面杂乱到着实让人烦恼，但是，这样的 React Native 不会隐藏任何标准的移动开发过程。

## 跳转到原生代码

React Native 工作在已有平台的上 API 所提供的 JavaScript 接口上。在实践中，这意味着开发者可以撰写原先自己熟悉的 React 代码，React Native 的“桥”会自动完成相关的转换，但是若转换的功能不够完善没有彻底搞定的时候该如何处理？

不可避免的是，基于诸如 React Native 这样的新框架来开发的话，总会有一些 API 是不被支持的。若发生了这样的事情，你就需要撰写“本地的模块”来提供主机平台和所开发的 JavaScript 代码之间的通信。下面是一个关于 Objective-C 模块的 “Hello，World”的简易实例：

```
// Objective-C

#import "RCTBridgeModule.h"

@interface MyCustomModule : NSObject <RCTBridgeModule>
@end

@implementation MyCustomModule

RCT_EXPORT_MODULE();

// Available as NativeModules.MyCustomModule.processString
RCT_EXPORT_METHOD(processString:(NSString *)input callback:(RCTResponseSenderBlock)callback)
{
  callback(@[[input stringByReplacingOccurrencesOfString:@"Goodbye" withString:@"Hello"]]);
}
@end
```

然后，要使用开发者本地的 JavaScript 模块的话，和需要其它的库是一样的：

```
// JavaScript

var React = require('react-native');
var { NativeModules, Text } = React;

var Message = React.createClass({
  getInitialState() {
    return { text: 'Goodbye World.' };
  },
  componentDidMount() {
    NativeModules.MyCustomModule.processString(this.state.text, (text) => {
      this.setState({text});
    });
  },
  render: function() {
    return (
      <Text>{this.state.text}</Text>
    );
  }
});
```

开发者这样做可能是因为所需要的 API 还没有得到支持，又或者是集成 React Native 组件到现有的 Objective-C 或 Java 代码中，又或者是需要写一些高性能的功能来处理一些密集的图形处理。非常值得庆幸的是，React Native 已经能够提供非常灵活的撰写和使用这些称之为“原生模块”，只要开发者需要，而且流程也是很顺溜的。哪怕是开发者从来没有 Objective-C 或 Java  的开发经验，撰写“桥”的代码是在和本地的移动开发相当舒服的情况下的一种很爽的体验。

## 部署应用程序

部署 React Native 的应用工作原理和传统的移动应用部署方式及其的类似，这并不是说这会非常的容易，众所周知，移动应用的发布流程是非常令人烦恼的。

要创建一个准备好部署的包，开发者需要使用打包好的 JavaScript 来代替在线重载的开发版本。在 iOS 中，这意味着需要在 ```AppDelegate.m``` 文件中更改一行代码，然后运行 **```react-native bundle --minify```**。对于 Android来说，开发者需要运行 **```./gradlew assembleRelease```**，在这之后，打包的流程就和原来的移动开发过程没有任何的区别了，且最终的打包结果会提交到相关的应用程序商店中。

我的 flashcard 应用在 iOS 应用商店花了两周的时间，在 Google Play 商店花了不到一天的时间。换句话说，批准的时间完全符合我的预期，即和“传统的”移动应用没有任何区别，对于 React Native 所写的程序没有作任何的处罚。

![app](http://cdn.infoq.com/statics_s2_20160217-0123u3/resource/articles/react-native-introduction/en/resources/14.jpg)

有趣的是，苹果允许应用自行更新－－因此绕过了令人头疼的部署过程－－如果只是更新 JavaScript的话。微软最近释出了[CodePush](http://www.infoq.com/news/2015/11/microsoft-codepush-cordova-react) SDK，其允许 React Native 开发者立即更新。这是一个非常好的特性，我希望在接下来的几个月当中能够看到更多的应用程序享用此特性所带来的便捷。

##结论和建议

如果你的背景是基于 web 开发的 JavaScript 工程师的话，我以为你会为 React Native 而高兴的。React Native 可以将任何背景的 web 开发者转变为潜在的移动开发者，而且对于现有的移动开发流程是得到了有效的改进。

当然，React Native 也不是完美无缺的，毕竟她还是一款较新的软件项目，要经受哪些不够成熟的程序库的折磨：有一些特性还是缺失的。而且最佳实践之类的还尚待挖掘。版本之间的变化太过于跳跃，虽然很少发生而且范围也比较有限，但还是偶尔会发生。

然而，React Native 已经足够的成熟，总而言之，好处是远远大于瑕疵的。基于 React Native，开发者可以使用单一的 JavaScript 代码库来创建 iOS 和 Android 的应用，而且还没有质量和性能上的损耗。即使开发者没有 JavaScript 的背景，也很难不被更加快速的开发周期和几乎完全的代码重用这样的好处所吸引。而且因为 React Native 允许开发者在需要的时候切换到“常见”的开发状态，你还不会受限于框架。总而言之，React Native 交付了一款高质量的、跨平台的移动开发工具，如果读者你要加入到移动开发的项目中来，你需要慎重的考虑下使用 React Native。

如果你想更进一步的阅读，我已经出版了一本专门、详细的图书：《React Native 学习》，电子版和纸版均有售卖，可以到[奥姆莱](http://www.tkqlhce.com/click-7874104-11260198-1448292209000?url=http%3A%2F%2Fshop.oreilly.com%2Fproduct%2F0636920041511.do%3Fcmp%3Daf-webplatform-books-videos-product_cj_9781491929056_%2525zp&cjsku=9781491929056) 和[亚马逊](http://www.amazon.com/gp/product/1491929006/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1491929006&linkCode=as2&tag=bonnieisen-20&linkId=IWLKP5BIVDREECM3)上找到。你也可以在Twitter上关注我，我的账号是：[@brindellev](https://twitter.com/brindellev)，我非常期望听到大家使用 React Native 的经历以及疑问。

## 关于作者
![Image of author 1](http://cdn.infoq.com/statics_s2_20160217-0123u3/resource/articles/react-native-introduction/en/resources/bonnie.jpg)Bonnie Eisenman 是来自Twitter的工程师，她是 NYC Resistor 黑客空间的成员之一，之前在Codecademy、Fog Creek 软件以及Google工作过。她也是《 Learning React Native 》一书的作者，《 Learning React Native 》是由 O'Reilly 出版的，介绍使用 JavaScript 来构建原生的 iOS 和 Android 应用的书籍。她也经常在一些研讨会上分享演讲，从 ReactJS，到 音乐编程，乃至 Arduinos。在空闲时间，她非常享受于学习新的语言，做一些硬件项目，用激光切割巧克力之类的。可以关注她的Twitter：@brindelle。

查看英文原文：[Writing Cross-Platform Apps with React Native](http://www.infoq.com/articles/react-native-introduction)
