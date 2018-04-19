# Handing Text Input - 文本输入处理

`TextInput`是一个允许用户输入文本的基本组件。 它有一个`onChangeText`道具，它在每次文本改变时都会调用一个函数，而`onSubmitEditing`道具在提交文本时会调用一个函数。

假如我们要实现当用户输入时，实时将其以单词为单位翻译为另一种文字。我们假设这种文字来一个美食自星球，只有一个单词： 🍕。所以"Hello there Bob"将会被翻译为"🍕🍕🍕"。

```jsx
import React, { Component } from 'react';
import { AppRegistry, Text, TextInput, View } from 'react-native';

export default class PizzaTranslator extends Component {
  constructor(props) {
    super(props);
    this.state = {text: ''};
  }

  render() {
    return (
      <View style={{padding: 10}}>
        <TextInput
          style={{height: 40}}
          placeholder="Type here to translate!"
          onChangeText={(text) => this.setState({text})}
        />
        <Text style={{padding: 10, fontSize: 42}}>
          {this.state.text.split(' ').map((word) => word && 'đ').join(' ')}
        </Text>
      </View>
    );
  }
}

// skip this line if using Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => PizzaTranslator);
```

在上面的例子里，我们把`text`保存到`state`中，因为它会随着时间变化。

文本输入方面还有很多其他的东西要处理。比如你可能想要在用户输入的时候进行验证，在`React`的表单组件中的受限组件一节中有一些详细的示例（注意`react`中的`onChange`对应的是`react-native`中的`onChangeText`）。此外你还需要看看TextInput的文档。

文本输入是用户与应用交互的方式之一。 接下来，让我们看看另一种输入类型，并学习如何处理触摸。