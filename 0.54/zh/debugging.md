---
id: version-0.54-debugging
title: 调试
original_id: debugging
---

## 开启调试快捷键

React Native 支持多种在ios模拟器上的快捷键，下面将会详细介绍，若要启动它们，打开`Hardware`菜单，选择`Keyboard`选项卡，确保 `Connect Hardware Keyboard` 选项开启。

## 访问APP内的开发菜单

您可以通过摇晃设备或在IOS模拟器的`Hardware`菜单中选择“Shake Gesture”选项来调出开发者菜单，另外，如果是在iOS模拟器中运行，还可以按下`⌘ + D` 快捷键，Android模拟器对应的则是`⌘ + M`。当然，如果是Android,您还可以通过adb工具运行命令`adb shell input keyevent 82`来打开开发者菜单（82是菜单代码）。

![](react-native/docs/assets/DeveloperMenu.png)

> 注：在非开发调试版本（release/production builds）中开发者菜单会被关闭。

## 刷新 JavaScript

在React Native开发中，每次改动后您再也不需要等待漫长的重编译，通过`reloading javascripts(重新加载js)`将可以简单快速的查看界面/功能变化，具体的操作就是在开发菜单中点击"Reload"选项。也可以在iOS模拟器中按下`⌘ + R` ，Android模拟器上对应的则是按两下`R`。

### 自动刷新

您可以在代码更改时自动重新加载应用程序，从而加快开发速度。 通过从开发者菜单中选择“启用Live Reload”可以启用自动重新加载。

您甚至可以更进一步，通过“开发者菜单”启用[Hot Reloading](https://facebook.github.io/react-native/blog/2016/03/24/introducing-hot-reloading.html)功能，将新版本的文件自动注入到JavaScript包中，从而让您的应用程序继续运行，这将允许您通过重新加载来保持应用程序的状态。

> 有些情况下`Hot Reloading`并不能完好的重加载。 如果遇到问题，请使用完全重载来重启您的应用。

You will need to rebuild your app for changes to take effect in certain situations:
在某些情况下，您必须重新编译您的应用，才能使改动生效：

* 您将新资源添加到您的 react-native 程序中，例如iOS上的`Images.xcassets`中的图像或Android上的 `res / drawable`。

* 更改了任何的原生代码（objective-c/swift/java）

## 应用内的错误与警告

红色错误提示或黄色警告都只会在开发版本中显示，在正式的release包中是不会显示的。

### 红色错误

应用内的报错会以全屏红色显示在应用中（调试模式下），我们称为红屏（red box）报错。你可以使用 `console.error()` 来手动触发红屏错误。

### 黄色警告

警告将以黄色背景显示在屏幕上。 这些警报被称为 `YellowBoxes`。 点击警告可以查看详情或是忽略掉他们。

和红屏报警相同的是你也可以使用console.warn()来手动触发黄屏警告。

通过使用console.disableYellowBox = true;可以在开发过程中禁用YellowBoxes。 通过设置应忽略的前缀数组，可以忽略特定的警告：

```javascript
import {YellowBox} from 'react-native';
YellowBox.ignoreWarnings(['Warning: ...']);
```

在 CI/Xcode 之中，可以使用 `IS_TESTING` 等环境变量来控制（启用/禁用） YellowBoxes

> 发布（production）版本中将自动禁用 RedBoxes 和 YellowBoxes

## Chrome 开发者工具

在开发者菜单中选择"Debug JS Remotely"选项，即可以开始在Chrome中调试JavaScript代码。点击这个选项的同时会自动打开调试页面 http://localhost:8081/debugger-ui.

在Chrome菜单中选择 `Tools → Developer Tools`可以打开[开发者工具](https://developer.chrome.com/devtools)，当然你也可以通过键盘快捷键来打开（Mac上`Command⌘ + Option⌥ + I`，Windows上是`Ctrl + Shift + I`或是`F12`）。同时打开[有异常时暂停](http://stackoverflow.com/questions/2233339/javascript-is-there-a-way-to-get-chrome-to-break-on-all-errors/17324511#17324511)（`Pause On Caught Exceptions`）选项，能够获得更好的开发体验。

> 注意：React Developer Tools 的 Chrome扩展程序不适用于React Native，但您可以改用rn的独立版本。 请阅读[本章节](debugging.md#react-developer-tools)。

### 使用自定义的JavaScript调试工具

如果想用其他的JavaScript调试工具来代替 Chrome 扩展调试工具，可以设置一个名为`REACT_DEBUGGER`的环境变量，其值为启动自定义调试器的命令。调试的流程依然是从开发者菜单中的"Debug JS Remotely"选项开始。

被指定的调试器需要知道项目所在的目录（可以一次传递多个目录参数，以空格隔开）。例如，如果你设定了 `REACT_DEBUGGER="node /path/to/launchDebugger.js --port 2345 --type ReactNative"`, 那么启动调试器的命令就应该是 `node /path/to/launchDebugger.js --port 2345 --type ReactNative /path/to/reactNative/app`

> 以这种方式执行的调试器最好是一个短进程（short-lived processes），同时最好也不要有超过200k的文字输出。

## React Developer Tools

您可以使用 [React Developer Tools](https://github.com/facebook/react-devtools/tree/master/packages/react-devtools) 来对react-naitve进行调试。 在使用前，您需要在全局安装 `react-devtools` 软件包：

```
npm install -g react-devtools
```

安装完成后，运行命令 `react-devtools` 即可启动此工具：

```
react-devtools
```

![React DevTools](react-native/docs/assets/ReactDevTools.png)

此工具应该仅需数秒就可以连接到你的模拟器

> 注意：如果您不想使用全局安装，可以将`react-devtools`添加为项目依赖项。 使用`npm install --save-dev react-devtools`将`react-devtools`包添加到你的项目中，然后在你的`package.json`脚本部分添加`“react-devtools”：“react-devtools”`，然后运行`npm run reac-devtoolst` 进行调试。

### 使用 React Native Inspector 进行界面的调试

打开APP内部的 开发菜单 选择 "Show Inspector"，将会打开一个UI信息解析的覆盖层，允许你点击任何UI元素并查看关于它的信息：

![React Native Inspector](react-native/docs/assets/Inspector.gif)

但是，如果`react-devtools`正在运行，`Inspector`将进入特殊的折叠模式，而将DevTools作为主要UI。 在这种模式下，单击模拟器中的某些内容才可以调出DevTools中的相关组件：

![React DevTools Inspector Integration](react-native/docs/assets/ReactDevToolsInspector.gif)

你可以在开发者菜单中选择 `"Hide Inspector"` 以退出此模式

### 组件检视模式

在Chrome中调试JavaScript时，您可以在浏览器控制台中检查React组件的属性（Props）和状态（state）。

首先，按照Chrome中的调试说明打开Chrome的控制台

**必须确保**Chrome控制台左上角的下拉菜单显示`debuggerWorker.js`。

然后在React DevTools中选择一个React组件。调试界面顶部有一个搜索框，可帮助您找到一个名称。 只要您选择它，它将在Chrome控制台中以 `$r` 的形式提供，让您检查它的道具，状态和实例属性。

![React DevTools Chrome Console Integration](react-native/docs/assets/ReactDevToolsDollarR.gif)

## 性能监测

你可以在开发者菜单中选择"Pref Monitor"选项以开启一个悬浮层，来帮助你对性能问题进行调试

<hr style="margin-top:25px; margin-bottom:25px;"/>

# Debugging in Ejected Apps

<div class="banner-crna-ejected" style="margin-top:25px">
  <h3>原生开发项目</h3>
  <p>
    本指南的其余部分仅适用于使用<code>react-native init</code>创建的项目或使用Create React Native App创建的项目，相关的更多信息，请参阅 <a href="https://github.com/react-community/create-react-native-app/blob/master/EJECTING.md" target="_blank">Create React Native App 库指南</a>。
  </p>
</div>

## 访问控制台日志

在运行RN应用时，你可以在终端中运行如下命令来查看控制台的日志：

```
$ react-native log-ios
$ react-native log-android
```

此外，你也可以在iOS模拟器的菜单中选择Debug → Open System Log...来查看。如果是Android应用，无论是运行在模拟器或是真机上，都可以通过在终端命令行里运行adb logcat *:S ReactNative:V ReactNativeJS:V命令来查看。

> 如果您使用的是 Create React Native App，则控制台日志会与打包程序在相同的终端中输出。

## 使用 Chrome 开发者工具调试设备

> 如果您使用的是 Create React Native App, 则程序将为你自动完成配置。

如果是 iOS 设备，请打开文件 [`RCTWebSocketExecutor.m`](https://github.com/facebook/react-native/blob/master/Libraries/WebSocket/RCTWebSocketExecutor.m) 将 "localhost" 修改为您计算机的ip,并在开发者菜单中选择 "Debug JS Remotely"

在通过USB连接的Android 5.0设备上，您可以使用[`adb`命令行工具](http://developer.android.com/tools/help/adb.html) 来设置端口转发：

`adb reverse tcp:8081 tcp:8081`

或者，您可以从开发菜单中选择“Dev Settings”，然后选择更新 “Debug server host for device” 设置以匹配您的计算机的IP地址。

> 如果遇到任何问题，这很可能是您的某个Chrome扩展程序导致的，因为他们可能会以某种意想不到的方式与调试器进行交互。请尝试禁用所有扩展并逐个重新启用它们，直到找到有问题的扩展。

### 在Android上使用 [Stetho](http://facebook.github.io/stetho/) 进行调试

按照本指南启用`Stetho for Debug`模式：

1. 在 `android/app/build.gradle` 文件的 `dependencies` 中添加：:

   ```gradle
    debugCompile 'com.facebook.stetho:stetho:1.5.0'
    debugCompile 'com.facebook.stetho:stetho-okhttp3:1.5.0'
   ```

> 以上配置仅限于 Stetho v1.5.0。 如果有更新的版本可用，你可以在http://facebook.github.io/stetho/上查看

2. 创建以下Java类来包装Stetho调用，一个用于发布，另一个用于调试：

   ```java
   // android/app/src/release/java/com/{yourAppName}/StethoWrapper.java

   public class StethoWrapper {

       public static void initialize(Context context) {
           // NO_OP
       }

       public static void addInterceptor() {
           // NO_OP
       }
   }
   ```

   ```java
   // android/app/src/debug/java/com/{yourAppName}/StethoWrapper.java

   public class StethoWrapper {
       public static void initialize(Context context) {
         Stetho.initializeWithDefaults(context);
       }

       public static void addInterceptor() {
         OkHttpClient client = OkHttpClientProvider.getOkHttpClient()
                .newBuilder()
                .addNetworkInterceptor(new StethoInterceptor())
                .build();

         OkHttpClientProvider.replaceOkHttpClient(client);
       }
   }
   ```

3. 打开 `android/app/src/main/java/com/{yourAppName}/MainApplication.java` 重写原有的 `onCreate` 方法:

```java
  public void onCreate() {
      super.onCreate();

      if (BuildConfig.DEBUG) {
          StethoWrapper.initialize(this);
          StethoWrapper.addInterceptor();
      }

      SoLoader.init(this, /* native exopackage */ false);
    }
```

4. 在Android Studio中打开项目并解决所有的依赖问题。 选中红线报错的部分，ID将E应引导您完成依赖的安装。

5. 运行 `react-native run-android`.

6. 新建一个的chrome页面, 打开: `chrome://inspect`, 然后点击“Powered by Stetho”旁边的“Inspect device”选项。

## 调试原生代码

在和原生代码打交道时（比如编写原生模块），可以直接从Android Studio或是Xcode中启动应用，并利用这些IDE的内置功能来调试（比如设置断点）。这一方面和开发原生应用并无二致。
