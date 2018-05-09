---
id: version-0.54-improvingux
title: 提升用户体验
original_id: improvingux
---

在移动应用开发之中，有大量琐碎而微妙的细节需要注意，而开发人员往往会忽视掉这些东西，本文将介绍这些问题，并示例如何在React Native中处理这些问题。

> We are improving and adding more details to this page. If you'd like to help out, chime in at [react-native/14979](https://github.com/facebook/react-native/issues/14979).

我们将持续改进并增加更多关于“提升用户体验”的信息。 如果你想帮忙，请访问 [react-native/14979](https://github.com/facebook/react-native/issues/14979)。

## 要点索引

* [配置文本输入](#配置文本输入)
* [虚拟键盘弹出时的布局管理](#虚拟键盘弹出时的布局管理)
* [点击区域自动放大](#make-tappable-areas-larger)
* [使用 Android Ripple(点击操作的图形反馈)](#use-android-ripple)
* [更多](#learn-more)

---

## 配置文本输入

在触控手机上输入文字是一种挑战 - 小屏幕，虚拟键盘。 但是根据用户需要输入的数据类型，我们可以通过配置文本输入设置来简化它：

* 输入框自动获取焦点
* 使用输入提示（placeholder）来展示正确的输入数据示例
* 启用或关闭自动补全和自动纠错
* 选择合适的键盘类型 (比如 邮件, 数字)
* Make sure the return button focuses the next field or submits the form 确保返回按钮

Check out [`TextInput` docs](textinput.md) for more configuration options.
查看 [`TextInput`文档](textinput.md)以获取更多的配置选项

<video src="/react-native/img/textinput.mp4" autoplay loop width="320" height="430"></video>

[Try it on your phone](https://snack.expo.io/H1iGt2vSW)

## 虚拟键盘弹出时的布局管理

Software keyboard takes almost half of the screen. If you have interactive elements that can get covered by the keyboard, make sure they are still accessible by using the [`KeyboardAvoidingView` component](keyboardavoidingview.md).

<video src="/react-native/img/keyboardavoidingview.mp4" autoplay loop width="320" height="448"></video>

[Try it on your phone](https://snack.expo.io/ryxRkwnrW)

## Make tappable areas larger

On mobile phones it's hard to be very precise when pressing buttons. Make sure all interactive elements are 44x44 or larger. One way to do this is to leave enough space for the element, `padding`, `minWidth` and `minHeight` style values can be useful for that. Alternatively, you can use [`hitSlop` prop](touchablewithoutfeedback.md#hitslop) to increase interactive area without affecting the layout. Here's a demo:

<video src="/react-native/img/hitslop.mp4" autoplay loop width="320" height="120"></video>

[Try it on your phone](https://snack.expo.io/rJPwCt4HZ)

## Use Android Ripple

Android API 21+ uses the material design ripple to provide user with feedback when they touch an interactable area on the screen. React Native exposes this through the [`TouchableNativeFeedback` component](touchablenativefeedback.md). Using this touchable effect instead of opacity or highlight will often make your app feel much more fitting on the platform. That said, you need to be careful when using it because it doesn't work on iOS or on Android API < 21, so you will need to fallback to using one of the other Touchable components on iOS. You can use a library like [react-native-platform-touchable](https://github.com/react-community/react-native-platform-touchable) to handle the platform differences for you.

<video src="/react-native/img/ripple.mp4" autoplay loop width="320"></video>

[Try it on your phone](https://snack.expo.io/SJywqe3rZ)

## Screen orientation lock

Unless supporting both, it is considered good practice to lock the screen orientation to either portrait or landscape. On iOS, in the General tab and Deployment Info section of Xcode enable the Device Orientation you want to support (ensure you have selected iPhone from the Devices menu when making the changes). For Android, open the AndroidManifest.xml file and within the activity element add 'android:screenOrientation=”portrait”' to lock to portrait or 'android:screenOrientation=”landscape”' to lock to landscape.

# Learn more

[Material Design](https://material.io/) and [Human Interface Guidelines](https://developer.apple.com/ios/human-interface-guidelines/overview/design-principles/) are great resources for learning more about designing for mobile platforms.
