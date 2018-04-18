# 使用长列表视图组件

`React-Native`提供了多种适用于展示列表数据的组件，通常来说，你可以选用`FlatList`或`SectionList`。

`FlatList`组件适用于展示一个滚动列表，其中的元素应当保持**结构基本一致**而仅仅是数据不同。

`FlatList`组件设计之初就是用来展示长列表数据的，在生命周期中可以任意增减元素（增减元素并不会导致组件全部刷新），同时`FlatList`与`ScrollView`相比，差异在于其并不会渲染未被展示部分的数据。

`FlatList`组件需要两个配置属性(`props`)：`data` 和 `renderItem`。`data`用于接收存储元数据，`renderItem`则作为结构范例，用于逐个解析元数据并返回一个格式化组件供以渲染。

下面的例子创建了一个简单的`FlatList`，并预设了一些模拟数据。首先是初始化`FlatList`所需的`data`，其中的每一项（行）数据之后都在`renderItem`中被渲染成了`Text`组件，最后构成整个`FlatList`。

``` jsx
import React, { Component } from 'react';
import { AppRegistry, FlatList, StyleSheet, Text, View } from 'react-native';

export default class FlatListBasics extends Component {
  render() {
    return (
      <View style={styles.container}>
        <FlatList
          data={[
            {key: 'Devin'},
            {key: 'Jackson'},
            {key: 'James'},
            {key: 'Joel'},
            {key: 'John'},
            {key: 'Jillian'},
            {key: 'Jimmy'},
            {key: 'Julie'},
          ]}
          renderItem={({item}) => <Text style={styles.item}>{item.key}</Text>}
        />
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
   flex: 1,
   paddingTop: 22
  },
  item: {
    padding: 10,
    fontSize: 18,
    height: 44,
  },
})

// skip this line if using Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => FlatListBasics);
```

如果你希望将一组数据渲染为逻辑结构，比如类似于`ios`系统的`UITableViews`类的`section`的头部，那么`SectionList`将是一个不错的选择。

```jsx
import React, { Component } from 'react';
import { AppRegistry, SectionList, StyleSheet, Text, View } from 'react-native';

export default class SectionListBasics extends Component {
  render() {
    return (
      <View style={styles.container}>
        <SectionList
          sections={[
            {title: 'D', data: ['Devin']},
            {title: 'J', data: ['Jackson', 'James', 'Jillian', 'Jimmy', 'Joel', 'John', 'Julie']},
          ]}
          renderItem={({item}) => <Text style={styles.item}>{item}</Text>}
          renderSectionHeader={({section}) => <Text style={styles.sectionHeader}>{section.title}</Text>}
          keyExtractor={(item, index) => index}
        />
      </View>
    );
  }
}

```

列表组件通常会用于展示从服务端拉取的数据，要实现这一过程，您需要学习网络章节。