---
id: version-0.54-navigation
title: 导航器跳转页面
original_id: navigation
---


移动端应用程序通常不会只有一个屏幕（页面），管理多个屏幕（页面）的呈现和跳转通常由称为导航器的处理来处理。

本文档涵盖了React-Native之中各种常见的导航组件。如果您刚刚接触导航组件，不如选择[React Navigation](navigation.md#react-navigation)进行学习。React Navigation提供了一个易于使用的导航解决方案，能够在iOS和Android上呈现常见堆栈导航和选项卡式导航。 由于其是由JavaScript实现的，它在与诸如[redux](https://reactnavigation.org/docs/redux-integration.html)等状态管理库进行集成时有着很好的可配置性和灵活性。

如果您只针对iOS进行开发，那么您可以使用[NavigatorIOS](navigation.md#navigatorios)导航组件，因为它提供了ios原生`UINavigationController`类的包装(译者注：与iOS系统原生外观一致)。但是，该组件无法在Android上运行。


如果您希望在iOS和Android上实现原生的外观和体验，或者将React-Native集成到原生开发的应用中，以下的两个库都能支持这种需求：[native-navigation](http://airbnb.io/native-navigation/), [react-native-navigation](https://github.com/wix/react-native-navigation)。

## React Navigation

社区今后主推的方案是一个单独的导航库`react-navigation`，它的使用十分简单。

首先在你的应用程序中安装此组件：

```
npm install --save react-navigation
```

接下来你就可以快速创建一个有两个页面（Home和Profile）的应用了：

```
import {
  StackNavigator,
} from 'react-navigation';

const App = StackNavigator({
  Home: { screen: HomeScreen },
  Profile: { screen: ProfileScreen },
});
```

每一个`screen`组件都可以单独设置导航选项，例如导航头的标题。还可以使用`navigation`属性中的方法去跳转到别的页面：

```
class HomeScreen extends React.Component {
  static navigationOptions = {
    title: 'Welcome',
  };
  render() {
    const { navigate } = this.props.navigation;
    return (
      <Button
        title="Go to Jane's profile"
        onPress={() =>
          navigate('Profile', { name: 'Jane' })
        }
      />
    );
  }
}
```

`React Navigation`的路由写法使其非常容易扩展导航逻辑，或是整合到`redux`中。由于路由可以嵌套使用，因而开发者可以根据不同页面编写不同的导航逻辑，且彼此互不影响。

`React Navigation`中的视图是原生组件，同时用到了运行在原生线程上的 [`Animated`](animated.md) 动画库，因而性能表现十分流畅。此外其动画形式和手势都非常便于定制。

有关`React Navigation`的完整介绍，请按照[React Navigation Getting Started Guide](https://reactnavigation.org/docs/getting-started.html)或浏览其他文档，例如`Navigator`的[Intro to Navigators](https://expo.io/@react-navigation/NavigationPlayground)。

## NavigatorIOS

`NavigatorIOS` 的外观和体验与[`UINavigationController`](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UINavigationController_Class/)非常相似，因为`NavigatorIOS`实际上是建立在它之上的。

![](images/NavigationStack-NavigatorIOS.gif)

``` javascript
<NavigatorIOS
  initialRoute={{
    component: MyScene,
    title: 'My Initial Scene',
    passProps: {myProp: 'foo'},
  }}
/>
```

与其他导航组件一样，`NavigatorIOS` 也使用路由对象来描述场景，但有一些重要的区别。 其中要渲染的组件在路由对象的component字段中指定，要给目标组件传递的参数则写在passProps中。被渲染的component都会自动接受到一个名为navigator的属性，你可以直接调用此对象(this.props.navigator)的`push` 和 `pop`方法。

由于 `NavigatorIOS` 使用的是原生的UIKit导航，所以它会自动渲染一个带有返回按钮和标题的导航栏。

```javascript
import React from 'react';
import PropTypes from 'prop-types';
import {Button, NavigatorIOS, Text, View} from 'react-native';

export default class NavigatorIOSApp extends React.Component {
  render() {
    return (
      <NavigatorIOS
        initialRoute={{
          component: MyScene,
          title: 'My Initial Scene',
          passProps: {index: 1},
        }}
        style={{flex: 1}}
      />
    );
  }
}

class MyScene extends React.Component {
  static propTypes = {
    route: PropTypes.shape({
      title: PropTypes.string.isRequired,
    }),
    navigator: PropTypes.object.isRequired,
  };

  constructor(props, context) {
    super(props, context);
    this._onForward = this._onForward.bind(this);
  }

  _onForward() {
    let nextIndex = ++this.props.index;
    this.props.navigator.push({
      component: MyScene,
      title: 'Scene ' + nextIndex,
      passProps: {index: nextIndex},
    });
  }

  render() {
    return (
      <View>
        <Text>Current Scene: {this.props.title}</Text>
        <Button
          onPress={this._onForward}
          title="Tap me to load the next scene"
        />
      </View>
    );
  }
}
```

查阅[`NavigatorIOS`相关文档](navigatorios.md)