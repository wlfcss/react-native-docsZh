# Handing Touchs - 触控处理

用户通过触摸操作与手机App进行交互操作。他们能使用手势组合，比如触摸按钮、滚动列表或是在地图上缩放视角。`React-native`提供了大量的组件来处理各式各样的操作手势，以及一个**全面的手势响应系统**，以便用户进行更高级的手势识别，但是现在，你可能最感兴趣的组件是`Button`。

## 显示一个基本按钮

`Button`提供了一个基础的按钮组件库，它们能很好的运行于各种平台上。以最精简的方式来显示一个按钮如下所示：

```jsx
<Button
  onPress={() => {
    Alert.alert('You tapped the button!');
  }}
  title="Press Me"
/>
```

下面的例子将在iOS上呈现蓝色标签，并在Android上呈现蓝色圆角矩形，并显示白色文字。 按下按钮将会调用 `onPress` 功能，在这种情况下会显示一个警报弹出窗口。 如果你喜欢，你可以指定一个 color 的属性来改变按钮的颜色。

 ![](./images/handingTouchs_Button.png)

 > Go ahead and play around with the Button component using the example below. You can select which platform your app is previewed in by clicking on the toggle in the bottom right, then click on "Tap to Play" to preview the app.

 ```jsx
 import React, { Component } from 'react';
import { Alert, AppRegistry, Button, StyleSheet, View } from 'react-native';

export default class ButtonBasics extends Component {
  _onPressButton() {
    Alert.alert('You tapped the button!')
  }

  render() {
    return (
      <View style={styles.container}>
        <View style={styles.buttonContainer}>
          <Button
            onPress={this._onPressButton}
            title="Press Me"
          />
        </View>
        <View style={styles.buttonContainer}>
          <Button
            onPress={this._onPressButton}
            title="Press Me"
            color="#841584"
          />
        </View>
        <View style={styles.alternativeLayoutButtonContainer}>
          <Button
            onPress={this._onPressButton}
            title="This looks great!"
          />
          <Button
            onPress={this._onPressButton}
            title="OK!"
            color="#841584"
          />
        </View>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
   flex: 1,
   justifyContent: 'center',
  },
  buttonContainer: {
    margin: 20
  },
  alternativeLayoutButtonContainer: {
    margin: 20,
    flexDirection: 'row',
    justifyContent: 'space-between'
  }
})

// skip this line if using Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => ButtonBasics);

 ```

## Touchables 

如果基本按钮`button`看起来并不适用于您的应用，则可以使用`R1eact-Native`提供的`Touchables`组件来构建自己的按钮。而`Touchables`仅仅提供了捕捉**敲击手势** 的功能，并且与`button`一致，均提供`onPress`等回调函数的能力。但`Touchables`组件并不会带有任何默认的样式，所以你需要自行定义样式让其在你的应用中更加好看。

你可以根据你想提供的交互模式来选择下列多种`Touchable`组件。

- 通常情况下，你可以在任何地方使用 [**TouchableHighlight**](touchablehighlight.md),一个按钮或是一个超链接，当用户按下按钮时，按钮的背景色将会变暗。

- 你可以考虑在安卓上使用 [**TouchableNativeFeedback**](touchablenativefeedback.md)(仅用于Android)来显示安卓系统反馈用户触摸的水波纹效果。

- [**TouchableOpacity**](touchableopacity.md)在按钮按下时通过减少按钮背景的透明度来提供视觉反馈。

- 如果你需要控制处理轻按手势，但不想有任何视觉反馈，请使用[**TouchableWithoutFeedback**](touchablewithoutfeedback.md)

在某些情况下，您可能需要检测用户按下并保持一定时间的情况。 这些长时间按压可以通过各种`Touchables`组件的 onLongPress 函数来处理。

如下所示：

``` jsx
import React, { Component } from 'react';
import { Alert, AppRegistry, Platform, StyleSheet, Text, TouchableHighlight, TouchableOpacity, TouchableNativeFeedback, TouchableWithoutFeedback, View } from 'react-native';

export default class Touchables extends Component {
  _onPressButton() {
    Alert.alert('You tapped the button!')
  }

  _onLongPressButton() {
    Alert.alert('You long-pressed the button!')
  }


  render() {
    return (
      <View style={styles.container}>
        <TouchableHighlight onPress={this._onPressButton} underlayColor="white">
          <View style={styles.button}>
            <Text style={styles.buttonText}>TouchableHighlight</Text>
          </View>
        </TouchableHighlight>
        <TouchableOpacity onPress={this._onPressButton}>
          <View style={styles.button}>
            <Text style={styles.buttonText}>TouchableOpacity</Text>
          </View>
        </TouchableOpacity>
        <TouchableNativeFeedback
            onPress={this._onPressButton}
            background={Platform.OS === 'android' ? TouchableNativeFeedback.SelectableBackground() : ''}>
          <View style={styles.button}>
            <Text style={styles.buttonText}>TouchableNativeFeedback</Text>
          </View>
        </TouchableNativeFeedback>
        <TouchableWithoutFeedback
            onPress={this._onPressButton}
            >
          <View style={styles.button}>
            <Text style={styles.buttonText}>TouchableWithoutFeedback</Text>
          </View>
        </TouchableWithoutFeedback>
        <TouchableHighlight onPress={this._onPressButton} onLongPress={this._onLongPressButton} underlayColor="white">
          <View style={styles.button}>
            <Text style={styles.buttonText}>Touchable with Long Press</Text>
          </View>
        </TouchableHighlight>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    paddingTop: 60,
    alignItems: 'center'
  },
  button: {
    marginBottom: 30,
    width: 260,
    alignItems: 'center',
    backgroundColor: '#2196F3'
  },
  buttonText: {
    padding: 20,
    color: 'white'
  }
})

// skip this line if using Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => Touchables);
```

## 滚动列表，滑动页面和双指缩放

移动应用中常用的另一个手势是滑动或平移。 该手势允许用户滚动浏览项目列表，或者滑过内容页面。 为了处理这些和其他手势，我们将学习如何使用ScrollView。