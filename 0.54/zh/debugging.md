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

You can use [the standalone version of React Developer Tools](https://github.com/facebook/react-devtools/tree/master/packages/react-devtools) to debug the React component hierarchy. To use it, install the `react-devtools` package globally:

```
npm install -g react-devtools
```

Now run `react-devtools` from the terminal to launch the standalone DevTools app:

```
react-devtools
```

![React DevTools](react-native/docs/assets/ReactDevTools.png)

It should connect to your simulator within a few seconds.

> Note: if you prefer to avoid global installations, you can add `react-devtools` as a project dependency. Add the `react-devtools` package to your project using `npm install --save-dev react-devtools`, then add `"react-devtools": "react-devtools"` to the `scripts` section in your `package.json`, and then run `npm run react-devtools` from your project folder to open the DevTools.

### Integration with React Native Inspector

Open the in-app developer menu and choose "Show Inspector". It will bring up an overlay that lets you tap on any UI element and see information about it:

![React Native Inspector](/react-native/docs/assets/Inspector.gif)

However, when `react-devtools` is running, Inspector will enter a special collapsed mode, and instead use the DevTools as primary UI. In this mode, clicking on something in the simulator will bring up the relevant components in the DevTools:

![React DevTools Inspector Integration](/react-native/docs/assets/ReactDevToolsInspector.gif)

You can choose "Hide Inspector" in the same menu to exit this mode.

### Inspecting Component Instances

When debugging JavaScript in Chrome, you can inspect the props and state of the React components in the browser console.

First, follow the instructions for debugging in Chrome to open the Chrome console.

Make sure that the dropdown in the top left corner of the Chrome console says `debuggerWorker.js`. **This step is essential.**

Then select a React component in React DevTools. There is a search box at the top that helps you find one by name. As soon as you select it, it will be available as `$r` in the Chrome console, letting you inspect its props, state, and instance properties.

![React DevTools Chrome Console Integration](/react-native/docs/assets/ReactDevToolsDollarR.gif)

## Performance Monitor

You can enable a performance overlay to help you debug performance problems by selecting "Perf Monitor" in the Developer Menu.

<hr style="margin-top:25px; margin-bottom:25px;"/>

# Debugging in Ejected Apps

<div class="banner-crna-ejected" style="margin-top:25px">
  <h3>Projects with Native Code Only</h3>
  <p>
    The remainder of this guide only applies to projects made with <code>react-native init</code>
    or to those made with Create React Native App which have since ejected. For
    more information about ejecting, please see
    the <a href="https://github.com/react-community/create-react-native-app/blob/master/EJECTING.md" target="_blank">guide</a> on
    the Create React Native App repository.
  </p>
</div>

## Accessing console logs

You can display the console logs for an iOS or Android app by using the following commands in a terminal while the app is running:

```
$ react-native log-ios
$ react-native log-android
```

You may also access these through `Debug → Open System Log...` in the iOS Simulator or by running `adb logcat *:S ReactNative:V ReactNativeJS:V` in a terminal while an Android app is running on a device or emulator.

> If you're using Create React Native App, console logs already appear in the same terminal output as the packager.

## Debugging on a device with Chrome Developer Tools

> If you're using Create React Native App, this is configured for you already.

On iOS devices, open the file [`RCTWebSocketExecutor.m`](https://github.com/facebook/react-native/blob/master/Libraries/WebSocket/RCTWebSocketExecutor.m) and change "localhost" to the IP address of your computer, then select "Debug JS Remotely" from the Developer Menu.

On Android 5.0+ devices connected via USB, you can use the [`adb` command line tool](http://developer.android.com/tools/help/adb.html) to setup port forwarding from the device to your computer:

`adb reverse tcp:8081 tcp:8081`

Alternatively, select "Dev Settings" from the Developer Menu, then update the "Debug server host for device" setting to match the IP address of your computer.

> If you run into any issues, it may be possible that one of your Chrome extensions is interacting in unexpected ways with the debugger. Try disabling all of your extensions and re-enabling them one-by-one until you find the problematic extension.

### Debugging with [Stetho](http://facebook.github.io/stetho/) on Android

Follow this guide to enable Stetho for Debug mode:

1. In `android/app/build.gradle`, add these lines in the `dependencies` section:

   ```gradle
    debugCompile 'com.facebook.stetho:stetho:1.5.0'
    debugCompile 'com.facebook.stetho:stetho-okhttp3:1.5.0'
   ```

> The above will configure Stetho v1.5.0. You can check at http://facebook.github.io/stetho/ if a newer version is available.

2. Create the following Java classes to wrap the Stetho call, one for release and one for debug:

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

3. Open `android/app/src/main/java/com/{yourAppName}/MainApplication.java` and replace the original `onCreate` function:

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

4. Open the project in Android Studio and resolve any dependency issues. The IDE should guide you through this steps after hovering your pointer over the red lines.

5. Run `react-native run-android`.

6. In a new Chrome tab, open: `chrome://inspect`, then click on the 'Inspect device' item next to "Powered by Stetho".

## Debugging native code

When working with native code, such as when writing native modules, you can launch the app from Android Studio or Xcode and take advantage of the native debugging features (setting up breakpoints, etc.) as you would in case of building a standard native app.
