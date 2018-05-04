---
id: version-0.54-state
title: 状态
original_id: state
---

我们使用 `props` 与 `state.props` 来控制一个组件，`props` 由父组件设定，且在组件的整个生命周期中不再改变。对于需要改变的数据，我们需要使用 `state` 。

通常情况下，我们在 `constructor` 中初始化 `state`,需要修改时调用方法 `setState`。

举例来说，当我们需要制作一段 **不断闪烁** 的文字，文本内容在创建之初已被指定与确认，那么文本内容应当是一个 `props` , 而控制文字闪烁的状态（文字在 **显示** 与 **隐藏** 两种状态中循环切换）则应该是随时间变化，那么这个状态控制应当写入 `state` 之中。
```jsx
import React, { Component } from 'react';
import { AppRegistry, Text, View } from 'react-native';

class Blink extends Component {
  constructor(props) {
    super(props);
    this.state = {isShowingText: true};

    // Toggle the state every second
    setInterval(() => {
      this.setState(previousState => {
        return { isShowingText: !previousState.isShowingText };
      });
    }, 1000);
  }

  render() {
    let display = this.state.isShowingText ? this.props.text : ' ';
    return (
      <Text>{display}</Text>
    );
  }
}

export default class BlinkApp extends Component {
  render() {
    return (
      <View>
        <Blink text='I love to blink' />
        <Blink text='Yes blinking is so great' />
        <Blink text='Why did they ever take this out of HTML' />
        <Blink text='Look at me look at me look at me' />
      </View>
    );
  }
}

// skip this line if using Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => BlinkApp);

```

在实际的开发项目中，我们一般不会在定时器函数（上方实例中的setInterval）中操作state。实际的应用场景一般是在接收到服务器返回的新数据，或者是用户输入的数据。在较为复杂的交互流程中，也可以使用像 [Redux](https://redux.js.org/) 这样的状态容器来控制数据流，在这种情况下，使用Redux来修改状态，而不是直接调用setState。（译者注：但我个人更见建议您使用mobx进行状态管理）。

当调用 `setState` 时，`BlinkApp` 将**重新渲染其组件**。 通过调用 `Timer` 中的 `setState`，该组件将在每次定时器滴答时重新呈现。

`State` 在 react-native 中的工作原理和 `React` 完全一致，所以对于处理 `state` 的一些更深入的细节，你可以参阅[React.Component API](https://reactjs.org/docs/react-component.html#setstate)。

看到这里，你可能觉得我们的例子总是千篇一律的黑色文本，这着实令人感到无趣。所以让我们一起来学习一下Style(样式)吧。