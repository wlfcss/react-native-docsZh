# Props - 属性
大多数的组件在被创建时会带有各种可定义的**参数**，这些参数被统一称之为 `props`（属性）。

举例来说，当我们使用React Native的基础组件 `Image` 创建一张图片时，你可以使用属性 `source` 来指定要显示图片的地址。
```jsx
import React, { Component } from 'react';
import { AppRegistry, Image } from 'react-native';

export default class Bananas extends Component {
  render() {
    let pic = {
      uri: 'https://upload.wikimedia.org/wikipedia/commons/d/de/Bananavarieties.jpg'
    };
    return (
      <Image source={pic} style={{width: 193, height: 110}}/>
    );
  }
}

// skip this line if using Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => Bananas);

```
*注：在ios系统上使用http链接指定图片地址时，由于ios系统的ATS安全限制，将会导致图片无法加载显示。详情请参考 [ios-ATS解决办法](https://segmentfault.com/a/1190000002933776).*

请注意在 `{pic}` 外围的花括号，当我们需要将一个合法的**变量**或是**表达式**嵌入JSX语句中时，需要加上花括号。

于自定义组件中亦可以使用 `props`。通过在不同的情况中使用不同的**属性**，可以达到有效的**组件复用**。只这一切只需在 `render` 函数中引入 `this.props` 。请参考下面的例子：
```jsx
import React, { Component } from 'react';
import { AppRegistry, Text, View } from 'react-native';

class Greeting extends Component {
  render() {
    return (
      <Text>Hello {this.props.name}!</Text>
    );
  }
}

export default class LotsOfGreetings extends Component {
  render() {
    return (
      <View style={{alignItems: 'center'}}>
        <Greeting name='Rexxar' />
        <Greeting name='Jaina' />
        <Greeting name='Valeera' />
      </View>
    );
  }
}

// skip this line if using Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => LotsOfGreetings);
```

在上方例子中定义的 `Greeting` 组件中将定制了一个属性 `name`，在需要多种 “问候语” 时就可以轻松做到组件复用。自定义组件 `Greeeting` 的实际使用体验与React native原生组件的体验完全一致，这使得个人开发者自定义私有UI框架变得异常轻松。

上面的例子出现了一个名为 `View` 的组件。`View` 常用作其他组件的容器，来帮助控制布局和样式。

仅仅使用props和基础的Text、Image以及View组件，就已经足以编写各式各样的UI组件了。如果要学习如何动态修改界面，那就需要进一步学习 `State`（状态）的概念。