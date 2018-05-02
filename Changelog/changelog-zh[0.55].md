## [0.55] React Native 中文更新日志

> 译者注：由于个人水平有限，另外翻译changelog需要阅读大量PR，翻译可能有不准确的地方，望谅解。如果发现有翻译不准确的地方，可以留言或是于Github上提交:[react-native-docsZh](https://github.com/wlfcss/react-native-docsZh)。

欢迎来到2018年3月的React Native发布！自二月份以来，超过81名社区开发者提交了247次提交。

新的亮点:

- React Native现在已经全面改为MIT license (译者注：原来的许可为BSD license)
- 已支持 Android TV 设备的开发

[![RNAndroidTVDemo](images/0.jpg)](http://www.youtube.com/watch?v=EzIQErHhY20)

- 使用原生驱动的`Animated tracking(动画跟踪)` - 示例可查 [silky smooth framerate](https://t.co/dE1KST1i3g)
- 众多的流程改进
- Bug修复

## 通用
-------

### 增加的新特性

- 增加对原生驱动的`Animated tracking(动画跟踪)`的支持，现在你能使用`useNativeDriver` 标签来跟踪其他 `Animated.Values`动画。([b48f7e5](https://github.com/facebook/react-native/commit/b48f7e5) by [@kmagiera](https://github.com/kmagiera))
- 新增一个`UTFSequence`模块用于处理常见的`Unicode`序列（比如`Emoji`）([54870e0](https://github.com/facebook/react-native/commit/54870e0) and [4761d5a](https://github.com/facebook/react-native/commit/4761d5a) by [@sahrens](https://github.com/sahrens))
- 为 **TextInput** 新增了一个 `contextMenuHidden` 属性(译者注：由于长按`TextInput` 后会出现在一个编辑菜单，比如复制、粘贴、剪切、全选等选项。新增的`contextMenuHidden`属性则可以禁止此菜单的出现) ([2dd2529](https://github.com/facebook/react-native/commit/2dd2529) by [@amhinson](https://github.com/amhinson))
- 将 `testOnly_pressed` 添加到 `TouchableHighlight` 以进行快照测试 ([3756d41](https://github.com/facebook/react-native/commit/3756d41) by [@sahrens](https://github.com/sahrens))

### 更改: 现有功能的一些变化

- React Native 现已经采用了MIT许可证 ([1490ab1](https://github.com/facebook/react-native/commit/1490ab1) and [26684cf](https://github.com/facebook/react-native/commit/26684cf) by [@sophiebits](https://github.com/sophiebits))
- HelloWorld模板现在从Git中排除 `*.jsbundle` 文件 ([2123108](https://github.com/facebook/react-native/commit/2123108) by [@aneophyte](https://github.com/aneophyte))
- `react-native-git-upgrade` 工具现在将把合并冲突的文件标记为红色 ([e53a8f7](https://github.com/facebook/react-native/commit/e53a8f7) by [@alvinthen](https://github.com/alvinthen))
- `ResolvedAssetSource` 类型将可访问所有的只读属性 ([4d0ee37](https://github.com/facebook/react-native/commit/4d0ee37) by [@sahrens](https://github.com/sahrens))
- `Flow` 的类型改进 ([b6c7e55](https://github.com/facebook/react-native/commit/b6c7e55), [b98bf1e](https://github.com/facebook/react-native/commit/b98bf1e), [80c1839](https://github.com/facebook/react-native/commit/80c1839), [70a3ece](https://github.com/facebook/react-native/commit/70a3ece), [f734357](https://github.com/facebook/react-native/commit/f734357), [a817c64](https://github.com/facebook/react-native/commit/a817c64), [3fd82d3](https://github.com/facebook/react-native/commit/3fd82d3), [cd8128b](https://github.com/facebook/react-native/commit/cd8128b), [5035af8](https://github.com/facebook/react-native/commit/5035af8), [26734a8](https://github.com/facebook/react-native/commit/26734a8), [321ba06](https://github.com/facebook/react-native/commit/321ba06), [b6b80f6](https://github.com/facebook/react-native/commit/b6b80f6), [f1316ca](https://github.com/facebook/react-native/commit/f1316ca), [2520c64](https://github.com/facebook/react-native/commit/2520c64), [214da52](https://github.com/facebook/react-native/commit/214da52), [dbdf43b](https://github.com/facebook/react-native/commit/dbdf43b), [49396aa](https://github.com/facebook/react-native/commit/49396aa), [4895c64](https://github.com/facebook/react-native/commit/4895c64), [a3c07c9](https://github.com/facebook/react-native/commit/a3c07c9), [49ffc9f](https://github.com/facebook/react-native/commit/49ffc9f), and [c129457](https://github.com/facebook/react-native/commit/c129457) by [@TheSavior](https://github.com/TheSavior), [@yungsters](https://github.com/yungsters), and [@alex288ms](https://github.com/alex288ms))
- 改进了 `WebSocket.js` 的跨平台支持 ([b9be289](https://github.com/facebook/react-native/commit/b9be289) by [@rozele](https://github.com/rozele))
- CLI创建目录将有更好的错误处理能力 ([d2817f4](https://github.com/facebook/react-native/commit/d2817f4) by [@BridgeAR](https://github.com/BridgeAR))
- 验证传递给 `createAnimatedComponent` 的组件是否能正常工作 ([10b642a](https://github.com/facebook/react-native/commit/10b642a) by [@janicduplessis](https://github.com/janicduplessis))
- 避免将emoji表情从中截断 ([9c8c597](https://github.com/facebook/react-native/commit/9c8c597) by [@Vince0613](https://github.com/Vince0613))
- 在 `UIManager` 中移除平台检查使代码能更好的适用于 `out-of-tree platforms` ([84affbd](https://github.com/facebook/react-native/commit/84affbd))
- In CLI, fix issue with `isInstalled` check for Android and references to unregister 在CLI中，修复 Android 的 `isInstalled` 参数传递检查以及link解除bug(译者注：`react-native-link` 命令存在bug，会出现无法解除link的情况，因为传递到`isInstalled`的参数存在错误)([ec88489](https://github.com/facebook/react-native/commit/ec88489) by [@rozele](https://github.com/rozele))

### 修正: 已修复的错误

- 在 `TouchableOpacity` 中，当属性为`disabled`时，透明度控制动画依旧会生效([9366ce4](https://github.com/facebook/react-native/commit/9366ce4) by [@maxkomarychev](https://github.com/maxkomarychev))
- 修复了使用 `react-native-vector-icons` 时遇到的问题(译者注：1.将测试文件夹添加进 `.npmignore` 文件中，2.将默认黑名单添加到生成设置中，以防止 `Metro` 处理不正确的引用文件。)  ([a759a44](https://github.com/facebook/react-native/commit/a759a44) and [54dc11a](https://github.com/facebook/react-native/commit/54dc11a) by [@jeanlauliac](https://github.com/jeanlauliac) and [@t4deu](https://github.com/t4deu)))
- 为 `Jest` 添加缺少的模拟 `removeEventListener` 方法 ([59c7b2c](https://github.com/facebook/react-native/commit/59c7b2c) by [@MoOx](https://github.com/MoOx))
- 修正根据纵横比进行主尺寸计算 ([f751c34](https://github.com/facebook/react-native/commit/f751c34))
- 修复了Subscribable中由于uglify-es造成的崩溃 ([b57a78c](https://github.com/facebook/react-native/commit/b57a78c) by [@iMagdy](https://github.com/iMagdy))
- 更新 `node-notifier` 依赖以修复内存泄漏问题 ([860fcd4](https://github.com/facebook/react-native/commit/860fcd4) by [@rickhanlonii](https://github.com/rickhanlonii))
- 修复 pollParams 和 link 的问题 ([ca8ce83](https://github.com/facebook/react-native/commit/ca8ce83) by [@grabbou](https://github.com/grabbou))

### 移除: 被删除的功能

- 移除各种类型(译者注：1.从StyleSheetTypes中删除未使用的导出 2.将 `StyleSheet.create` 类型为私有 3.删除内部样式表类型的使用 4.删除样式类型检测StyleProp的使用) ([b58e377](https://github.com/facebook/react-native/commit/b58e377), [ee26d9b](https://github.com/facebook/react-native/commit/ee26d9b), [d89517d](https://github.com/facebook/react-native/commit/d89517d), [852084a](https://github.com/facebook/react-native/commit/852084a) by [@TheSavior](https://github.com/TheSavior))
- 删除在`Systrace.js` 之中的 `Systrace.swizzleJSON()` ([3e141cb](https://github.com/facebook/react-native/commit/3e141cb) by [@yungsters](https://github.com/yungsters))

## Android相关

#### Android-新特性

- 新增对于 Android TV 设备的支持 ([b7bb2e5](https://github.com/facebook/react-native/commit/b7bb2e5) by [@krzysztofciombor](https://github.com/krzysztofciombor))
- 为 **Text** 和 **TextInput** 实现了样式属性 `letterSpacing`(https://github.com/facebook/react-native/commit/5898817) by [@motiz88](https://github.com/motiz88))
- 现在会显示 `Bundle` 包的下载进度 [d06e143](https://github.com/facebook/react-native/commit/d06e143) by [@janicduplessis](https://github.com/janicduplessis))
- **AndroidInfoModule** 现在会返回 Android ID (译者注：在设备首次启动时，系统会随机生成一个64位的数字，并把这个数字以16进制字符串的形式保存下来，这个16进制的字符串就是ANDROID_ID，此数字可能会因root或返厂被改变。另外某些厂商的定制系统的ANDROID_ID会有重复；或者返回值为null) ([216c8ec](https://github.com/facebook/react-native/commit/216c8ec) by [@L33tcodex0r](https://github.com/L33tcodex0r))

#### Android-Bug修复

- 修正行高计算错误 ([74e54cb](https://github.com/facebook/react-native/commit/74e54cb) by [@strindhaug](https://github.com/strindhaug))
- 修复0.53版本引入的 TextInput 方法 onKeyPress 造成的崩溃问题  ([b60a727](https://github.com/facebook/react-native/commit/b60a727) by [@joshyhargreaves](https://github.com/joshyhargreaves))
- 更新ReactAndroid构建脚本以支持 `gradle 2.3.0` ([d8bb990](https://github.com/facebook/react-native/commit/d8bb990))
- 使用 **Fetch** 方法时，允许在Android上捕获“意外URL”的异常 ([da84eba](https://github.com/facebook/react-native/commit/da84eba) by [@jcurtis](https://github.com/jcurtis))
- 修复 **TextInput** 的 `onLayout` 属性 ([8a073c1](https://github.com/facebook/react-native/commit/8a073c1) by [@rozele](https://github.com/rozele))
- 修复使用 `native navigation` 造成的 `ViewPager` 的bug (译者注：使用wix导航库导航，viewpager会失去定位焦点)  ([a1295e1](https://github.com/facebook/react-native/commit/a1295e1) by [@ruiaraujo](https://github.com/ruiaraujo))
- 修正了在本地化之中导致**DevSettingsActivity**的崩溃 ([427e464](https://github.com/facebook/react-native/commit/427e464) by [@ayc1](https://github.com/ayc1))
- 修复 `touch-responsive views` 中缩放造成的崩溃 ([67c3ad4](https://github.com/facebook/react-native/commit/67c3ad4) by [@tobycox](https://github.com/tobycox))
- 修复 “循环原生动画” 中的错误 `IllegalStateException` ([ef9d1fb](https://github.com/facebook/react-native/commit/ef9d1fb) by [@kmagiera](https://github.com/kmagiera))
- 修复关于安卓JS模块的文件引用Bug ([c20e0f9](https://github.com/facebook/react-native/commit/c20e0f9) by [@fkgozali](https://github.com/fkgozali))
- Fix ReadableNativeMap.toHashMap() for nested maps and arrays ([8a6ab14](https://github.com/facebook/react-native/commit/8a6ab14) by [@esamelson](https://github.com/esamelson))
- 修复 **Android Sanity Buck** 版本检查 ([e057322](https://github.com/facebook/react-native/commit/e057322) by [@hramos](https://github.com/hramos))
- 通过遵循 whatwg.org 的 XMLHttpRequest send()方法修复与Firestore的连接 ([d52569c](https://github.com/facebook/react-native/commit/d52569c) by [@samsafay](https://github.com/samsafay))
- 现在可以从 **SectionList** 或 **FlatList** 中设置 `invertStickyHeaders` ([3d69b5c](https://github.com/facebook/react-native/commit/3d69b5c) by [@dannycochran](https://github.com/dannycochran))

#### Android-移除

- `ReactInstanceManager#registerAdditionalPackages` 已被删除; 创建UIManager界面并在uimanager/common中获取常用类 ([6b45fb2](https://github.com/facebook/react-native/commit/6b45fb2) by [@mdvacca](https://github.com/mdvacca))


## iOS相关

#### iOS-新特性

- 关于 **InputAccessoryView**, 一个可以自定义键盘输入附件视图的组件 ([38197c8](https://github.com/facebook/react-native/commit/38197c8), [84ef7bc](https://github.com/facebook/react-native/commit/84ef7bc), and [6d9fe45](https://github.com/facebook/react-native/commit/6d9fe45) by [@PeteTheHeat](https://github.com/PeteTheHeat))
- `base-line` metric exposure for **Text** and **TextInput** ([51b3529](https://github.com/facebook/react-native/commit/51b3529), [0dbe183](https://github.com/facebook/react-native/commit/0dbe183), and [7630a61](https://github.com/facebook/react-native/commit/7630a61) by [@shergin](https://github.com/shergin))
- **DatePickerIOS** 现在有 `initialDate` 属性 ([446ce49](https://github.com/facebook/react-native/commit/446ce49))
- Expose version via `RCTVersion.h`'s `RCTGetReactNativeVersion()` ([30469ed](https://github.com/facebook/react-native/commit/30469ed) by [@LeoNatan](https://github.com/LeoNatan))
- 允许使用 `react-native run-ios --simulator ...` 来同时运行多个模拟器 ([2ad3407](https://github.com/facebook/react-native/commit/2ad3407) by [@koenpunt](https://github.com/koenpunt))
- 引入**RCTSurfaceHostingProxyRootView**以迁移到**RCTSurfaceHostingView** ([34b8876](https://github.com/facebook/react-native/commit/34b8876) by [@fkgozali](https://github.com/fkgozali))
- 新的 UIManager API 允许拦截/延迟挂载过程 ([402ae2f](https://github.com/facebook/react-native/commit/402ae2f) and [b90c1cf](https://github.com/facebook/react-native/commit/b90c1cf) by [@shergin](https://github.com/shergin))



#### iOS-更改

- tvOS 的 `onPress` 放大动画现在可以通过 `tvParallaxProperties` 属性对象使用 `pressMagnification`, `pressDuration` 和 `pressDelay` 等方法实现 ([6c353fd](https://github.com/facebook/react-native/commit/6c353fd) by [@JulienKode](https://github.com/JulienKode))


#### iOS-Bug修复

- DevLoadingView 现在支持iPhone X ([47b36d3](https://github.com/facebook/react-native/commit/47b36d3) by [@mrtnrst](https://github.com/mrtnrst))
-添加边界检查以防止 ScrollView 滚动超出 ScrollView 边界 ([16c9e5b](https://github.com/facebook/react-native/commit/16c9e5b) by [@siddhantsoni](https://github.com/siddhantsoni))
- **NetInfo** 的 `isConnected` 方法可正常使用了 ([dbafc29](https://github.com/facebook/react-native/commit/dbafc29) by [@alburdette619](https://github.com/alburdette619))
- 在 **AlertIOS** 之中, 已修复重复的 var 名称声明 ([6893a26](https://github.com/facebook/react-native/commit/6893a26))
- 可使用 `react-native run-ios --device [id]` 来选择设备运行APP ([f8fee0a](https://github.com/facebook/react-native/commit/f8fee0a) by [@jozan](https://github.com/jozan))
- 当运行命令 `run-ios` 收到错误 `Entry, ":CFBundleIdentifier", Does Not Exist` 的BUG被修复  ([5447ca6](https://github.com/facebook/react-native/commit/5447ca6) by [@blackneck](https://github.com/blackneck))
- 修复了 **iOS** 上 `Text measurent` 中的问题 ([a534672](https://github.com/facebook/react-native/commit/a534672) by [@shergin](https://github.com/shergin))
- 修复tvOS在重新加载时引起崩溃的问题 ([3a3d884](https://github.com/facebook/react-native/commit/3a3d884) by [@dlowder-salesforce](https://github.com/dlowder-salesforce))
-修正了在 **Text** 中定位嵌套视图的错误 ([7d20de4](https://github.com/facebook/react-native/commit/7d20de4) by [@shergin](https://github.com/shergin))
- 修复 blob 方法返回的结构体序列化后 body 为空的问题 ([093a78d](https://github.com/facebook/react-native/commit/093a78d) by [@janicduplessis](https://github.com/janicduplessis))
- 修复 tvOS react-native init 发布版本的bug (译者注：已将正确的依赖关系和链接器标志添加到HelloWorld模板的Xcode项目中) ([3002c4e](https://github.com/facebook/react-native/commit/3002c4e) by [@dlowder-salesforce](https://github.com/dlowder-salesforce)
- Fix RedBox from bridge reload due is not re-registering its root view ([2e51fa5](https://github.com/facebook/react-native/commit/2e51fa5) by [@fkgozali](https://github.com/fkgozali))


#### iOS-移除

- 删除 `callFunctionSync` 的实验性 APIs ([19a4a7d](https://github.com/facebook/react-native/commit/19a4a7d) by [@danzimm](https://github.com/danzimm))