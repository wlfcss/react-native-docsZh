---
id: version-0.54-using-a-scrollview
title: 使用滚动视图
original_id: using-a-scrollview
---

[ScrollView](scrollview.md)是一个通用的可滚动容器，可以同时容纳多个组件与视图，而且这些组件可以是多种类型。同时你可以自由定义滚动方式：垂直滚动 / 水平滚动 （使用 `horizontal`属性）。

下面的代码展示了一个垂直滚动的`ScrollView`，其中包含了多个`images`与`text`组件：

```ReactNativeWebPlayer
import React, { Component } from 'react';
import { AppRegistry, ScrollView, Image, Text } from 'react-native';

export default class IScrolledDownAndWhatHappenedNextShockedMe extends Component {
  render() {
      return (
        <ScrollView>
          <Text style={{fontSize:96}}>Scroll me plz</Text>
          <Image source={require('/react-native/img/favicon.png')} />
          <Image source={require('/react-native/img/favicon.png')} />
          <Image source={require('/react-native/img/favicon.png')} />
          <Image source={require('/react-native/img/favicon.png')} />
          <Image source={require('/react-native/img/favicon.png')} />
          <Text style={{fontSize:96}}>If you like</Text>
          <Image source={require('/react-native/img/favicon.png')} />
          <Image source={require('/react-native/img/favicon.png')} />
          <Image source={require('/react-native/img/favicon.png')} />
          <Image source={require('/react-native/img/favicon.png')} />
          <Image source={require('/react-native/img/favicon.png')} />
          <Text style={{fontSize:96}}>Scrolling down</Text>
          <Image source={require('/react-native/img/favicon.png')} />
          <Image source={require('/react-native/img/favicon.png')} />
          <Image source={require('/react-native/img/favicon.png')} />
          <Image source={require('/react-native/img/favicon.png')} />
          <Image source={require('/react-native/img/favicon.png')} />
          <Text style={{fontSize:96}}>What's the best</Text>
          <Image source={require('/react-native/img/favicon.png')} />
          <Image source={require('/react-native/img/favicon.png')} />
          <Image source={require('/react-native/img/favicon.png')} />
          <Image source={require('/react-native/img/favicon.png')} />
          <Image source={require('/react-native/img/favicon.png')} />
          <Text style={{fontSize:96}}>Framework around?</Text>
          <Image source={require('/react-native/img/favicon.png')} />
          <Image source={require('/react-native/img/favicon.png')} />
          <Image source={require('/react-native/img/favicon.png')} />
          <Image source={require('/react-native/img/favicon.png')} />
          <Image source={require('/react-native/img/favicon.png')} />
          <Text style={{fontSize:80}}>React Native</Text>
        </ScrollView>
    );
  }
}

// skip these lines if using Create React Native App
AppRegistry.registerComponent(
  'AwesomeProject',
  () => IScrolledDownAndWhatHappenedNextShockedMe);
```

`ScrollViews` 可以通过 `pagingEnabled`属性配置为允许使用滑动手势浏览，在安卓平台上使用[ViewPagerAndroid](viewpagerandroid.md) 则可以实现页面间的切换滑动。

只用单个组件的`ScrollView`可用于允许用户缩放内容。 设置`maximumZoomScale`和`minimumZoomScale`属性，用户则可使用缩放手势进行组件的放大和缩小。

`ScrollView` 适用于展示少量的滚动元素，由于放置于`ScrollView`之中的组件在页面加载时都会被统一渲染，即使其内容过长被挤出到屏幕外（译者注：由于`ScrollView`的全渲染特性，在内容过长时会导致严重的性能问题），所以如果需要显示较长的滚动列表时，则应该使用功能基本一致而性能更好的[ListView组件](using-a-listview.md)。
