---
id: platform-specific-code
title: 特定平台代码
---

当编写跨平台APP时，你可能试图尽可能的复用代码，但也可以针对不同平台编写代码，例如：您可以为ios和android实现两套不同的可视化组件。

`React-Native`提供了两种针对不同平台编写不同代码的方法：

* 使用 [`Platform` module](platform-specific-code.md#platform-module).
* 使用 [platform-specific file extensions](platform-specific-code.md#platform-specific-extensions).

某些组件可能具有只能在一个平台上运行的属性。 所有这些组件在本文档中都会用`@platform`标注，并在页面上有一个小标志。

## 平台模块

`React Native`提供了一个用于检测应用程序运行平台的模块。如果组件只有一小部分代码需要依据平台定制，那么就可以使用此模块。

```javascript
import {Platform, StyleSheet} from 'react-native';

const styles = StyleSheet.create({
  height: Platform.OS === 'ios' ? 200 : 100,
});
```

`Platform.OS`在iOS上会返回 ios，而在Android设备或模拟器上则会返回 android。


另有一个可用的`Platform.select`方法，它可以以Platform.OS为key，从传入的对象中返回对应平台的值。

```javascript
import {Platform, StyleSheet} from 'react-native';

const styles = StyleSheet.create({
  container: {
    flex: 1,
    ...Platform.select({
      ios: {
        backgroundColor: 'red',
      },
      android: {
        backgroundColor: 'blue',
      },
    }),
  },
});
```

上面的例子里，同一个设定为`flex: 1`的容器在ios上背景色为红色，在Android上背景色则为蓝色。

由于`Platform`方法接受任何值，您也可以使用它来返回特定于平台的组件，如下所示：

```javascript
const Component = Platform.select({
  ios: () => require('ComponentIOS'),
  android: () => require('ComponentAndroid'),
})();

<Component />;
```

### 检测Android版本

在Android上，平台模块也可用于检测应用程序运行的Android平台的版本：

```javascript
import {Platform} from 'react-native';

if (Platform.Version === 25) {
  console.log('Running on Nougat!');
}
```

### 检测iOS版本

在iOS上，`Versions` 属性是 `-[UIDevice systemVersion]`的的返回值。它是当前版本操作系统的字符串，比如“10.3”。下面的例子，检测iOS版本号：

```javascript
import {Platform} from 'react-native';

const majorVersionIOS = parseInt(Platform.Version, 10);
if (majorVersionIOS <= 9) {
  console.log('Work around a change in behavior');
}
```

## 特定平台扩展名

当您的平台特定的代码更复杂时，您应该考虑将代码拆分为单独的文件。`React Native`会检测某个文件是否具有`.ios`或是`.android`的扩展名，然后根据当前运行的平台加载正确对应的文件。

例如，假设你的项目中有以下文件：

``` sh
BigButton.ios.js
BigButton.android.js
```

然后您可以按如下方式导入组件：

```javascript
const BigButton = require('./BigButton');
```

React Native 会根据运行平台自动选择正确的文件。
