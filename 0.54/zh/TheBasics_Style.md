---
id: version-0.54-style
title: 样式
original_id: style
---

在React-native 体系中，我们无需学习特殊的语言语法来定义样式，依旧只需使用 `JavaScript` 语法定义样式。所有的核心组件均能支持名为 `style` 的属性。这些样式名以及[定义值](colors.md) 与 `web` 页面上的 `CSS` 的命名保持一致，只是按照 `JavaScript` 的语法要求使用了驼峰命名法，例如将 `background-color` 改为`backgroundColor`。

`Style` 属性可以是一个普通的 `JavaScript对象`。这是最简单的用法，因此在示例代码中很常见。你也可以传入一个由样式组成的数组（越靠后的数组元素将拥有更高的优先级），这样我们就能实现的样式的继承。

在实际开发中，组件的样式会非常复杂，使用 `StyleSheet.create` 来集中定义组件的样式将使代码更加清晰。如下方的例子：
```jsx
import React, { Component } from 'react';
import { AppRegistry, StyleSheet, Text, View } from 'react-native';

export default class LotsOfStyles extends Component {
  render() {
    return (
      <View>
        <Text style={styles.red}>just red</Text>
        <Text style={styles.bigblue}>just bigblue</Text>
        <Text style={[styles.bigblue, styles.red]}>bigblue, then red</Text>
        <Text style={[styles.red, styles.bigblue]}>red, then bigblue</Text>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  bigblue: {
    color: 'blue',
    fontWeight: 'bold',
    fontSize: 30,
  },
  red: {
    color: 'red',
  },
});

// skip this line if using Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => LotsOfStyles);
```

常见的做法是按顺序声明和使用style属性，以借鉴CSS中的“层叠”做法（即后声明的属性会覆盖先声明的同名属性）。

文本的样式定义请参阅[Text组件](text.md)的文档。

现在你已经了解如何调整文本样式了，下面我们要学习的是如何控制[组件的尺寸](height-and-width.md)。