---
id: version-0.54-performance
title: 性能
original_id: performance
---

使用React Native替代基于WebView的框架来开发App的一个强有力的理由，就是为了使App可以达到每秒60帧（足够流畅），并且能有类似原生App的外观和手感。因此我们也尽可能地优化React Native去实现这一目标，使开发者能集中精力处理App的业务逻辑，而不用费心考虑性能。但是，总还是有一些地方有所欠缺，以及在某些场合React Native还不能够替你决定如何进行优化（用原生代码写也无法避免），因此人工的干预依然是必要的。 本文的目的是教给你一些基本的知识，来帮你排查性能方面的问题，以及探讨这些问题产生的原因和推荐的解决方法。

本指南旨在教您一些基本知识，以帮助您[解决性能问题](performance.md#profiling)，并[讨论问题的常见来源及其建议的解决方案](performance.md#common-sources-of-performance-problems)。

## 关于“帧”你所需要知道的

老一辈人常常把电影称为[“活动画面”](https://www.youtube.com/watch?v=F1i40rnpOsA)，是因为视频中逼真的动态效果其实是一种幻觉，这种幻觉是由一组静态的图片以一个稳定的速度快速变化所产生的。我们把这组图片中的每一张图片叫做一帧，而每秒钟显示的帧数直接的影响了视频（或者说用户界面）的流畅度和真实感。iOS设备提供了每秒60的帧率，这就留给了开发者和UI系统大约16.67ms来完成生成一张静态图片（帧）所需要的所有工作。如果在这分派的16.67ms之内没有能够完成这些工作，就会引发‘丢帧’的后果，使界面表现的不够流畅。

下面要讲的事情可能更为复杂：请先调出你应用的开发菜单，打开 `Show FPS Monitor`. 你会注意到有两个不同的帧率.

![](react-native/docs/assets/PerfUtil.png)

### JavaScript 帧率 (JavaScript 线程)

对大多数React Native应用来说，业务逻辑是运行在JavaScript线程上的。这是React应用所在的线程，也是发生API调用，以及处理触摸事件等操作的线程。更新数据到原生支持的视图是批量进行的，并且在事件循环每进行一次的时候被发送到原生端，这一步通常会在一帧时间结束之前处理完（如果一切顺利的话）。如果JavaScript线程有一帧没有及时响应，就被认为发生了一次丢帧。 例如，你在一个复杂应用的根组件上调用了`this.setState`，从而导致一次开销很大的子组件树的重绘，可想而知，这可能会花费200ms也就是整整12帧的丢失。此时，任何由JavaScript控制的动画都会卡住。只要卡顿超过100ms，用户就会感觉到明显的卡顿。

这种情况经常发生在`Navigator`的切换过程中：当你push一个新的路由时，JavaScript需要绘制新场景所需的所有组件，以发送正确的命令给原生端去创建视图。由于切换是由JavaScript线程所控制，因此经常会占用若干帧的时间，引起一些卡顿( [jank](http://jankfree.org/) )。有的时候，组件会在`componentDidMount`函数中做一些额外的事情，这甚至可能会导致页面切换过程中多达一秒的卡顿。

另一个例子是触摸事件的响应：如果你正在JavaScript线程处理一个跨越多个帧的工作，你可能会注意到`TouchableOpacity`的响应被延迟了。这是因为JavaScript线程太忙了，不能够处理主线程发送过来的原始触摸事件。结果`TouchableOpacity`就不能及时响应这些事件并命令主线程的页面去调整透明度了。

### UI 帧速率 (主线程)

很多人会注意到，`NavigatorIOS` 的性能要比 `Navigator`好的多。原因就是它的切换动画是完全在主线程上执行的，因此不会被JavaScript线程上的掉帧所影响。

同样，当JavaScript线程卡住的时候，你仍然可以欢快的上下滚动 `ScrollView`，因为 `ScrollView` 运行在主线程之上（尽管滚动事件会被分发到JS线程，但是接收这些事件对于滚动这个动作来说并不必要）。

## 性能问题的常见原因

### 使用开发模式运行APP (`dev=true`)

在开发模式下，JavaScript线程的性能会受到极大的影响，这无法避免：运行时需要做大量的其他工作才能为您提供良好的警告和错误消息提示、以及验证propTypes和其他各种断点。请在[release builds](running-on-device.md#building-your-app-for-production) 中测试性能以确认其正确发布。

### 使用 console.log 语句

运行bundle App时，这些语句可能会在JavaScript线程中造成严重瓶颈。包括调试库（如[redux-logger](https://github.com/evgenyrodionov/redux-logger)）的调用，因此请确保在捆绑之前将其删除。你也可以使用这个babel插件来删除所有的控制台 `console.*`。你需要先运行命令`npm i babel-plugin-transform-remove-console --save`，然后依照下方示例编辑`.babelrc`文件:

```javascripton
{
  "env": {
    "production": {
      "plugins": ["transform-remove-console"]
    }
  }
}
```

这将在项目发布的 release(production)版本中自动屏蔽所有的 `console.*` 调用。

### `ListView` 初始化渲染过慢以及列表项过多时滚动性能变差的相关问题

请改用新的[`FlatList`](flatlist.md)或[`SectionList`](sectionList.md)组件。他们不仅仅简化了API，还具有显着的性能增强，无论列表中有多少项元素组件的内存占用都不会发生太大的变化。

如果您的[`FlatList`](flatlist.md)渲染缓慢，请确保您已经使用了[`getItemLayout`](https://facebook.github.io/react-native/flatlist.md#getitemlayout)，以跳过对渲染项目的数量统计以优化渲染速度。

### 重绘一个几乎没有变化的页面时，JS帧率严重下降（卡顿）

如果你正在使用一个ListView，你必须提供一个 `rowHasChanged` 函数，它通过快速的算出某一行是否需要重绘，来减少很多不必要的工作。如果你使用了不可变的数据结构，这项工作就只需检查其引用是否相等。

同样的，你可以实现 `shouldComponentUpdate` 函数来指明在什么样的确切条件下，你希望这个组件得到重绘。如果你编写的是纯粹的组件（返回值完全由props和state所决定），你可以利用PureComponent来为你做这个工作。再强调一次，不可变的数据结构在提速方面非常有用 —— 当你不得不对一个长列表对象做一个深度的比较，它会使重绘你的整个组件更加快速，而且代码量更少。

### 在JavaScript线程中同时执行多个任务，导致JS线程掉帧

“导航切换极慢” 是该问题的常见表现。在其他情形下，这种问题也可能会出现。使用InteractionManager是一个好的方法，但是如果在动画中，为了用户体验的开销而延迟其他工作并不太能接受，那么你可以考虑一下使用LayoutAnimation。

Animated的接口一般会在JavaScript线程中计算出所需要的每一个关键帧，除非您[`设置useNativeDriver：true`](https://facebook.github.io/react-native/blog/2017/02/14/using-native-driver-for-animated.html#how-do-i-use-this-in-my-app)，这样一来LayoutAnimation将利用Core Animation，使动画不会被JS线程和主线程的掉帧所影响。

举一个需要使用这项功能的例子：比如需要给一个模态框做动画（从下往上划动，并在半透明遮罩中淡入），而这个模态框正在初始化，并且可能响应着几个网络请求，渲染着页面的内容，并且还在更新着打开这个模态框的父页面。了解更多有关如何使用LayoutAnimation的信息，请参阅动画指南。

注意：

* LayoutAnimation只工作在“一次性”的动画上（"静态"动画） -- 如果动画可能会被中途取消，你还是需要使用 `Animated`。

### 在屏幕上移动视图（滚动、切换、旋转）出现UI线程掉帧

This is especially true when you have text with a transparent background positioned on top of an image, or any other situation where alpha compositing would be required to re-draw the view on each frame. You will find that enabling `shouldRasterizeIOS` or `renderToHardwareTextureAndroid` can help with this significantly.

Be careful not to overuse this or your memory usage could go through the roof. Profile your performance and memory usage when using these props. If you don't plan to move a view anymore, turn this property off.

当具有透明背景的文本位于一张图片上时，或者在每帧重绘视图时需要用到透明合成的任何其他情况下，这种现象尤为明显。设置shouldRasterizeIOS或者renderToHardwareTextureAndroid属性可以显著改善这一现象。 注意不要过度使用该特性，否则你的内存使用量将会飞涨。在使用时，要评估你的性能和内存使用情况。如果你没有需要移动这个视图的需求，请关闭这一属性。

### Animating the size of an image drops UI thread FPS

On iOS, each time you adjust the width or height of an Image component it is re-cropped and scaled from the original image. This can be very expensive, especially for large images. Instead, use the `transform: [{scale}]` style property to animate the size. An example of when you might do this is when you tap an image and zoom it in to full screen.

### My TouchableX view isn't very responsive

Sometimes, if we do an action in the same frame that we are adjusting the opacity or highlight of a component that is responding to a touch, we won't see that effect until after the `onPress` function has returned. If `onPress` does a `setState` that results in a lot of work and a few frames dropped, this may occur. A solution to this is to wrap any action inside of your `onPress` handler in `requestAnimationFrame`:

```javascript
handleOnPress() {
  // Always use TimerMixin with requestAnimationFrame, setTimeout and
  // setInterval
  this.requestAnimationFrame(() => {
    this.doExpensiveAction();
  });
}
```

### Slow navigator transitions

As mentioned above, `Navigator` animations are controlled by the JavaScript thread. Imagine the "push from right" scene transition: each frame, the new scene is moved from the right to left, starting offscreen (let's say at an x-offset of 320) and ultimately settling when the scene sits at an x-offset of

0. Each frame during this transition, the JavaScript thread needs to send a new x-offset to the main thread. If the JavaScript thread is locked up, it cannot do this and so no update occurs on that frame and the animation stutters.

One solution to this is to allow for JavaScript-based animations to be offloaded to the main thread. If we were to do the same thing as in the above example with this approach, we might calculate a list of all x-offsets for the new scene when we are starting the transition and send them to the main thread to execute in an optimized way. Now that the JavaScript thread is freed of this responsibility, it's not a big deal if it drops a few frames while rendering the scene -- you probably won't even notice because you will be too distracted by the pretty transition.

Solving this is one of the main goals behind the new [React Navigation](navigation.md) library. The views in React Navigation use native components and the [`Animated`](animated.md) library to deliver 60 FPS animations that are run on the native thread.

## Profiling

Use the built-in profiler to get detailed information about work done in the JavaScript thread and main thread side-by-side. Access it by selecting Perf Monitor from the Debug menu.

For iOS, Instruments is an invaluable tool, and on Android you should learn to use [`systrace`](performance.md#profiling-android-ui-performance-with-systrace).

But first, [**make sure that Development Mode is OFF!**](performance.md#running-in-development-mode-dev-true) You should see `__DEV__ === false, development-level warning are OFF, performance optimizations are ON` in your application logs.

Another way to profile JavaScript is to use the Chrome profiler while debugging. This won't give you accurate results as the code is running in Chrome but will give you a general idea of where bottlenecks might be. Run the profiler under Chrome's `Performance` tab. A flame graph will appear under `User Timing`. To view more details in tabular format, click at the `Bottom Up` tab below and then select `DedicatedWorker Thread` at the top left menu.

### Profiling Android UI Performance with `systrace`

Android supports 10k+ different phones and is generalized to support software rendering: the framework architecture and need to generalize across many hardware targets unfortunately means you get less for free relative to iOS. But sometimes, there are things you can improve -- and many times it's not native code's fault at all!

The first step for debugging this jank is to answer the fundamental question of where your time is being spent during each 16ms frame. For that, we'll be using a standard Android profiling tool called `systrace`.

`systrace` is a standard Android marker-based profiling tool (and is installed when you install the Android platform-tools package). Profiled code blocks are surrounded by start/end markers which are then visualized in a colorful chart format. Both the Android SDK and React Native framework provide standard markers that you can visualize.

#### 1. Collecting a trace

First, connect a device that exhibits the stuttering you want to investigate to your computer via USB and get it to the point right before the navigation/animation you want to profile. Run `systrace` as follows:

```
$ <path_to_android_sdk>/platform-tools/systrace/systrace.py --time=10 -o trace.html sched gfx view -a <your_package_name>
```

A quick breakdown of this command:

* `time` is the length of time the trace will be collected in seconds
* `sched`, `gfx`, and `view` are the android SDK tags (collections of markers) we care about: `sched` gives you information about what's running on each core of your phone, `gfx` gives you graphics info such as frame boundaries, and `view` gives you information about measure, layout, and draw passes
* `-a <your_package_name>` enables app-specific markers, specifically the ones built into the React Native framework. `your_package_name` can be found in the `AndroidManifest.xml` of your app and looks like `com.example.app`

Once the trace starts collecting, perform the animation or interaction you care about. At the end of the trace, systrace will give you a link to the trace which you can open in your browser.

#### 2. Reading the trace

After opening the trace in your browser (preferably Chrome), you should see something like this:

![Example](/react-native/docs/assets/SystraceExample.png)

> **HINT**: Use the WASD keys to strafe and zoom

If your trace .html file isn't opening correctly, check your browser console for the following:

![ObjectObserveError](/react-native/docs/assets/ObjectObserveError.png)

Since `Object.observe` was deprecated in recent browsers, you may have to open the file from the Google Chrome Tracing tool. You can do so by:

* Opening tab in chrome chrome://tracing
* Selecting load
* Selecting the html file generated from the previous command.

> **Enable VSync highlighting**
>
> Check this checkbox at the top right of the screen to highlight the 16ms frame boundaries:
>
> ![Enable VSync Highlighting](/react-native/docs/assets/SystraceHighlightVSync.png)
>
> You should see zebra stripes as in the screenshot above. If you don't, try profiling on a different device: Samsung has been known to have issues displaying vsyncs while the Nexus series is generally pretty reliable.

#### 3. Find your process

Scroll until you see (part of) the name of your package. In this case, I was profiling `com.facebook.adsmanager`, which shows up as `book.adsmanager` because of silly thread name limits in the kernel.

On the left side, you'll see a set of threads which correspond to the timeline rows on the right. There are a few threads we care about for our purposes: the UI thread (which has your package name or the name UI Thread), `mqt_js`, and `mqt_native_modules`. If you're running on Android 5+, we also care about the Render Thread.

* **UI Thread.** This is where standard android measure/layout/draw happens. The thread name on the right will be your package name (in my case book.adsmanager) or UI Thread. The events that you see on this thread should look something like this and have to do with `Choreographer`, `traversals`, and `DispatchUI`:

  ![UI Thread Example](/react-native/docs/assets/SystraceUIThreadExample.png)

* **JS Thread.** This is where JavaScript is executed. The thread name will be either `mqt_js` or `<...>` depending on how cooperative the kernel on your device is being. To identify it if it doesn't have a name, look for things like `JSCall`, `Bridge.executeJSCall`, etc:

  ![JS Thread Example](/react-native/docs/assets/SystraceJSThreadExample.png)

* **Native Modules Thread.** This is where native module calls (e.g. the `UIManager`) are executed. The thread name will be either `mqt_native_modules` or `<...>`. To identify it in the latter case, look for things like `NativeCall`, `callJavaModuleMethod`, and `onBatchComplete`:

  ![Native Modules Thread Example](/react-native/docs/assets/SystraceNativeModulesThreadExample.png)

* **Bonus: Render Thread.** If you're using Android L (5.0) and up, you will also have a render thread in your application. This thread generates the actual OpenGL commands used to draw your UI. The thread name will be either `RenderThread` or `<...>`. To identify it in the latter case, look for things like `DrawFrame` and `queueBuffer`:

  ![Render Thread Example](/react-native/docs/assets/SystraceRenderThreadExample.png)

#### Identifying a culprit

A smooth animation should look something like the following:

![Smooth Animation](/react-native/docs/assets/SystraceWellBehaved.png)

Each change in color is a frame -- remember that in order to display a frame, all our UI work needs to be done by the end of that 16ms period. Notice that no thread is working close to the frame boundary. An application rendering like this is rendering at 60 FPS.

If you noticed chop, however, you might see something like this:

![Choppy Animation from JS](/react-native/docs/assets/SystraceBadJS.png)

Notice that the JS thread is executing basically all the time, and across frame boundaries! This app is not rendering at 60 FPS. In this case, **the problem lies in JS**.

You might also see something like this:

![Choppy Animation from UI](/react-native/docs/assets/SystraceBadUI.png)

In this case, the UI and render threads are the ones that have work crossing frame boundaries. The UI that we're trying to render on each frame is requiring too much work to be done. In this case, **the problem lies in the native views being rendered**.

At this point, you'll have some very helpful information to inform your next steps.

#### Resolving JavaScript issues

If you identified a JS problem, look for clues in the specific JS that you're executing. In the scenario above, we see `RCTEventEmitter` being called multiple times per frame. Here's a zoom-in of the JS thread from the trace above:

![Too much JS](/react-native/docs/assets/SystraceBadJS2.png)

This doesn't seem right. Why is it being called so often? Are they actually different events? The answers to these questions will probably depend on your product code. And many times, you'll want to look into [shouldComponentUpdate](https://facebook.github.io/react/component-specs.md#updating-shouldcomponentupdate).

#### Resolving native UI Issues

If you identified a native UI problem, there are usually two scenarios:

1. the UI you're trying to draw each frame involves too much work on the GPU, or
2. You're constructing new UI during the animation/interaction (e.g. loading in new content during a scroll).

##### Too much GPU work

In the first scenario, you'll see a trace that has the UI thread and/or Render Thread looking like this:

![Overloaded GPU](/react-native/docs/assets/SystraceBadUI.png)

Notice the long amount of time spent in `DrawFrame` that crosses frame boundaries. This is time spent waiting for the GPU to drain its command buffer from the previous frame.

To mitigate this, you should:

* investigate using `renderToHardwareTextureAndroid` for complex, static content that is being animated/transformed (e.g. the `Navigator` slide/alpha animations)
* make sure that you are **not** using `needsOffscreenAlphaCompositing`, which is disabled by default, as it greatly increases the per-frame load on the GPU in most cases.

If these don't help and you want to dig deeper into what the GPU is actually doing, you can check out [Tracer for OpenGL ES](http://developer.android.com/tools/help/gltracer.html).

##### Creating new views on the UI thread

In the second scenario, you'll see something more like this:

![Creating Views](/react-native/docs/assets/SystraceBadCreateUI.png)

Notice that first the JS thread thinks for a bit, then you see some work done on the native modules thread, followed by an expensive traversal on the UI thread.

There isn't an easy way to mitigate this unless you're able to postpone creating new UI until after the interaction, or you are able to simplify the UI you're creating. The react native team is working on an infrastructure level solution for this that will allow new UI to be created and configured off the main thread, allowing the interaction to continue smoothly.

## Unbundling + inline requires

If you have a large app you may want to consider unbundling and using inline requires. This is useful for apps that have a large number of screens which may not ever be opened during a typical usage of the app. Generally it is useful to apps that have large amounts of code that are not needed for a while after startup. For instance the app includes complicated profile screens or lesser used features, but most sessions only involve visiting the main screen of the app for updates. We can optimize the loading of the bundle by using the unbundle feature of the packager and requiring those features and screens inline (when they are actually used).

### Loading JavaScript

Before react-native can execute JS code, that code must be loaded into memory and parsed. With a standard bundle if you load a 50mb bundle, all 50mb must be loaded and parsed before any of it can be executed. The optimization behind unbundling is that you can load only the portion of the 50mb that you actually need at startup, and progressively load more of the bundle as those sections are needed.

### Inline Requires

Inline requires delay the requiring of a module or file until that file is actually needed. A basic example would look like this:

#### VeryExpensive.js

```
import React, { Component } from 'react';
import { Text } from 'react-native';
// ... import some very expensive modules

// You may want to log at the file level to verify when this is happening
console.log('VeryExpensive component loaded');

export default class VeryExpensive extends Component {
  // lots and lots of code
  render() {
    return <Text>Very Expensive Component</Text>;
  }
}
```

#### Optimized.js

```
import React, { Component } from 'react';
import { TouchableOpacity, View, Text } from 'react-native';

let VeryExpensive = null;

export default class Optimized extends Component {
  state = { needsExpensive: false };

  didPress = () => {
    if (VeryExpensive == null) {
      VeryExpensive = require('./VeryExpensive').default;
    }

    this.setState(() => ({
      needsExpensive: true,
    }));
  };

  render() {
    return (
      <View style={{ marginTop: 20 }}>
        <TouchableOpacity onPress={this.didPress}>
          <Text>Load</Text>
        </TouchableOpacity>
        {this.state.needsExpensive ? <VeryExpensive /> : null}
      </View>
    );
  }
}
```

Even without unbundling inline requires can lead to startup time improvements, because the code within VeryExpensive.js will only execute once it is required for the first time.

### Enable Unbundling

On iOS unbundling will create a single indexed file that react native will load one module at a time. On Android, by default it will create a set of files for each module. You can force Android to create a single file, like iOS, but using multiple files can be more performant and requires less memory.

Enable unbundling in Xcode by editing the build phase "Bundle React Native code and images". Before `../node_modules/react-native/packager/react-native-xcode.sh` add `export BUNDLE_COMMAND="unbundle"`:

```
export BUNDLE_COMMAND="unbundle"
export NODE_BINARY=node
../node_modules/react-native/packager/react-native-xcode.sh
```

On Android enable unbundling by editing your android/app/build.gradle file. Before the line `apply from: "../../node_modules/react-native/react.gradle"` add or amend the `project.ext.react` block:

```
project.ext.react = [
  bundleCommand: "unbundle",
]
```

Use the following lines on Android if you want to use a single indexed file:

```
project.ext.react = [
  bundleCommand: "unbundle",
  extraPackagerArgs: ["--indexed-unbundle"]
]
```

### Configure Preloading and Inline Requires

Now that we have unbundled our code, there is overhead for calling require. require now needs to send a message over the bridge when it encounters a module it has not loaded yet. This will impact startup the most, because that is where the largest number of require calls are likely to take place while the app loads the initial module. Luckily we can configure a portion of the modules to be preloaded. In order to do this, you will need to implement some form of inline require.

### Adding a packager config file

Create a folder in your project called packager, and create a single file named config.js. Add the following:

```
const config = {
  getTransformOptions: () => {
    return {
      transform: { inlineRequires: true },
    };
  },
};

module.exports = config;
```

In Xcode, in the build phase, include `export BUNDLE_CONFIG="packager/config.js"`.

```
export BUNDLE_COMMAND="unbundle"
export BUNDLE_CONFIG="packager/config.js"
export NODE_BINARY=node
../node_modules/react-native/packager/react-native-xcode.sh
```

Edit your android/app/build.gradle file to include `bundleConfig: "packager/config.js",`.

```
project.ext.react = [
  bundleCommand: "unbundle",
  bundleConfig: "packager/config.js"
]
```

Finally, you can update "start" under "scripts" on your package.json to use the config:

`"start": "node node_modules/react-native/local-cli/cli.js start --config ../../../../packager/config.js",`

Start your package server with `npm start`. Note that when the dev packager is automatically launched via xcode and `react-native run-android`, etc, it does not use `npm start`, so it won't use the config.

### Investigating the Loaded Modules

In your root file (index.(ios|android).js) you can add the following after the initial imports:

```
const modules = require.getModules();
const moduleIds = Object.keys(modules);
const loadedModuleNames = moduleIds
  .filter(moduleId => modules[moduleId].isInitialized)
  .map(moduleId => modules[moduleId].verboseName);
const waitingModuleNames = moduleIds
  .filter(moduleId => !modules[moduleId].isInitialized)
  .map(moduleId => modules[moduleId].verboseName);

// make sure that the modules you expect to be waiting are actually waiting
console.log(
  'loaded:',
  loadedModuleNames.length,
  'waiting:',
  waitingModuleNames.length
);

// grab this text blob, and put it in a file named packager/moduleNames.js
console.log(`module.exports = ${JSON.stringify(loadedModuleNames.sort())};`);
```

When you run your app, you can look in the console and see how many modules have been loaded, and how many are waiting. You may want to read the moduleNames and see if there are any surprises. Note that inline requires are invoked the first time the imports are referenced. You may need to investigate and refactor to ensure only the modules you want are loaded on startup. Note that you can change the Systrace object on require to help debug problematic requires.

```
require.Systrace.beginEvent = (message) => {
  if(message.includes(problematicModule)) {
    throw new Error();
  }
}
```

Every app is different, but it may make sense to only load the modules you need for the very first screen. When you are satisified, put the output of the loadedModuleNames into a file named packager/moduleNames.js.

### Transforming to Module Paths

The loaded module names get us part of the way there, but we actually need absolute module paths, so the next script will set that up. Add `packager/generateModulePaths.js` to your project with the following:

```
// @flow
/* eslint-disable no-console */
const execSync = require('child_process').execSync;
const fs = require('fs');
const moduleNames = require('./moduleNames');

const pjson = require('../package.json');
const localPrefix = `${pjson.name}/`;

const modulePaths = moduleNames.map(moduleName => {
  if (moduleName.startsWith(localPrefix)) {
    return `./${moduleName.substring(localPrefix.length)}`;
  }
  if (moduleName.endsWith('.js')) {
    return `./node_modules/${moduleName}`;
  }
  try {
    const result = execSync(
      `grep "@providesModule ${moduleName}" $(find . -name ${moduleName}\\\\.js) -l`
    )
      .toString()
      .trim()
      .split('\n')[0];
    if (result != null) {
      return result;
    }
  } catch (e) {
    return null;
  }
  return null;
});

const paths = modulePaths
  .filter(path => path != null)
  .map(path => `'${path}'`)
  .join(',\n');

const fileData = `module.exports = [${paths}];`;

fs.writeFile('./packager/modulePaths.js', fileData, err => {
  if (err) {
    console.log(err);
  }

  console.log('Done');
});
```

You can run via `node packager/modulePaths.js`.

This script attempts to map from the module names to module paths. Its not foolproof though, for instance, it ignores platform specific files (\*ios.js, and \*.android.js). However based on initial testing, it handles 95% of cases. When it runs, after some time it should complete and output a file named `packager/modulePaths.js`. It should contain paths to module files that are relative to your projects root. You can commit modulePaths.js to your repo so it is transportable.

### Updating the config.js

Returning to packager/config.js we should update it to use our newly generated modulePaths.js file.

```
const modulePaths = require('./modulePaths');
const resolve = require('path').resolve;
const fs = require('fs');

const config = {
  getTransformOptions: () => {
    const moduleMap = {};
    modulePaths.forEach(path => {
      if (fs.existsSync(path)) {
        moduleMap[resolve(path)] = true;
      }
    });
    return {
      preloadedModules: moduleMap,
      transform: { inlineRequires: { blacklist: moduleMap } },
    };
  },
};

module.exports = config;
```

The preloadedModules entry in the config indicates which modules should be marked as preloaded by the unbundler. When the bundle is loaded, those modules are immediately loaded, before any requires have even executed. The blacklist entry indicates that those modules should not be required inline. Because they are preloaded, there is no performance benefit from using an inline require. In fact the javascript spends extra time resolving the inline require every time the imports are referenced.

### Test and Measure Improvements

You should now be ready to build your app using unbundling and inline requires. Make sure you measure the before and after startup times.
