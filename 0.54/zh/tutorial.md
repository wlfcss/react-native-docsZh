---
id: version-0.54-tutorial
title: 基础学习
original_id: tutorial
---

React Native与React类似，但它使用原生组件而不是Web组件。 因此，要了解React Native程序的基本结构，您需要了解一些基本的React概念，比如JSX，组件，`state(状态)`和`props(属性)`。即使你已经了解过React，但仍然需要学习一些React-Native特有的东西，比如原生组件。 本教程针对所有开发者，无论您是否具有React经验。

让我们开始吧！

## Hello World

根据程序员的古老传统，在最开始的时候我们需要构建一个除了输出 “Hello World” 之外啥也干不了的简单程序，如下所示：

```ReactNativeWebPlayer
import React, { Component } from 'react';
import { Text } from 'react-native';

export default class HelloWorldApp extends Component {
  render() {
    return (
      <Text>Hello world!</Text>
    );
  }
}
```

如果您感到好奇，可以直接在网页模拟器中运行示例代码。 当然你也可以将代码段拷贝至你的`App.js`文件中，在你的物理机上创建一个本地应用程序。

## 接下来呢？

你可能觉着上面的示例与通常的Javascript并不相同，不要紧张，_这是未来。_

首先，ES2015（也被称为ES6）是对JavaScript的一系列改进，目前它已成为官方标准的一部分，但尚未被所有浏览器支持，所以它并未在Web开发中推广开来。 React Native提供ES2015支持，因此您可以放心使用。 在上面的例子中，`import`, `from`, `class`, `extends` 和 `() =>` 语法都是ES2015的特性。 如果您对ES2015不熟悉，您可以通过阅读本教程中的示例代码来熟悉使用。 如果你愿意，这个[页面](https://babeljs.io/learn-es2015/)很好的介绍了ES2015的功能。

这个代码示例中的另一个不寻常的东西是 `<Text> Hello world！</ Text>`。 这是JSX - 一种在JavaScript中嵌入XML的语法。 许多框架使用特殊的模板语言，可让您将代码嵌入标记语言中。 在React中，这是相反的。 JSX允许您在代码中编写标记语言。 它看起来像Web上的HTML，除了使用React组件之外的其他网络事物（例如 `<div>` 或 `<span>` ）。 在这种情况下，`<Text>` 是一个内置组件，只显示一些文本。

## 组件

上面的代码定义了一个名为 `HelloWorldApp` 的新的组件`Component`。你在编写React Native应用时，肯定会写出很多新的组件。而一个App的最终界面，其实也就是各式各样的组件的组合。组件本身结构可以非常简单 —— 唯一必须的就是在 `render` 方法中返回一些用于渲染结构的JSX语句。

## 这个APP太简陋了！

是的，如果你想编写一些更有趣更高级的东西，请前往 [Props 章节](props.md)进行学习.
