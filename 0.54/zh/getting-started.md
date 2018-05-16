---
id: version-0.54-getting-started
title: 入门引导
original_id: getting-started
---

<style>
  .toggler li {
    display: inline-block;
    position: relative;
    top: 1px;
    padding: 10px;
    margin: 0px 2px 0px 2px;
    border: 1px solid #05A5D1;
    border-bottom-color: transparent;
    border-radius: 3px 3px 0px 0px;
    color: #05A5D1;
    background-color: transparent;
    font-size: 0.99em;
    cursor: pointer;
  }
  .toggler li:first-child {
    margin-left: 0;
  }
  .toggler li:last-child {
    margin-right: 0;
  }
  .toggler ul {
    width: 100%;
    display: inline-block;
    list-style-type: none;
    margin: 0;
    border-bottom: 1px solid #05A5D1;
    cursor: default;
  }
  @media screen and (max-width: 960px) {
    .toggler li,
    .toggler li:first-child,
    .toggler li:last-child {
      display: block;
      border-bottom-color: #05A5D1;
      border-radius: 3px;
      margin: 2px 0px 2px 0px;
    }
    .toggler ul {
      border-bottom: 0;
    }
  }
  .toggler a {
    display: inline-block;
    padding: 10px 5px;
    margin: 2px;
    border: 1px solid #05A5D1;
    border-radius: 3px;
    text-decoration: none !important;
  }
  .display-guide-quickstart .toggler .button-quickstart,
  .display-guide-native .toggler .button-native,
  .display-os-mac .toggler .button-mac,
  .display-os-linux .toggler .button-linux,
  .display-os-windows .toggler .button-windows,
  .display-platform-ios .toggler .button-ios,
  .display-platform-android .toggler .button-android {
    background-color: #05A5D1;
    color: white;
  }
  block { display: none; }
  .display-guide-quickstart.display-platform-ios.display-os-mac .quickstart.ios.mac,
  .display-guide-quickstart.display-platform-ios.display-os-linux .quickstart.ios.linux,
  .display-guide-quickstart.display-platform-ios.display-os-windows .quickstart.ios.windows,
  .display-guide-quickstart.display-platform-android.display-os-mac .quickstart.android.mac,
  .display-guide-quickstart.display-platform-android.display-os-linux .quickstart.android.linux,
  .display-guide-quickstart.display-platform-android.display-os-windows .quickstart.android.windows,    .display-guide-native.display-platform-ios.display-os-mac .native.ios.mac,
  .display-guide-native.display-platform-ios.display-os-linux .native.ios.linux,
  .display-guide-native.display-platform-ios.display-os-windows .native.ios.windows,
  .display-guide-native.display-platform-android.display-os-mac .native.android.mac,
  .display-guide-native.display-platform-android.display-os-linux .native.android.linux,
  .display-guide-native.display-platform-android.display-os-windows .native.android.windows {
    display: block;
  }
</style>

本文档将帮助您安装并构建您的第一个**React Native应用程序**。 如果您已经安装了React Native，则可以跳过本章节进入[Tutorial](tutorial.md)。

<div class="toggler">
  <ul role="tablist" >
    <li id="quickstart" class="button-quickstart" aria-selected="false" role="tab" tabindex="0" aria-controls="quickstarttab" onclick="displayTab('guide', 'quickstart')">
      快速开始
    </li>
    <li id="native" class="button-native" aria-selected="false" role="tab" tabindex="-1" aria-controls="nativetab" onclick="displayTab('guide', 'native')">
      构建本地开发环境
    </li>
  </ul>
</div>

<block class="quickstart mac windows linux ios android" />

[Create React Native App](https://github.com/react-community/create-react-native-app)是构建新的React Native应用程序的最简单方法。它允许你启动一个项目，而不需要安装或配置任何工具来构建本地代码 - 不需要安装Xcode或Android Studio（请参阅[注意事项](getting-started.md#caveats)）。

假如你已经安装了 [Node](https://nodejs.org/en/download/)，你可以使用 NPM 工具安装 `create-react-native-app`命令行工具：

```npm
npm install -g create-react-native-app
```

Then run the following commands to create a new React Native project called "AwesomeProject":

接下来运行以下命令来创建一个名为 `AwesomeProject` 的新React Native项目：

```npm
create-react-native-app AwesomeProject

cd AwesomeProject
npm start
```

这将为您启动一个开发服务器，并在命令行界面输出一个二维码。

## 运行您的 React Native 应用 

在您的 ios 或 android 手机上安装 [Expo](https://expo.io) 客户端，并使其与你的开发服务器处于同一局域网(能互相通信)内，启动 Expo app，扫描命令行终端打印的二维码打开您的项目。

### 修改您的APP

现在您已经成功运行该应用程序，如果需要修改它。在您选择的文本编辑器中打开App.js进行一些修改。保存更改后，手机上的应用程序会自动重新加载。

### 恭喜你

你已经成功运行并修改了你的第一个React Native APP。

<center><img src="/react-native/docs/assets/GettingStartedCongratulations.png" width="150"></img></center>

## 接下来? 

* Create React Native App also has a [user guide](https://github.com/react-community/create-react-native-app/blob/master/react-native-scripts/template/README.md) you can reference if you have questions specific to the tool.

* 如果你无法使其正常工作，请参看关于`Create React Native App`项目中的[疑难解答](https://github.com/react-community/create-react-native-app/blob/master/react-native-scripts/template/README.md#troubleshooting)。

如果您想了解更多关于React Native的内容，请继续阅读[教程](tutorial.md)。

### 在模拟器或是虚拟机上运行你的应用程序

`Create React Native App` 使您可以轻松地在物理设备上运行您的React Native APP，而无需设置开发环境。如果您想在iOS模拟器或Android虚拟设备上运行应用程序，请参阅有关使用native代码构建项目的说明，以了解如何安装Xcode以及设置Android开发环境。

一旦设置完毕，你就可以通过运行`npm run android`在Android虚拟设备上启动你的应用，或者通过运行`npm run ios`（仅限macOS）在iOS模拟器上启动你的应用。

### 注意事项

由于使用`Create React Native App`创建项目时不会生成任何原生代码，因此除了可以在Expo客户端应用程序中使用的React Native API和组件之外，但无法使用自定义的原生模块。

如果您必须嵌入原生开发代码，那么创建React Native应用程序仍然是开始的好方法。在这种情况下，你只需要使用"[eject](https://github.com/react-community/create-react-native-app/blob/master/react-native-scripts/template/README.md#ejecting-from-create-react-native-app)"来构建本地项目。如果您使用`eject`，则需要“Building Projects with Native Code”继续处理项目。

`Create React Native App` 将为您的项目配置并使用`EXPO客户端`所支持的最新 React-Native 版本。当React Native版本稳定发布后的一周左右，Expo客户端通常会获得最新的React Native版本的支持。 您可以[查看此文档](https://github.com/react-community/create-react-native-app/blob/master/VERSIONS.md)以了解哪些版本受支持

如果您将React Native集成到现有项目中，则您需要跳过`create React Native App`并学习如何设置本地开发环境。 有关为React Native配置本机开发环境的说明，请选择上面的“使用本机代码构建项目”。

<block class="native mac windows linux ios android" />

<p>如果您需要在您的项目中构建本地代码，请按下列的说明操作。 例如，如果您要将React Native集成到现有的程序中，又不想使用<a href="getting-started.html" onclick="displayTab('guide', 'quickstart')">Create React Native App`</a>，请仔细阅读本教程</p>

根据你所使用的操作系统、针对的目标平台不同，具体步骤有所不同。如果想同时开发iOS和Android也没问题，你只需要先选一个平台开始，另一个平台的环境搭建只是稍有不同。

<div class="toggler">
  <span>Development OS:</span>
  <a href="javascript:void(0);" class="button-mac" onclick="displayTab('os', 'mac')">macOS</a>
  <a href="javascript:void(0);" class="button-windows" onclick="displayTab('os', 'windows')">Windows</a>
  <a href="javascript:void(0);" class="button-linux" onclick="displayTab('os', 'linux')">Linux</a>
  <span>Target OS:</span>
  <a href="javascript:void(0);" class="button-ios" onclick="displayTab('platform', 'ios')">iOS</a>
  <a href="javascript:void(0);" class="button-android" onclick="displayTab('platform', 'android')">Android</a>
</div>

<block class="native linux windows ios" />

## Unsupported

<blockquote><p>使用本地开发环境构建IOS程序必须要使用MAC，当然你也可以前往 <a href="getting-started.md" onclick="displayTab('guide', 'quickstart')">快速开始</a> 学习使用 Create React Native App 来代替。</p></blockquote>

<block class="native mac ios" />

## 安装依赖

你需要安装 Node、Watchman,react-native命令行工具和xcode。

虽然你可以使用任意编辑器（IDE）来开发你的App，但你必须要安装 **xcode** 才能完整构建适用于iOS的React Native应用程序。

<block class="native mac android" />

## 安装依赖

你需要安装 Node、Watchman,react-native命令行工具以及JDK和Android Studio。

<block class="native linux android" />

## 安装依赖

你需要安装 Node、react-native命令行工具以及JDK和Android Studio。

<block class="native windows android" />

## 安装依赖

你需要安装 Node、react-native命令行工具、python2以及JDK和Android Studio。

<block class="native mac windows linux android" />

While you can use any editor of your choice to develop your app, you will need to install Android Studio in order to set up the necessary tooling to build your React Native app for Android.

虽然你可以使用任意编辑器（IDE）来开发你的App，你最好安装 **Android Studio** 以自动配置安卓的相关依赖包及组件。

<block class="native mac ios android" />

### Node, Watchman

We recommend installing Node and Watchman using [Homebrew](http://brew.sh/). Run the following commands in a Terminal after installing Homebrew:

我们推荐使用 [Homebrew](http://brew.sh/) 来安装 Node 和 Watchman ,在安装好Homebrew之后你可以通过下列命令安装：

```
brew install node
brew install watchman
```

如果你已经安装了 Node 环境，请确认其版本 >= 8.0

[Watchman](https://facebook.github.io/watchman) is a tool by Facebook for watching changes in the filesystem. It is highly recommended you install it for better performance.

[Watchman](https://facebook.github.io/watchman) 是一个由Facebook开发的实时监控开发文件变更的工具，我们强烈建议你安装此工具以获得更好的开发体验。

<block class="native linux android" />

### Node

Follow the [installation instructions for your Linux distribution](https://nodejs.org/en/download/package-manager/) to install Node 6 or newer.

<block class='native windows android' />

### Node, Python2, JDK

我们推荐使用[Chocolatey](https://chocolatey.org)来安装 Node 和 Python2,这是一个倍受欢迎的windows包管理工具。

React Native 仍然需要安装新版本的[Java SE Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html),当然，你也可以通过 `Chocolatey` 进行安装。

请使用管理员权限运行windows命令行(右键点击CMD快捷方式选择“使用管理员权限运行”)，再运行以下命令：

```powershell
choco install -y nodejs.install python2 jdk8
```

如果你已经安装了 Node 环境，请确认其版本 >= 8.0，如果你已经安装了 JDK 环境，请确认其版本 >= 8.0

> 当然你也可以在[Node官方网站](https://nodejs.org/en/download/)上找到其它版本。

<block class="native mac ios android" />

### React Native CLI（命令行工具）

Node包含了NPM(包管理器),你可以使用此工具安装 `React Native CLI`

在命令行里运行下列命令

```
npm install -g react-native-cli
```

> 如果遇到`Cannot find module 'npmlog'`的错误，请尝试直接安装npm：`curl -0 -L https://npmjs.org/install.sh | sudo sh`。

<block class="native windows linux android" />

### The React Native CLI

Node comes with npm, which lets you install the React Native command line interface.

Run the following command in a Command Prompt or shell:

```powershell
npm install -g react-native-cli
```

> If you get an error like `Cannot find module 'npmlog'`, try installing npm directly: `curl -0 -L https://npmjs.org/install.sh | sudo sh`.

<block class="native mac ios" />

### Xcode

The easiest way to install Xcode is via the [Mac App Store](https://itunes.apple.com/us/app/xcode/id497799835?mt=12). Installing Xcode will also install the iOS Simulator and all the necessary tools to build your iOS app.

If you have already installed Xcode on your system, make sure it is version 8 or higher.

#### Command Line Tools

You will also need to install the Xcode Command Line Tools. Open Xcode, then choose "Preferences..." from the Xcode menu. Go to the Locations panel and install the tools by selecting the most recent version in the Command Line Tools dropdown.

![Xcode Command Line Tools](/react-native/docs/assets/GettingStartedXcodeCommandLineTools.png)

<block class="native mac linux android" />

### Java Development Kit

React Native requires a recent version of the Java SE Development Kit (JDK). [Download and install JDK 8 or newer](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) if needed.

<block class="native mac linux windows android" />

### Android development environment

Setting up your development environment can be somewhat tedious if you're new to Android development. If you're already familiar with Android development, there are a few things you may need to configure. In either case, please make sure to carefully follow the next few steps.

<block class="native mac windows linux android" />

#### 1. Install Android Studio

[Download and install Android Studio](https://developer.android.com/studio/index.html). Choose a "Custom" setup when prompted to select an installation type. Make sure the boxes next to all of the following are checked:

<block class="native mac windows android" />

* `Android SDK`
* `Android SDK Platform`
* `Performance (Intel ® HAXM)`
* `Android Virtual Device`

<block class="native linux android" />

* `Android SDK`
* `Android SDK Platform`
* `Android Virtual Device`

<block class="native mac windows linux android" />

Then, click "Next" to install all of these components.

> If the checkboxes are grayed out, you will have a chance to install these components later on.

Once setup has finalized and you're presented with the Welcome screen, proceed to the next step.

#### 2. Install the Android SDK

Android Studio installs the latest Android SDK by default. Building a React Native app with native code, however, requires the `Android 6.0 (Marshmallow)` SDK in particular. Additional Android SDKs can be installed through the SDK Manager in Android Studio.

The SDK Manager can be accessed from the "Welcome to Android Studio" screen. Click on "Configure", then select "SDK Manager".

<block class="native mac android" />

![Android Studio Welcome](/react-native/docs/assets/GettingStartedAndroidStudioWelcomeMacOS.png)

<block class="native windows android" />

![Android Studio Welcome](/react-native/docs/assets/GettingStartedAndroidStudioWelcomeWindows.png)

<block class="native mac windows linux android" />

> The SDK Manager can also be found within the Android Studio "Preferences" dialog, under **Appearance & Behavior** → **System Settings** → **Android SDK**.

Select the "SDK Platforms" tab from within the SDK Manager, then check the box next to "Show Package Details" in the bottom right corner. Look for and expand the `Android 6.0 (Marshmallow)` entry, then make sure the following items are all checked:

* `Google APIs`
* `Android SDK Platform 23`
* `Intel x86 Atom_64 System Image`
* `Google APIs Intel x86 Atom_64 System Image`

<block class="native mac android" />

![Android SDK Manager](/react-native/docs/assets/GettingStartedAndroidSDKManagerMacOS.png)

<block class="native windows android" />

![Android SDK Manager](/react-native/docs/assets/GettingStartedAndroidSDKManagerWindows.png)

<block class="native windows mac linux android" />

Next, select the "SDK Tools" tab and check the box next to "Show Package Details" here as well. Look for and expand the "Android SDK Build-Tools" entry, then make sure that `23.0.1` is selected.

<block class="native mac android" />

![Android SDK Manager - 23.0.1 Build Tools](/react-native/docs/assets/GettingStartedAndroidSDKManagerSDKToolsMacOS.png)

<block class="native windows android" />

![Android SDK Manager - 23.0.1 Build Tools](/react-native/docs/assets/GettingStartedAndroidSDKManagerSDKToolsWindows.png)

<block class="native windows mac linux android" />

Finally, click "Apply" to download and install the Android SDK and related build tools.

<block class="native mac android" />

![Android SDK Manager - Installs](/react-native/docs/assets/GettingStartedAndroidSDKManagerInstallsMacOS.png)

<block class="native windows android" />

![Android SDK Manager - Installs](/react-native/docs/assets/GettingStartedAndroidSDKManagerInstallsWindows.png)

<block class="native mac windows linux android" />

#### 3. Configure the ANDROID_HOME environment variable

The React Native tools require some environment variables to be set up in order to build apps with native code.

<block class="native mac linux android" />

Add the following lines to your `$HOME/.bash_profile` config file:

<block class="native mac android" />

```
export ANDROID_HOME=$HOME/Library/Android/sdk
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/platform-tools
```

<block class="native linux android" />

```
export ANDROID_HOME=$HOME/Android/Sdk
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/platform-tools
```

<block class="native mac linux android" />

> `.bash_profile` is specific to `bash`. If you're using another shell, you will need to edit the appropriate shell-specific config file.

Type `source $HOME/.bash_profile` to load the config into your current shell. Verify that ANDROID_HOME has been added to your path by running `echo $PATH`.

> Please make sure you use the correct Android SDK path. You can find the actual location of the SDK in the Android Studio "Preferences" dialog, under **Appearance & Behavior** → **System Settings** → **Android SDK**.

<block class="native windows android" />

Open the System pane under **System and Security** in the Control Panel, then click on **Change settings...**. Open the **Advanced** tab and click on **Environment Variables...**. Click on **New...** to create a new `ANDROID_HOME` user variable that points to the path to your Android SDK:

![ANDROID_HOME Environment Variable](/react-native/docs/assets/GettingStartedAndroidEnvironmentVariableANDROID_HOME.png)

The SDK is installed, by default, at the following location:

```powershell
c:\Users\YOUR_USERNAME\AppData\Local\Android\Sdk
```

You can find the actual location of the SDK in the Android Studio "Preferences" dialog, under **Appearance & Behavior** → **System Settings** → **Android SDK**.

Open a new Command Prompt window to ensure the new environment variable is loaded before proceeding to the next step.

<block class="native linux android" />

### Watchman (optional)

Follow the [Watchman installation guide](https://facebook.github.io/watchman/docs/install.html#buildinstall) to compile and install Watchman from source.

> [Watchman](https://facebook.github.io/watchman/docs/install.html) is a tool by Facebook for watching changes in the filesystem. It is highly recommended you install it for better performance, but it's alright to skip this if you find the process to be tedious.

<block class="native mac ios" />

## Creating a new application

Use the React Native command line interface to generate a new React Native project called "AwesomeProject":

```
react-native init AwesomeProject
```

This is not necessary if you are integrating React Native into an existing application, if you "ejected" from Create React Native App, or if you're adding iOS support to an existing React Native project (see [Platform Specific Code](platform-specific-code.md)).

<block class="native mac windows linux android" />

## Creating a new application

Use the React Native command line interface to generate a new React Native project called "AwesomeProject":

```
react-native init AwesomeProject
```

This is not necessary if you are integrating React Native into an existing application, if you "ejected" from Create React Native App, or if you're adding Android support to an existing React Native project (see [Platform Specific Code](platform-specific-code.md)).

<block class="native mac windows linux android" />

## Preparing the Android device

You will need an Android device to run your React Native Android app. This can be either a physical Android device, or more commonly, you can use an Android Virtual Device which allows you to emulate an Android device on your computer.

Either way, you will need to prepare the device to run Android apps for development.

### Using a physical device

If you have a physical Android device, you can use it for development in place of an AVD by plugging it in to your computer using a USB cable and following the instructions [here](running-on-device.md).

### Using a virtual device

You can see the list of available Android Virtual Devices (AVDs) by opening the "AVD Manager" from within Android Studio. Look for an icon that looks like this:

![Android Studio AVD Manager](/react-native/docs/assets/GettingStartedAndroidStudioAVD.png)

If you have just installed Android Studio, you will likely need to [create a new AVD](https://developer.android.com/studio/run/managing-avds.html). Select "Create Virtual Device...", then pick any Phone from the list and click "Next".

<block class="native windows android" />

![Android Studio AVD Manager](/react-native/docs/assets/GettingStartedCreateAVDWindows.png)

<block class="native mac android" />

![Android Studio AVD Manager](/react-native/docs/assets/GettingStartedCreateAVDMacOS.png)

<block class="native mac windows linux android" />

Select the "x86 Images" tab, then look for the **Marshmallow** API Level 23, x86_64 ABI image with a Android 6.0 (Google APIs) target.

<block class="native linux android" />

> We recommend configuring [VM acceleration](https://developer.android.com/studio/run/emulator-acceleration.html#vm-linux) on your system to improve performance. Once you've followed those instructions, go back to the AVD Manager.

<block class="native windows android" />

![Install HAXM](/react-native/docs/assets/GettingStartedCreateAVDx86Windows.png)

> If you don't have HAXM installed, click on "Install HAXM" or follow [these instructions](https://github.com/intel/haxm/wiki/Installation-Instructions-on-Windows) to set it up, then go back to the AVD Manager.

![AVD List](/react-native/docs/assets/GettingStartedAVDManagerWindows.png)

<block class="native mac android" />

![Install HAXM](/react-native/docs/assets/GettingStartedCreateAVDx86MacOS.png)

> If you don't have HAXM installed, follow [these instructions](https://github.com/intel/haxm/wiki/Installation-Instructions-on-macOS) to set it up, then go back to the AVD Manager.

![AVD List](/react-native/docs/assets/GettingStartedAVDManagerMacOS.png)

<block class="native mac windows linux android" />

Click "Next" then "Finish" to create your AVD. At this point you should be able to click on the green triangle button next to your AVD to launch it, then proceed to the next step.

<block class="native mac ios" />

## Running your React Native application

Run `react-native run-ios` inside your React Native project folder:

```
cd AwesomeProject
react-native run-ios
```

You should see your new app running in the iOS Simulator shortly.

![AwesomeProject on iOS](/react-native/docs/assets/GettingStartediOSSuccess.png)

`react-native run-ios` is just one way to run your app. You can also run it directly from within Xcode or [Nuclide](https://nuclide.io/).

> If you can't get this to work, see the [Troubleshooting](troubleshooting.md#content) page.

### Running on a device

The above command will automatically run your app on the iOS Simulator by default. If you want to run the app on an actual physical iOS device, please follow the instructions [here](running-on-device.md).

<block class="native mac windows linux android" />

## Running your React Native application

Run `react-native run-android` inside your React Native project folder:

```
cd AwesomeProject
react-native run-android
```

If everything is set up correctly, you should see your new app running in your Android emulator shortly.

<block class="native mac android" />

![AwesomeProject on Android](/react-native/docs/assets/GettingStartedAndroidSuccessMacOS.png)

<block class="native windows android" />

![AwesomeProject on Android](/react-native/docs/assets/GettingStartedAndroidSuccessWindows.png)

<block class="native mac windows linux android" />

`react-native run-android` is just one way to run your app - you can also run it directly from within Android Studio or [Nuclide](https://nuclide.io/).

> If you can't get this to work, see the [Troubleshooting](troubleshooting.md#content) page.

<block class="native mac ios android" />

### Modifying your app

Now that you have successfully run the app, let's modify it.

<block class="native mac ios" />

* Open `App.js` in your text editor of choice and edit some lines.
* Hit `⌘R` in your iOS Simulator to reload the app and see your changes!

<block class="native mac android" />

* Open `App.js` in your text editor of choice and edit some lines.
* Press the `R` key twice or select `Reload` from the Developer Menu (`⌘M`) to see your changes!

<block class="native windows linux android" />

### Modifying your app

Now that you have successfully run the app, let's modify it.

* Open `App.js` in your text editor of choice and edit some lines.
* Press the `R` key twice or select `Reload` from the Developer Menu (`Ctrl + M`) to see your changes!

<block class="native mac ios android" />

### That's it!

Congratulations! You've successfully run and modified your first React Native app.

<center><img src="/react-native/docs/assets/GettingStartedCongratulations.png" width="150"></img></center>

<block class="native windows linux android" />

### That's it!

Congratulations! You've successfully run and modified your first React Native app.

<center><img src="/react-native/docs/assets/GettingStartedCongratulations.png" width="150"></img></center>

<block class="native mac ios" />

## Now what?

* Turn on [Live Reload](debugging.md#reloading-javascript) in the Developer Menu. Your app will now reload automatically whenever you save any changes!

* If you want to add this new React Native code to an existing application, check out the [Integration guide](integration-with-existing-apps.md).

If you're curious to learn more about React Native, continue on to the [Tutorial](tutorial.md).

<block class="native windows linux mac android" />

## Now what?

* Turn on [Live Reload](debugging.md#reloading-javascript) in the Developer Menu. Your app will now reload automatically whenever you save any changes!

* If you want to add this new React Native code to an existing application, check out the [Integration guide](integration-with-existing-apps.md).

If you're curious to learn more about React Native, continue on to the [Tutorial](tutorial.md).

<script>
  function displayTab(type, value) {
    var container = document.getElementsByTagName('block')[0].parentNode;
    container.className = 'display-' + type + '-' + value + ' ' +
      container.className.replace(RegExp('display-' + type + '-[a-z]+ ?'), '');
  }
  function convertBlocks() {
    // Convert <div>...<span><block /></span>...</div>
    // Into <div>...<block />...</div>
    var blocks = document.querySelectorAll('block');
    for (var i = 0; i < blocks.length; ++i) {
      var block = blocks[i];
      var span = blocks[i].parentNode;
      var container = span.parentNode;
      container.insertBefore(block, span);
      container.removeChild(span);
    }
    // Convert <div>...<block />content<block />...</div>
    // Into <div>...<block>content</block><block />...</div>
    blocks = document.querySelectorAll('block');
    for (var i = 0; i < blocks.length; ++i) {
      var block = blocks[i];
      while (
        block.nextSibling &&
        block.nextSibling.tagName !== 'BLOCK'
      ) {
        block.appendChild(block.nextSibling);
      }
    }
  }
  function guessPlatformAndOS() {
    if (!document.querySelector('block')) {
      return;
    }
    // If we are coming to the page with a hash in it (i.e. from a search, for example), try to get
    // us as close as possible to the correct platform and dev os using the hashtag and block walk up.
    var foundHash = false;
    if (
      window.location.hash !== '' &&
      window.location.hash !== 'content'
    ) {
      // content is default
      var hashLinks = document.querySelectorAll(
        'a.hash-link'
      );
      for (
        var i = 0;
        i < hashLinks.length && !foundHash;
        ++i
      ) {
        if (hashLinks[i].hash === window.location.hash) {
          var parent = hashLinks[i].parentElement;
          while (parent) {
            if (parent.tagName === 'BLOCK') {
              // Could be more than one target os and dev platform, but just choose some sort of order
              // of priority here.
              // Dev OS
              if (parent.className.indexOf('mac') > -1) {
                displayTab('os', 'mac');
                foundHash = true;
              } else if (
                parent.className.indexOf('linux') > -1
              ) {
                displayTab('os', 'linux');
                foundHash = true;
              } else if (
                parent.className.indexOf('windows') > -1
              ) {
                displayTab('os', 'windows');
                foundHash = true;
              } else {
                break;
              }
              // Target Platform
              if (parent.className.indexOf('ios') > -1) {
                displayTab('platform', 'ios');
                foundHash = true;
              } else if (
                parent.className.indexOf('android') > -1
              ) {
                displayTab('platform', 'android');
                foundHash = true;
              } else {
                break;
              }
              // Guide
              if (parent.className.indexOf('native') > -1) {
                displayTab('guide', 'native');
                foundHash = true;
              } else if (
                parent.className.indexOf('quickstart') > -1
              ) {
                displayTab('guide', 'quickstart');
                foundHash = true;
              } else {
                break;
              }
              break;
            }
            parent = parent.parentElement;
          }
        }
      }
    }
    // Do the default if there is no matching hash
    if (!foundHash) {
      var isMac = navigator.platform === 'MacIntel';
      var isWindows = navigator.platform === 'Win32';
      displayTab('platform', isMac ? 'ios' : 'android');
      displayTab(
        'os',
        isMac ? 'mac' : isWindows ? 'windows' : 'linux'
      );
      displayTab('guide', 'quickstart');
      displayTab('language', 'objc');
    }
  }
  convertBlocks();
  guessPlatformAndOS();
</script>
