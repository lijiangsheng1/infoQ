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



### 它是真正的原生

![unknown](http://cdn.infoq.com/statics_s2_20160217-0123u3/resource/articles/react-native-introduction/en/resources/21.jpg)

### 更好的开发者体验

![brower debug tool](http://cdn.infoq.com/statics_s2_20160217-0123u3/resource/articles/react-native-introduction/en/resources/52.jpg)


## 掌控多平台

## 使用 React Native

### 上手入门

### 常见 React 组件


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


## 样式表

```
var styles = StyleSheet.create({
  container: {
    flex: 1,
    marginTop: 30
  }
});
```

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

## 关于作者
![Image of author 1](http://cdn.infoq.com/statics_s2_20160217-0123u3/resource/articles/react-native-introduction/en/resources/bonnie.jpg)Bonnie Eisenman 是来自Twitter的工程师，她是 NYC Resistor 黑客空间的成员之一，之前在Codecademy、Fog Creek 软件以及Google工作过。她也是《 Learning React Native 》一书的作者，《 Learning React Native 》是由 O'Reilly 出版的，介绍使用 JavaScript 来构建原生的 iOS 和 Android 应用的书籍。她也经常在一些研讨会上分享演讲，从 ReactJS，到 音乐编程，乃至 Arduinos。在空闲时间，她非常享受于学习新的语言，做一些硬件项目，用激光切割巧克力之类的。可以关注她的Twitter：@brindelle。

查看英文原文：[Writing Cross-Platform Apps with React Native](http://www.infoq.com/articles/react-native-introduction)
