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

在一个组件的样式中指定 `justifyContent` 的值