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

