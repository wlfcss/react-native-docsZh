---
id: version-0.54-height-and-width
title: 高度与宽度
original_id: height-and-width
---

一个组件的宽高将决定骑在屏幕上的尺寸。

## 确定的尺寸

设置组件尺寸的最简单方法是在样式中指定固定的`width`和`height`。 `React-Native` 中的所有尺寸都是**无单位**的，并且表示的都是与设备密度无关的所谓 **逻辑像素点**。

``` jsx
import React, { Component } from 'react';
import { AppRegistry, View } from 'react-native';

export default class FixedDimensionsBasics extends Component {
  render() {
    return (
      <View>
        <View style={{width: 50, height: 50, backgroundColor: 'powderblue'}} />
        <View style={{width: 100, height: 100, backgroundColor: 'skyblue'}} />
        <View style={{width: 150, height: 150, backgroundColor: 'steelblue'}} />
      </View>
    );
  }
}

// skip this line if using Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => FixedDimensionsBasics);

```

无论在何种尺寸、密度的设备上，确定尺寸的组件都将在显示大小上保持一致。

## 弹性布局 （Flex Dimensions）

在组件样式中使用 `Flex` 可使组件根据可用空间动态扩展与收缩，通常我们会使用 `Flex: 1`以填充所有可用的空间，若有多个相同层级的组件flex值相同时，则会均分可用空间（可以类比于bootstrap中的栅格系统），若flex值不同，则flex值越大，所占空间越大。

> 组件能够使用空间的前提在于在其父组件定义中明确的宽高，比如定义了:`width` `height` 或是 `flex`,若父组件尺寸为0，子组件的`flex`属性将不会生效。

```jsx
import React, { Component } from 'react';
import { AppRegistry, View } from 'react-native';

export default class FlexDimensionsBasics extends Component {
  render() {
    return (
      // Try removing the `flex: 1` on the parent View.
      // The parent will not have dimensions, so the children can't expand.
      // What if you add `height: 300` instead of `flex: 1`?
      <View style={{flex: 1}}>
        <View style={{flex: 1, backgroundColor: 'powderblue'}} />
        <View style={{flex: 2, backgroundColor: 'skyblue'}} />
        <View style={{flex: 3, backgroundColor: 'steelblue'}} />
      </View>
    );
  }
}
```

当你熟练掌握了控制组件尺寸，下一步将学习[组件布局](flexbox.md)。