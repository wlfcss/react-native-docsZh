---
id: version-0.54-animations
title: 图像
original_id: animations
---

动画对于营造良好的用户体验有着极重要的作用。在现实生活中的物体都具有一个名为“惯性”的属性，我们在移动端App界面上亦可以使用此种遵循物理规律的交互体验。

`React Native`提供了两种完善的动画系统：[`Animated`](animations.md#animated-api)是小粒度的和基本的交互控制的动画库;[`LayoutAnimation`](animations.md#layoutanimation-api)则是控制布局排版的动画库。

## `Animated` API

[`Animated`](animated.md)库的设计思想是使开发者能极为简便的实现各种高性能的动画和交互。`Animated`侧重于以声明的形式定义动画的输入和输出，并在两者之间设定可配置的变化函数，使用 `start`/`stop` 方法来控制动画执行的时间顺序。

`Animated` 仅仅封装了四种基本组件：`View`, `Text`, `Image`, 以及 `ScrollView`，当然你也可以使用 `Animated.createAnimatedComponent` 封装属于你自己的组件。

一个在加载时有淡入淡出效果的组件，如下所示：

```SnackPlayer
import React from 'react';
import { Animated, Text, View } from 'react-native';

class FadeInView extends React.Component {
  state = {
    fadeAnim: new Animated.Value(0),  // Initial value for opacity: 0
  }

  componentDidMount() {
    Animated.timing(                  // Animate over time
      this.state.fadeAnim,            // The animated value to drive
      {
        toValue: 1,                   // Animate to opacity: 1 (opaque)
        duration: 10000,              // Make it take a while
      }
    ).start();                        // Starts the animation
  }

  render() {
    let { fadeAnim } = this.state;

    return (
      <Animated.View                 // Special animatable View
        style={{
          ...this.props.style,
          opacity: fadeAnim,         // Bind opacity to animated value
        }}
      >
        {this.props.children}
      </Animated.View>
    );
  }
}

// You can then use your `FadeInView` in place of a `View` in your components:
export default class App extends React.Component {
  render() {
    return (
      <View style={{flex: 1, alignItems: 'center', justifyContent: 'center'}}>
        <FadeInView style={{width: 250, height: 50, backgroundColor: 'powderblue'}}>
          <Text style={{fontSize: 28, textAlign: 'center', margin: 10}}>Fading in</Text>
        </FadeInView>
      </View>
    )
  }
}
```

让我们来分析一下，在 `FadeInView` 的构造函数中，声明了一个名为`fadeAnim`的新`Animated.Value`，并放置于 `state` 之中。同时我们将`View`的透明度与其绑定。

当组件(component)加载时，初始透明度设置为0。接下来，启动与`fadeAnim`值绑定的动画函数，该值将在每帧上更新其所有依赖的映射（透明度），最终该透明度数值由0变为1。

上面的例子是一种经过优化的方案，比直接调用`setState`重新渲染要快。由于整个配置事先已经过声明，我们能够实现进一步的优化，动画在序列化配置的同时能在高优先级的线程上运行。

### 动画配置

`Animated` 拥有非常灵活的配置项，自定义和预定义的渐变(easing)函数，延迟，持续时间，衰减因子，弹簧常数等都可以根据动画的类型进行调整。

`Animated` 提供了多种动画类型，其中最常用的则是[`Animated.timing()`](animated.md#timing)。它支持使用各种预定义的方法：比如渐变函数：随着时间推移改变绑定值，或者你也可以使用自定义函数。渐变函数则通常用于需要逐渐加速活减速的图形动画。

默认情况下，`timing` 将使用`easeInOut`曲线，该曲线将逐步加速传递到全速，并通过逐渐减速停止结束。 您可以通过传递一个`easing`参数来指定一个不同的渐变函数。 自定义持续时间或动画开始之前的延迟也支持。

（举例来说，如果我们希望创建一个时长为2s的动画：在其移动到最终位置前进行一个备份？）
For example, if we want to create a 2-second long animation of an object that slightly backs up before moving to its final position:

```javascript
Animated.timing(this.state.xPosition, {
  toValue: 100,
  easing: Easing.back(),
  duration: 2000,
}).start();
```

查看[Configuring animations](animated.md#configuring-animations)的动画配置部分，了解有关内置动画配置参数的更多信息。

### 组合动画

动画可以组合并按顺序或并行播放。 连续动画可以在上一个动画结束后立即播放，或者可以在指定的延迟后开始。 `Animated API` 提供了多种方法，比如 `顺序执行 sequence()` 和 `延时执行 delay()` ，每个方法只需要一组动画来执行，并根据需要自动调用 `start()` / `stop()`。

在下面的例子里，当动画元素运动停止后，进行旋转并返回：

```javascript
Animated.sequence([
  // decay, then spring to start and twirl
  Animated.decay(position, {
    // coast to a stop
    velocity: {x: gestureState.vx, y: gestureState.vy}, // velocity from gesture release
    deceleration: 0.997,
  }),
  Animated.parallel([
    // after decay, in parallel:
    Animated.spring(position, {
      toValue: {x: 0, y: 0}, // return to start
    }),
    Animated.timing(twirl, {
      // and twirl
      toValue: 360,
    }),
  ]),
]).start(); // start the sequence group
```

通常来说，如果任何一个动画被停止或中断了，组内所有其它的动画也会被停止。Parallel有一个stopTogether属性，如果设置为false，可以禁用自动停止。

你可以在[Composing animations](animated.md#composing-animations)中找到动画api合成方法的完整解释。

### 组合动画

您可以通过添加，乘法，除法或模数来 [组合两个动画](animated.md#combining-animated-values)，以创建新的动画。

在某些情况中，动画值需要反转另一个动画值以进行计算。 在下面的例子中是反转比例（2x - > 0.5x）：

```javascript
const a = new Animated.Value(1);
const b = Animated.divide(1, a);

Animated.spring(a, {
  toValue: 2,
}).start();
```

### 插值

每个属性都可以先通过插值运行。 插值将输入区间映射到输出区间，通常来说会使用线性插值，但也支持渐变功能(`easing functions`)。 默认情况下，它会将曲线外推到给定的范围之外，但您也可以使曲线限制输出值。

下面有一个一个简单的从 0-1区间 到 0-100区间 的映射示例：

```javascript
value.interpolate({
  inputRange: [0, 1],
  outputRange: [0, 100],
});
```

通常来说，你可能想
例如，您可能想要将 `Animated.Value` 变化视为从 0 到 1，但其位置从 150px 变为 0px，不透明度从 0 变为 1.这可以通过修改上述示例的 `style` 轻松完成 ：

```javascript
  style={{
    opacity: this.state.fadeAnim, // Binds directly
    transform: [{
      translateY: this.state.fadeAnim.interpolate({
        inputRange: [0, 1],
        outputRange: [150, 0]  // 0 : 150, 0.5 : 75, 1 : 0
      }),
    }],
  }}
```

[`interpolate()`](animated.md#interpolate)支持多种区间设置，一般用作定义静止区间。举例来说，要设计输入在等于-300时取相反值，在输入等于-100时取0,接下来在输入等于0时又增长到1,接着一直到输入到100的过程中逐步回到0，最后形成一个始终为0的静止区间，对于任何大于100的输入都返回0。其具体写法如下：

```javascript
value.interpolate({
  inputRange: [-300, -100, 0, 100, 101],
  outputRange: [300, 0, 1, 0, 0],
});
```

则其最终的映射结果如下：

```
Input | Output
------|-------
  -400|    450
  -300|    300
  -200|    150
  -100|      0
   -50|    0.5
     0|      1
    50|    0.5
   100|      0
   101|      0
   200|      0
```

`interpolate()` 亦支持映射字符串，从而可以实现颜色和带有单位数值的动画变换，如下所示：

```javascript
value.interpolate({
  inputRange: [0, 360],
  outputRange: ['0deg', '360deg'],
});
```

`interpolate()` 支持任意的渐变函数，其中许多函数已经在 [`Easing`](easing.md) 模块中进行了定义(译者注：包括二次、贝塞尔等曲线)。`interpolate()` 还支持限制输出区间 `outputRange`。你可以通过设置 `extrapolate`, `extrapolateLeft` 或是`extrapolateRight` 等参数来限制输出区间。其默认值为`extend`(默认允许超出)，你也可以使用 `clamp` 参数来禁止输出值超过 `outputRange`。

### 跟踪动态值

动画中所设的值还可以通过跟踪别的值得到。你只要把 `toValue` 设置成另一个动态值而不是一个普通数字即可。比如我们可以用弹跳动画来实现聊天头像的闪动，又比如通过 `timing` 设置 `duration:0` 来实现快速的跟随。还可以使用插值来进行组合：

```javascript
Animated.spring(follower, {toValue: leader}).start();
Animated.timing(opacity, {
  toValue: pan.x.interpolate({
    inputRange: [0, 300],
    outputRange: [1, 0],
  }),
}).start();
```

`leader` 和 `follower` 动画将使用 `Animated.ValueXY()` 来实现。 `ValueXY` 是一个能方便处理2D交互的方式，比如旋转或是拖拽，这是一个包含了两种 `Animated.Value` 实例的包装器，提供了大量的辅助函数，这使得 `ValueXY` 在很多时候都可以替代 `Value` 使用。比如在上方的示例中，当 `leader` 和 `follower` 均为 `ValueXY` 类型是，x 与 y 值都能被跟踪。

### 手势跟踪

Animated.event是Animated API中与输入有关的部分，允许手势或其它事件直接绑定到动态值上。它通过一个结构化的映射语法来完成，使得复杂事件对象中的值可以被正确的解开。第一层是一个数组，允许同时映射多个值，然后数组的每一个元素是一个嵌套的对象。在下面的例子里，你可以发现scrollX被映射到了event.nativeEvent.contentOffset.x(event通常是回调函数的第一个参数)，并且pan.x和pan.y分别映射到gestureState.dx和gestureState.dy（gestureState是传递给PanResponder回调函数的第二个参数）。

Gestures, like panning or scrolling, and other events can map directly to animated values using [`Animated.event`](animated.md#event). This is done with a structured map syntax so that values can be extracted from complex event objects. The first level is an array to allow mapping across multiple args, and that array contains nested objects.

手势，比如平移或滚动，以及其他事件可以使用[`Animated.event`](animated.md#event)直接映射到动画值。 这是通过结构化的映射语法完成的，以便可以从复杂的事件对象中提取值。第一层是一个数组，允许同时映射多个值，然后数组的每一个元素是一个嵌套的对象

For example, when working with horizontal scrolling gestures, you would do the following in order to map `event.nativeEvent.contentOffset.x` to `scrollX` (an `Animated.Value`):

在下面的例子里，你可以发现 `scrollX` 被映射到了 `event.nativeEvent.contentOffset.x`(`event` 通常是回调函数的第一个参数)。

```javascript
 onScroll={Animated.event(
   // scrollX = e.nativeEvent.contentOffset.x
   [{ nativeEvent: {
        contentOffset: {
          x: scrollX
        }
      }
    }]
 )}
```

使用 `PanResponder` 时，可以使用以下代码从 `gestureState.dx` 和 `gestureState.dy` 中提取x和y位置。 我们在数组的第一个位置使用null，因为我们只关心传递给 `PanResponder` 处理程序(即 `gestureState`)的第二个参数。

```javascript
onPanResponderMove={Animated.event(
  [null, // ignore the native event
  // extract dx and dy from gestureState
  // like 'pan.x = gestureState.dx, pan.y = gestureState.dy'
  {dx: pan.x, dy: pan.y}
])}
```

### 响应当前的动画值

你可能会注意到这里没有一个明显的方法来在动画的过程中读取当前的值 —— 这是出于优化的角度考虑，有些值只有在原生代码运行阶段中才知道。如果你需要在JavaScript中响应当前的值，有两种可能的办法：

* `spring.stopAnimation(callback)` 会停止动画并且把最终的值作为参数传递给回调函数`callback` ——这在处理手势动画的时候非常有用。
* `spring.addListener(callback)`会在动画的执行过程中持续异步调用 `callback` 回调函数，提供一个最近的值作为参数。这在用于触发状态切换的时候非常有用，譬如当用户拖拽一个东西靠近的时候弹出一个新的气泡选项。不过这个状态切换可能并不会十分灵敏，因为它不像许多连续手势操作（如旋转）那样在60fps下运行。

`Animated` 被设计为可以完全序列化，以保证其拥有高效率的性能，且独立于普通的js事件循环，这极大的影响了相关API的设计，所以请记住一点，当你感到非常棘手时，请查阅 `Animated.Value.addListener`,及时其作为一种有诸多限制与警告的方法，请谨慎使用（这对性能将造成极大的影响）。 
 
### 使用原生驱动动画

`Animated(动画)` 的API可转化为字符串表达以便通信或存储（可序列化）。通过使用 [native driver](http://facebook.github.io/react-native/blog/2017/02/14/using-native-driver-for-animated.html)，我们在启动动画前就把其所有配置信息都发送到原生端，利用原生代码在UI线程执行动画，而不用每一帧都在两端间来回沟通。 如此一来，动画一开始就完全脱离了JS线程，因此此时即便JS线程被卡住，也不会影响到动画。

在动画中启用原生驱动非常简单。 只需在开始动画之前，在动画配置中加入一行`useNativeDriver: true`，如下所示：

```javascript
Animated.timing(this.state.animatedValue, {
  toValue: 1,
  duration: 500,
  useNativeDriver: true, // <-- Add this
}).start();
```

动画值在不同的驱动方式之间是不能兼容的。因此如果你在某个动画中启用了原生驱动，那么所有和此动画依赖相同动画值的其他动画也必须启用原生驱动。

原生驱动还可以在 `Animated.event` 中使用。由于 React Native 的异步特性，这对于没有原生驱动的页面滚动后的动画特别有效，因为动画将始终运行于手势线程以外。

```javascript
<Animated.ScrollView // <-- Use the Animated ScrollView wrapper
  scrollEventThrottle={1} // <-- Use 1 here to make sure no events are ever missed
  onScroll={Animated.event(
    [
      {
        nativeEvent: {
          contentOffset: {y: this.state.animatedValue},
        },
      },
    ],
    {useNativeDriver: true} // <-- Add this
  )}>
  {content}
</Animated.ScrollView>
```

您可以通过运行[RNTester app](https://github.com/facebook/react-native/blob/master/RNTester/) 应用程序来熟悉原生驱动加载本地动画示例。 您也可以查看[源代码](https://github.com/facebook/react-native/blob/master/RNTester/js/NativeAnimationsExample.js)以了解这些示例的制作方式。

#### 注意事项

原生驱动目前并不完全支持`Animated`。 主要限制是您只能对非布局属性进行动画处理：比如 `transform` 和 `opacity` 但`flexbox`和`position`属性则不行。 使用`Animated.event`时，它只能用于直接事件而不是冒泡事件。 这意味着它不适用于`PanResponder`，但可以与`ScrollView#onScroll`一起使用
在动画运行时，可以防止VirtualizedList组件渲染更多行。 如果您需要在用户滚动浏览列表时运行长循环动画，则可以在动画配置中使用 `isInteraction：false` 来防止此问题。

### Bear in mind

While using transform styles such as `rotateY`, `rotateX`, and others ensure the transform style `perspective` is in place. At this time some animations may not render on Android without it. Example below.

```javascript
<Animated.View
  style={{
    transform: [
      {scale: this.state.scale},
      {rotateY: this.state.rotateY},
      {perspective: 1000}, // without this line this Animation will not render on Android while working fine on iOS
    ],
  }}
/>
```

### Additional examples

The RNTester app has various examples of `Animated` in use:

* [AnimatedGratuitousApp](https://github.com/facebook/react-native/tree/master/RNTester/js/AnimatedGratuitousApp)
* [NativeAnimationsExample](https://github.com/facebook/react-native/blob/master/RNTester/js/NativeAnimationsExample.js)

## `LayoutAnimation` API

`LayoutAnimation` allows you to globally configure `create` and `update` animations that will be used for all views in the next render/layout cycle. This is useful for doing flexbox layout updates without bothering to measure or calculate specific properties in order to animate them directly, and is especially useful when layout changes may affect ancestors, for example a "see more" expansion that also increases the size of the parent and pushes down the row below which would otherwise require explicit coordination between the components in order to animate them all in sync.

Note that although `LayoutAnimation` is very powerful and can be quite useful, it provides much less control than `Animated` and other animation libraries, so you may need to use another approach if you can't get `LayoutAnimation` to do what you want.

Note that in order to get this to work on **Android** you need to set the following flags via `UIManager`:

```javascript
UIManager.setLayoutAnimationEnabledExperimental &&
  UIManager.setLayoutAnimationEnabledExperimental(true);
```

```SnackPlayer
import React from 'react';
import {
  NativeModules,
  LayoutAnimation,
  Text,
  TouchableOpacity,
  StyleSheet,
  View,
} from 'react-native';

const { UIManager } = NativeModules;

UIManager.setLayoutAnimationEnabledExperimental &&
  UIManager.setLayoutAnimationEnabledExperimental(true);

export default class App extends React.Component {
  state = {
    w: 100,
    h: 100,
  };

  _onPress = () => {
    // Animate the update
    LayoutAnimation.spring();
    this.setState({w: this.state.w + 15, h: this.state.h + 15})
  }

  render() {
    return (
      <View style={styles.container}>
        <View style={[styles.box, {width: this.state.w, height: this.state.h}]} />
        <TouchableOpacity onPress={this._onPress}>
          <View style={styles.button}>
            <Text style={styles.buttonText}>Press me!</Text>
          </View>
        </TouchableOpacity>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'center',
  },
  box: {
    width: 200,
    height: 200,
    backgroundColor: 'red',
  },
  button: {
    backgroundColor: 'black',
    paddingHorizontal: 20,
    paddingVertical: 15,
    marginTop: 15,
  },
  buttonText: {
    color: '#fff',
    fontWeight: 'bold',
  },
});
```

This example uses a preset value, you can customize the animations as you need, see [LayoutAnimation.js](https://github.com/facebook/react-native/blob/master/Libraries/LayoutAnimation/LayoutAnimation.js) for more information.

## Additional notes

### `requestAnimationFrame`

`requestAnimationFrame` is a polyfill from the browser that you might be familiar with. It accepts a function as its only argument and calls that function before the next repaint. It is an essential building block for animations that underlies all of the JavaScript-based animation APIs. In general, you shouldn't need to call this yourself - the animation APIs will manage frame updates for you.

### `setNativeProps`

As mentioned [in the Direct Manipulation section](direct-manipulation.md), `setNativeProps` allows us to modify properties of native-backed components (components that are actually backed by native views, unlike composite components) directly, without having to `setState` and re-render the component hierarchy.

We could use this in the Rebound example to update the scale - this might be helpful if the component that we are updating is deeply nested and hasn't been optimized with `shouldComponentUpdate`.

If you find your animations with dropping frames (performing below 60 frames per second), look into using `setNativeProps` or `shouldComponentUpdate` to optimize them. Or you could run the animations on the UI thread rather than the JavaScript thread [with the useNativeDriver option](http://facebook.github.io/react-native/blog/2017/02/14/using-native-driver-for-animated.html). You may also want to defer any computationally intensive work until after animations are complete, using the [InteractionManager](interactionmanager.md). You can monitor the frame rate by using the In-App Developer Menu "FPS Monitor" tool.
