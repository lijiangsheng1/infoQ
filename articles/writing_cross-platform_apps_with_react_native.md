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



![unknown](http://cdn.infoq.com/statics_s2_20160217-0123u3/resource/articles/react-native-introduction/en/resources/21.jpg)

### 更好的开发者体验

![brower debug tool](http://cdn.infoq.com/statics_s2_20160217-0123u3/resource/articles/react-native-introduction/en/resources/52.jpg)


## 掌控多平台

## 使用 React Native

使用单一的 JavaScript 库就想写出真正的原生的 iOS 和 Android 的应用来，无异于异想天开。那么 React Native 又是如何做到的了呢？

### 上手入门

要开始开发 React Native 应用程序，需要为 iOS 和 Android 的开发安装一些常见的依赖，即使是 React Native。在 React Native [官方站点](https://facebook.github.io/react-native/docs/getting-started.html)上有非常好的指南。设置 React Native 其实蛮简单，如果开发者已经安装了最新版的 Node.js 的话，只需要执行命令 **```npm install -g react-native-cli```** 就可以安装 React Native了。

一旦这些相关的依赖安装完成后，运行 **```react-native init ProjectName```** ，此命令会自动生成开发者开始一个项目所需要的所有样板。

这里有一点需要特别注意：开发 React Native 的话需要使用 OS X 操作系统。开发 iOS 应用，苹果公司强制要求使用 Mac，这一点对于大多数开发人员来说这个限制已经不可避免。如果开发者是专门撰写 Android 应用的话，React Native 还支持 [Windows 和 Linux](https://facebook.github.io/react-native/docs/linux-windows-support.html#content) 平台，不过目前尚处于试验阶段，开发者不妨尝试一下。

### 常见 React 组件

一旦准备好了开发环境，那么就可以开始撰写一些真正的应用程序了。



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
因为 React Native 的组件和常见的 React 的组件极为类似，所以切换到 React Native相对是很容易的。

## 样式表

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

## 设置移动开发环境

![java scripts code](http://cdn.infoq.com/statics_s2_20160217-0123u3/resource/articles/react-native-introduction/en/resources/43.jpg)

## 跳转到原生代码

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

## 部署应用程序

![app](http://cdn.infoq.com/statics_s2_20160217-0123u3/resource/articles/react-native-introduction/en/resources/14.jpg)

##结论和建议


如果你想更进一步的阅读，我已经出版了一本专门、详细的图书：《React Native 学习》，电子版和纸版均有售卖，可以到[奥姆莱](http://www.tkqlhce.com/click-7874104-11260198-1448292209000?url=http%3A%2F%2Fshop.oreilly.com%2Fproduct%2F0636920041511.do%3Fcmp%3Daf-webplatform-books-videos-product_cj_9781491929056_%2525zp&cjsku=9781491929056) 和[亚马逊](http://www.amazon.com/gp/product/1491929006/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1491929006&linkCode=as2&tag=bonnieisen-20&linkId=IWLKP5BIVDREECM3)上找到。你也可以在Twitter上关注我，我的账号是：[@brindellev](https://twitter.com/brindellev)，我非常期望听到大家使用 React Native 的经历以及疑问。

## 关于作者
![Image of author 1](http://cdn.infoq.com/statics_s2_20160217-0123u3/resource/articles/react-native-introduction/en/resources/bonnie.jpg)Bonnie Eisenman 是来自Twitter的工程师，她是 NYC Resistor 黑客空间的成员之一，之前在Codecademy、Fog Creek 软件以及Google工作过。她也是《 Learning React Native 》一书的作者，《 Learning React Native 》是由 O'Reilly 出版的，介绍使用 JavaScript 来构建原生的 iOS 和 Android 应用的书籍。她也经常在一些研讨会上分享演讲，从 ReactJS，到 音乐编程，乃至 Arduinos。在空闲时间，她非常享受于学习新的语言，做一些硬件项目，用激光切割巧克力之类的。可以关注她的Twitter：@brindelle。

查看英文原文：[Writing Cross-Platform Apps with React Native](http://www.infoq.com/articles/react-native-introduction)
