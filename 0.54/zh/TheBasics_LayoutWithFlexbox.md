# Layout with Flexbox - 使用Flexbox布局

`React-native` 的组件可使用flexbox算法来指定其子级的布局。 Flexbox旨在为使用不同屏幕尺寸设备的用户提供一致的布局。

一般情况下，你仅需使用`flexDirection`、`alignItems`、`justifyContent`就可以完成基本的布局排版。

> `React-Naitve` 中 `FlexBox` 的工作原理与 Web上的CSS基本相同，只存在少许差异：默认值不同。例：`flexDirection` 的默认值是`column` 而不是 `row`，而`flex`也只能指定一个数字值。

## Flex Direction

在一个组件的样式中指定 `flexDirection` 的值将决定其布局的主轴方向（水平/纵向），子元素（组件）的排列方向究竟是水平（`row`）或者纵向垂直（`column`）？默认值为`column`。

```jsx
import React, { Component } from 'react';
import { AppRegistry, View } from 'react-native';
export default class FlexDirectionBasics extends Component {
  render() {
    return (
      // Try setting `flexDirection` to `column`.
      <View style={{flex: 1, flexDirection: 'row'}}>
        <View style={{width: 50, height: 50, backgroundColor: 'powderblue'}} />
        <View style={{width: 50, height: 50, backgroundColor: 'skyblue'}} />
        <View style={{width: 50, height: 50, backgroundColor: 'steelblue'}} />
      </View>
    );
  }
};

// skip this line if using Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => FlexDirectionBasics);
```

## justify Content

在一个组件样式中指定 `justifyContent` 的值可以决定其子元素沿着主轴的排列方式。子元素是应该靠近主轴的起始端还是末尾段分布呢？亦或应该均匀分布？对应的这些可选项有：`flex-start`、`center`、`flex-end`、`space-around`以及`space-between`。

```jsx

import React, { Component } from 'react';
import { AppRegistry, View } from 'react-native';

export default class JustifyContentBasics extends Component {
  render() {
    return (
      // Try setting `justifyContent` to `center`.
      // Try setting `flexDirection` to `row`.
      <View style={{
        flex: 1,
        flexDirection: 'column',
        justifyContent: 'space-between',
      }}>
        <View style={{width: 50, height: 50, backgroundColor: 'powderblue'}} />
        <View style={{width: 50, height: 50, backgroundColor: 'skyblue'}} />
        <View style={{width: 50, height: 50, backgroundColor: 'steelblue'}} />
      </View>
    );
  }
};

// skip this line if using Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => JustifyContentBasics);

```

## Align Items

在组件的`style`中指定`alignItems`可以决定其子元素沿着次轴（与主轴垂直的轴，比如若主轴方向为row，则次轴方向为column）的排列方式。子元素是应该靠近次轴的起始端还是末尾段分布呢？亦或应该均匀分布？对应的这些可选项有：`flex-start`、`center`、`flex-end`以及`stretch`。

> 注意：要使stretch选项生效的话，子元素在次轴方向上不能有固定的尺寸。以下面的代码为例：只有将子元素样式中的width: 50去掉之后，alignItems: 'stretch'才能生效。

```jsx
import React, { Component } from 'react';
import { AppRegistry, View } from 'react-native';

export default class AlignItemsBasics extends Component {
  render() {
    return (
      // Try setting `alignItems` to 'flex-start'
      // Try setting `justifyContent` to `flex-end`.
      // Try setting `flexDirection` to `row`.
      <View style={{
        flex: 1,
        flexDirection: 'column',
        justifyContent: 'center',
        alignItems: 'center',
      }}>
        <View style={{width: 50, height: 50, backgroundColor: 'powderblue'}} />
        <View style={{width: 50, height: 50, backgroundColor: 'skyblue'}} />
        <View style={{width: 50, height: 50, backgroundColor: 'steelblue'}} />
      </View>
    );
  }
};

// skip this line if using Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => AlignItemsBasics);
```

## 深入学习

我们已经介绍了布局的基本知识，但还有许多其他样式和属性。 [这里](https://facebook.github.io/react-native/docs/0.54/layout-props.html)记录了控制布局的属性的完整列表。

我们正学习如何够建立一个真正的应用程序。 但我们仍然缺少一种获取用户输入的方式。因此，让我们继续学习如何使用TextInput组件处理文本输入。