---
id: version-0.54-timers
title: 定时器
original_id: timers
---

定时器是一个应用中非常重要的部分。React Native实现了和浏览器一致的[定时器Timer](https://developer.mozilla.org/en-US/Add-ons/Code_snippets/Timers)。

## 定时器

* setTimeout, clearTimeout
* setInterval, clearInterval
* setImmediate, clearImmediate
* requestAnimationFrame, cancelAnimationFrame

`requestAnimationFrame(fn)`和`setTimeout(fn, 0)`不同，前者会在每帧刷新之后执行一次，而后者则会尽可能快的执行（在iPhone5S上有可能每秒1000次以上）。

`setImmediate`则会在当前JavaScript执行块结束的时候执行，就在将要发送批量响应数据到原生之前。注意如果你在`setImmediate`的回调函数中又执行了`setImmediate`，它会紧接着立刻执行，而不会在调用之前等待原生代码。

`Promise`的实现就使用了`setImmediate`来执行异步调用。

## InteractionManager

原生应用感觉如此流畅的一个重要原因就是在互动和动画的过程中避免繁重的操作。在React Native里，我们目前受到限制，因为我们只有一个JavaScript执行线程。不过你可以用 `InteractionManager` 来确保在执行繁重工作之前所有的交互和动画都已经处理完毕。

应用可以通过以下代码来安排一个任务，使其在交互结束之后执行：

```javascript
InteractionManager.runAfterInteractions(() => {
  // ...long-running synchronous task...
});
```

我们来把它和之前的几个任务安排方法对比一下：

- requestAnimationFrame(): 用来执行在一段时间内控制视图动画的代码
- setImmediate/setTimeout/setInterval(): 在稍后执行代码。注意这有可能会延迟当前正在进行的动画。
- runAfterInteractions(): 在稍后执行代码，不会延迟当前进行的动画。

触摸处理系统会把一个或多个进行中的触摸操作认定为'交互'，并且会将`runAfterInteractions()`的回调函数延迟执行，直到所有的触摸操作都结束或取消了。

InteractionManager还允许应用注册动画，在动画开始时创建一个交互“句柄”，然后在结束的时候清除它。

```javascript
var handle = InteractionManager.createInteractionHandle();
// run animation... (`runAfterInteractions` tasks are queued)
// later, on animation completion:
InteractionManager.clearInteractionHandle(handle);
// queued tasks run if all handles were cleared
```

## TimerMixin

我们发现使用React Native构建的应用发生致命错误（闪退）的主要原因是由于定时器在组件卸载后被触发。 为了解决这个反复出现的问题，我们带来了`TimerMixin`。 如果您包含`TimerMixin`，则可以使用`this.setTimeout（fn，500）`将您的调用替换为`setTimeout（fn，500）（只需预先设置）`。当组件卸载后，所有内容都将被正确清理。

这个库并未集成至React-Native,如果你需要使用它，请使用 `npm i react-timer-mixin --save` 进行安装。

```javascript
import TimerMixin from 'react-timer-mixin';

var Component = createReactClass({
  mixins: [TimerMixin],
  componentDidMount: function() {
    this.setTimeout(() => {
      console.log('I do not leak!');
    }, 500);
  },
});
```

这将避免在消除BUG上耗费过多的时间，例如组件卸载后定时器超时引发的崩溃。

请记住，如果您使用ES6来编写React组件 [不能使用mixins的内置API](https://facebook.github.io/react/blog/2015/01/27/react-v0.13.0-beta-1.html#mixins).要将`TimerMixin` 与 ES6 类一齐使用 , 我们推荐 [react-mixin](https://github.com/brigand/react-mixin).
