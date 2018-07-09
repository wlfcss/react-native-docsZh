## [0.56] React Native 中文更新日志

欢迎阅读React Native的2018年6月的更新日志！自3月份以来，有超过60位贡献者提交了总计 [816份 commits](https://github.com/facebook/react-native/compare/0.55-stable...0.56-stable) - 在此，向你们致以诚挚的敬意！

正如您刚刚看到的，0.56新版本有一些重要的 **突破性变化** 需要大量的额外测试才能达到稳定版本。这也是时隔数月（4月和5月）才发布的主要原因，但每月发布一个新版本的计划并不会因此改变。

## 要点

### React Native 现在使用 **Babel 7**

升级到0.56时，请确保将您的 `babel-preset-react-native` `package.json` 依赖项提升至 `^5.0.1` 或更高的版本。

React Native 组件作者需要更新其依赖库以使用最新的Babel预设，因为Babel 7 并不向下兼容。

如果您在升级到Babel 7时遇到问题，请仔细检查[相关文档](https://new.babeljs.io/docs/en/next/v7-migration.html#versioning-dependencies-blog-2017-12-27-nearing-the-70-releasehtml-peer-dependencies-integrations)，特别是与 _Package Renames_ 和 _Scoped Packages_ 相关的部分。

如果您需要使用尚未升级到Babel 7 的库，[`babel-bridge`](https://github.com/babel/babel-bridge) 组件可以助您实现暂时的兼容。当然您还可以通过 [yarn resolutions](https://yarnpkg.com/lang/en/docs/selective-version-resolutions/) 等工具强制执行Babel 7 依赖。

### **Node 8** 是此版本RN所需的最低版本。

现在已允许使用尾部逗号。

### **iOS 9** 是此版本RN所需的最低版本

（译者注：截止至2018.05，在所有类型的ios设备上，国内使用低于ios9系统的设备占有率应当在2%左右）

对于用户来说，任何可以运行iOS 8的设备都可以升级到iOS 9。而开发人员也仅仅只需修改一个Xcode级别的设置项（`IPHONEOS_DEPLOYMENT_TARGET`）。

### **Xcode 9** 是此版本RN所需的最低版本

我们建议使用 Xcode 9.4，因为这是Facebook官方开发测试过RN时使用的版本。

### **Android** 项目现在使用 _Android 26 SDK_ 进行编译。

在当前版本中的 `target API level` 保持不变。

自2018年8月开始起，提交给 Google Play Store 的新应用程序至少需要以API 26为目标。您现在就可将项目的 `target API level` 设置为API​​ 26（或更新版本）。如有任何问题，请告知官方。因为我们希望在发布 RN-0.57.0 时得以确定对 Android API 26 的完全支持。

### `WebView` 在默认情况下只会加载http（s）URL

默认情况下将禁用 `地理位置获取`

### Flow 改进, PropTypes 将被抛弃使用.

为几个组件添加了相应的Flow类型。

我们正在抛弃 PropTypes 和 runtime checks（运行检查），而是依赖于 **Flow**。您将注意到此版本中有众多的与Flow相关的改进。

- 在较新的Xcode版本上修复项目设置警告，删除不必要的控制台日志记录。
- 更先进的 `YellowBox`.
  按新旧程度排序警告，按格式字符串分组警告，显示堆栈跟踪，显示加载源映射的状态，支持检查每次出现的警告以及错误修复。
- 更漂亮的文件！
- 众多的错误修复.

### React Native 迭代进度

Heads-up: the Facebook internal team is [currently working on a rewrite of some core architecture pieces](https://facebook.github.io/react-native/blog/2018/06/14/state-of-react-native-2018). This is a **work in progress** and we do not expect it to be ready for use in open source quite yet, but we felt the need to let you know what those commits mentioning Fabric are about.

提要: Facebook内部团队目前正在[努力重构一些核心架构](http://rn.wlfcss.com/react-native/blog/2018/06/14/state-of-react-native-2018.html)这是一项 **正在进行的工作**，距离投入开源世界使用还需要一段时间，但我们觉得有必要让您知道前文中提到的重构大体内容是什么。

---

### 增加的新特性

- 更新(译者注：更新内容为于babelHelpers.js文件中添加自动脚本代码) `babelHelpers` 以支持 Babel 7 - [fbd1bea](https://github.com/facebook/react-native/commit/fbd1beaf666be9c09a380784f8c0cd34ba083a6b)
- `FlatList` 已兼容严格模式 - [a90d0e3](https://github.com/facebook/react-native/commit/a90d0e3614c467c33cf85bcbe65be71903d5aecc)
- 启用 `?.` 可选的链接操作符插件 - [aa6f394](https://github.com/facebook/react-native/commit/aa6f394c4236e5a4998c3be8ed61ec1bab950775)
- 支持 `flexWrap: 'wrap-reverse'` - [d69e550](https://github.com/facebook/react-native/commit/d69e55060fd76d91eccc45905d250a9fce4b2c49)
- 增加属性类型 `accessibilityTraits` 至 `Text`（译者注：为了修复 `VoiceOver` 无法正确识别标题的bug） - [654435d](https://github.com/facebook/react-native/commit/654435d1ed9e584e65fff601e1fa50591e042664)
- 为 templates 添加devDependencies支持（译者注：templates 可以有一个devDependencies.json文件，在里面申明依赖项和devDependencies，亦可保持与当前版本的兼容性。） - [c4ab03a](https://github.com/facebook/react-native/commit/c4ab03a18e75e6ed55444b5d86f3ceee435b9a78)
- 在 `SpringInterpolator` 中添加对springDamping的支持- [1dde989](https://github.com/facebook/react-native/commit/1dde989919d2c272ca7fcaa5c4b2d9ee02c490a0)

#### Android specific additions

- Add support for build.gradle with CRLF for use with `react-native link` - https://github.com/facebook/react-native/commit/843cfc3b202433aad9a236b1b623da7c45e1ac15
- add decimal pad to android - https://github.com/facebook/react-native/commit/5b7a817723e626453eedc800e71a4babd256218f
- Add a way to dismiss PopupMenu elements - https://github.com/facebook/react-native/commit/353c070be9e9a5528d2098db4df3f0dc02d758a9
- Implement `Image.defaultSource` - https://github.com/facebook/react-native/commit/b0fa3228a77d89d6736da6fcae5dd32f74f3052c
- Support Image resizeMode=repeat - https://github.com/facebook/react-native/commit/0459e4ffaadb161598ce1a5b14c08d49a9257c9c
- Yoga: Add back deprecated `getParent` methods for non-breaking API change - https://github.com/facebook/react-native/commit/c3c5c3cbce24a31f73ae6339e377ee76ca6401ad

#### iOS specific additions

- Run tests using Xcode 9.4 and iOS 11.4 - https://github.com/facebook/react-native/commit/c55bcd6ea729cdf57fc14a5478b7c2e3f6b2a94d
- Add support for Homebrew-installed Node - https://github.com/facebook/react-native/commit/0964135a178b459e06b44a49a4ecb0dd6c5bec9b
- Add textTransform style support - https://github.com/facebook/react-native/commit/8621d4b79731e13a0c6e397abd93c193c6219000
- Add docs for Swift usage to `RCTBridgeModule.h` - https://github.com/facebook/react-native/commit/ca898f4367083e0943603521a41c48dec403e6c9

---

### Changes: existing functionality that is now different

- Upgrade React Native to Babel 7 - https://github.com/facebook/react-native/commit/f8d6b97140cffe8d18b2558f94570c8d1b410d5c
- New projects created using `react-native init` will use Babel 7 - https://github.com/facebook/react-native/commit/e315ec9891eb0bcb51afb0e797dbd49aa8f9ac71
- Restrict `WebView` to only http(s) URLs: https://github.com/facebook/react-native/commit/634e7e11e3ad39e0b13bf20cc7722c0cfd3c3e28 https://github.com/facebook/react-native/commit/23f8f7aecb1f21f4f5e44fb9e4a7456ea97935c9
- Node 8 is now the minimum required version - https://github.com/facebook/react-native/commit/c1e6f278237e84c8ed26d3d2eb45035f250e2d40
- Upgrade React to v16.4.1, sync React Renderer to revision ae14317 - https://github.com/facebook/react-native/commit/72d22e8828feece1500487b9c28bb1df21b090f5
- Update new project template's Flow config to fix `Cannot resolve module X` isse due to removal of `@providesModule` - https://github.com/facebook/react-native/commit/843a433e87b0ccaa64ab70d07e22bffbabad8045
- Upgrade Flow to v0.75 - https://github.com/facebook/react-native/commit/3bed272a620ac806a6142327013265ea8138641a, https://github.com/facebook/react-native/commit/8aaf73b4b0bef0d224004b9f1b1c877d46493e71, https://github.com/facebook/react-native/commit/6264b6932a08e1cefd83c4536ff7839d91938730
- Upgrade Flow definitions - https://github.com/facebook/react-native/commit/f8b4850425f115c8a23dead7ec0716b61663aed6
- Upgrade Prettier to v1.13.6 - https://github.com/facebook/react-native/commit/29fb2a8e90fa3811f9485d4b89d9dbcfffea93a6, https://github.com/facebook/react-native/commit/8aaf73b4b0bef0d224004b9f1b1c877d46493e71
- Upgrade Jest to v23.2.0 - https://github.com/facebook/react-native/commit/536c9372692712b12317e657fc3e4263ecc70164#diff-b9cfc7f2cdf78a7f4b91a753d10865a2, https://github.com/facebook/react-native/commit/8aaf73b4b0bef0d224004b9f1b1c877d46493e71
- Upgrade Metro to v0.38 - https://github.com/facebook/react-native/commit/d081f83a0487ffbc7d19f8edc7532611b359dfc6
- Modernized `YellowBox` - https://github.com/facebook/react-native/commit/d0219a0301e59e8b0ef75dbd786318d4b4619f4c
- Disallow requiring from invariant/warning - https://github.com/facebook/react-native/commit/521fb6d041167ec8a8d0e98ac606db1f27f0c5c8
- Remove native prop type validation - https://github.com/facebook/react-native/commit/8dc3ba0444c94d9bbb66295b5af885bff9b9cd34
- Add `$FlowFixMe` to invalid prop accesses where Flow wasn't complaining before - https://github.com/facebook/react-native/commit/f19ee28e7d896aaacf26c6f850230019bdef0d3d
- Create Flow props for `Image` - https://github.com/facebook/react-native/commit/8bac869f5d1f2ef42e707d0ec817afc6ac98b3b2
- Flow type for `SegmentedControlIOS` - https://github.com/facebook/react-native/commit/113f009698dbd8f1b4c1048d77ff1eb373021083
- Flow type for `ProgressViewIOS` - https://github.com/facebook/react-native/commit/c87701ba05a8524756e87c089eb92c8f3c81823e
- Flow type for `PickerIOS` - https://github.com/facebook/react-native/commit/1c66cdc7e8ce8190dfbef76629601497446b2b0a
- Flow type for `Switch` - https://github.com/facebook/react-native/commit/06052a2330fc9c1dd0d56c6bbe5a17703f80c6b9
- Flow type for `Slider` - https://github.com/facebook/react-native/commit/cbe045a95f1ca53d99ae521742a93299a53d6136
- Flow type for `RefreshControl` - https://github.com/facebook/react-native/commit/891dfc3da4b5825097aedf73ff04e8982c00aeff
- Flow type for `ListView` - https://github.com/facebook/react-native/commit/4b1ecb62045fbb78764d1f51030f2253be705c5c
- Flow type for `TextInput` - https://github.com/facebook/react-native/commit/c8bcda8150278fde07331ca6958976b2b3395688
- Flow type for `TouchableBounce` - https://github.com/facebook/react-native/commit/8454a36b0bc54cb1e267bc264657cc693607da71
- Flow type for `TouchableOpacity` - https://github.com/facebook/react-native/commit/44743c07ad672e39668f92a801578906ec92996a
- Flow type for `TouchableHighlight` - https://github.com/facebook/react-native/commit/f0c18dc820537892dcc33d5aebbf4f52cf299b95
- Flow type for `TouchableWithoutFeedback` - https://github.com/facebook/react-native/commit/0b79d1faa21eb3c29aeeba08ee0fb2ed62e6cc54
- Flow type for `ScrollView` - https://github.com/facebook/react-native/commit/b1276622791d5dbe4199bb075f473908c3e62b31
- Flow type for `DatePickerIOS` - https://github.com/facebook/react-native/commit/97e572ea6d7b1fd829ca20f5d5c8ff970d88e68b
- Flow type for `KeyboardAvoidingView` - https://github.com/facebook/react-native/commit/188b118b6075be1614c553596b85d430767f2dbc
- Flow type for `ActivityIndicator` - https://github.com/facebook/react-native/commit/0b71d1ddb03c036ed118574c105b0af505da19fc
- Remove `$FlowFixMe` in `TouchableBounce` - https://github.com/facebook/react-native/commit/ffda0178509ed92396f15db37a41d3d668ade4e6
- Remove `$FlowFixMe` in `ScrollView` - https://github.com/facebook/react-native/commit/af6e2eb02d3651f869b5436e68e61ef3ab3405a0
- Remove `$FlowFixMe` in `ListView` - https://github.com/facebook/react-native/commit/af6e2eb02d3651f869b5436e68e61ef3ab3405a0
- Remove `$FlowFixMe` in `Text` - https://github.com/facebook/react-native/commit/6042592cf46787f089e76b661376705380607207
- Remove `$FlowFixMe` in `RTLExample` - https://github.com/facebook/react-native/commit/206ef54aa415e3e2bb0d48111104dfc372b97e0f
- Remove `$FlowFixMe` in `AppContainer` - https://github.com/facebook/react-native/commit/a956551af73cf785ee4345e92e71fd5b17c5644e
- Remove `$FlowFixMe` in `Slider` - https://github.com/facebook/react-native/commit/1615f9d16149c7082ce0e1485aa04a6f2108f7ba
- `StyleSheet`: Support animated values for border dimensions - https://github.com/facebook/react-native/commit/3e3b10f4044ada7b523d363afb614720468c217f
- Update `react-devtools-core` and `plist` to include security fixes reported by `npm audit` - https://github.com/facebook/react-native/commit/3a1d949906acb0c3b44d125d54d0c99305bbbb56
- Update `Switch` to ES6 Class - https://github.com/facebook/react-native/commit/970caa4552d4ba87c1a954391535ff42b00832e7
- Update `Slider` to ES6 Class - https://github.com/facebook/react-native/commit/5259450c143f71c65e157d6b7d3f0e1655eb7aa1
- Update `ActivityIndicator` to ES6 Class - https://github.com/facebook/react-native/commit/edd7acbb1e6fe185600a19cc1cbb38feb16c85ad
- Update `RefreshControl` to ES6 Class - https://github.com/facebook/react-native/commit/a35a23831789030e17f766f72d307ae315be107d
- Update `KeyboardAvoidingView` to ES6 Class - https://github.com/facebook/react-native/commit/c017dcb0f2903b49b2f21cc150226aeb7f5026ee
- Update `DatePickerIOS` to ES6 Class - https://github.com/facebook/react-native/commit/f8c8231706492b588331354d45b833aa21434e13
- Update `Text` to ES6 Class - https://github.com/facebook/react-native/commit/ab92c00245c0ce717819ddb0ab8b9204d4c13c34
- Replace `context.isInAParentText` w/ `React.createContext` - https://github.com/facebook/react-native/commit/e1339bc18303ca5394cd0c9dc97cededb2261581
- Cleanup `Text` implementation - https://github.com/facebook/react-native/commit/06c05e744d8af9582bde348210f254d76dae48b9
- Switch `Text` to `React.forwardRef` - https://github.com/facebook/react-native/commit/e708010d18f938e2d6b6424cfc9485d8e5dd2800
- Switch `View` to `React.forwardRef` - https://github.com/facebook/react-native/commit/3e534b9aab5156adac67762877b2457408fe8934
- Update uses of `genMockFunction` and `genMockFn` to `fn` in tests - https://github.com/facebook/react-native/commit/390ded871cb905d149e9c1f4a082e67a7ec7addb
- Make `ViewProps` exact - https://github.com/facebook/react-native/commit/65c336f38f4afd43c8b5f81745abf38bd9b8ddbf
- Spread `TVViewProps` into `ViewProps` instead of intersection - https://github.com/facebook/react-native/commit/bc658d3c4405676643d952a126295dbc7fc26217
- Allow trailing commas - https://github.com/facebook/react-native/commit/1e2de712907e5fe0d17648f0ff5c81d4384ca85b
- Use `let`/`const` - https://github.com/facebook/react-native/commit/8f5ebe5952d0675b463137103a82f3fb0c26ae0d
- Refactor `MockNativeMethods` in Jest - https://github.com/facebook/react-native/commit/5d4c542c58d84bbe05f76bf01d9efdd9d438572c
- Use app name from `app.json` after ejecting - https://github.com/facebook/react-native/commit/57774a4a981e2f12cfe9b029447e34f203221b18
- Suggest `git apply --reject` for failed upgrades - https://github.com/facebook/react-native/commit/4fbd244b9a6b62e0efe1b4b5a7ec3de468f020f6
- Moved `TouchHistoryMath` from React to React Native - https://github.com/facebook/react-native/commit/06085d38366373f3135074dc14e2c9871ca4fe29
- Refactor `RCTInputAccessoryView` - https://github.com/facebook/react-native/commit/c136c54ff0211e2bf149fab600cd6e295f9d19dd
- Don't wrap `ListEmptyComponent` in an extra view - https://github.com/facebook/react-native/commit/db061ea8c7b78d7e9df4a450c9e7a24d9b2382b4
- Move `Text` PropTypes to its own file - https://github.com/facebook/react-native/commit/cd8128b2eccf6898cdf798a1e1be1f7a5762a0d4
- Mock `ReactNative.NativeComponent` native methods in Jest - https://github.com/facebook/react-native/commit/3e9a371ace5f25b2eb7a0d30177251f8a0c10ed9
- Tightening types for `View` and `VirtualizedList` - https://github.com/facebook/react-native/commit/5035af80ecddb44e2a8444780f25f336b760bf32
- Make values optional in `ViewPropTypes` - https://github.com/facebook/react-native/commit/f1316cab6c351852ef1da9939d4c8f0244fb8a6f
- propTypes are optional for native components - https://github.com/facebook/react-native/commit/dbdf43b428da19a9eba012753904bcf33339ea9a
- Rename `Style` to `DangerouslyImpreciseStyle` - https://github.com/facebook/react-native/commit/4895c645ea17ff939811f3d5ec6218cd4e31c5fb

### iOS specific changes

- iOS 9 is now the minimum required version - https://github.com/facebook/react-native/commit/f50df4f5eca4b4324ff18a49dcf8be3694482b51
- Update podspecs to target iOS 9 - https://github.com/facebook/react-native/commit/092103e7525e58e04346e0a1a16a67ca4f31c2e9
- Xcode 9.4 is now used to run tests - https://github.com/facebook/react-native/commit/c55bcd6ea729cdf57fc14a5478b7c2e3f6b2a94d
- Prevent console logging on iOS 11.3+ within WebSocket - https://github.com/facebook/react-native/commit/8125be942bd5fd8fe851bad04ae6b9bcb0af4727
- Expose `RCTFont` size overrides - https://github.com/facebook/react-native/commit/6611fefef7559c4cd3d1824235d263bff210d5e2

### Android specific changes

- Projects are now compiled using Android SDK 26 - https://github.com/facebook/react-native/commit/065c5b6590de18281a8c592a04240751c655c03c
- Use Google Maven repo in new Android projects - https://github.com/facebook/react-native/commit/6d56a234e3cf5984335ff2713236260fac977f5f
- Upgrade Buck to v2018.03.26.01 - https://github.com/facebook/react-native/commit/1324e7b5580db815471172cf6dd140124bd2f11a
- Upgrade gradle-plugin to 2.3.3, gradle to 3.5.1, gradle-download-task to 3.4.3 - https://github.com/facebook/react-native/commit/699e5eebe807d1ced660d2d2f39b5679d26925da
- Bump NDK APP_PLATFORM to android-16 - https://github.com/facebook/react-native/commit/5ae97990418db613cd67b1fb9070ece976d17dc7
- Bump glog to 0.3.5 (added libc++ support) - https://github.com/facebook/react-native/commit/8bd43449f0bdf5a5be1e29328810ae68e20c42af
- `ReactFragmentActivity` deprecated as it's not necessary when targeting API level 14 and above - https://github.com/facebook/react-native/commit/8ea8dd6d48bc3db0b8255f320537e662e8fa2a09
- Touchables now play a sound on press - https://github.com/facebook/react-native/commit/722f88ca9058c5d902c416b826a7a7ab347326b8
- Default `underlineColorAndroid` to transparent - https://github.com/facebook/react-native/commit/a3a98eb1c7fa0054a236d45421393874ce8ce558
- Disable `WebView` geolocation by default - https://github.com/facebook/react-native/commit/23d61b35fb6fdbfb84f77b6d99ff155a0ff868e6
- Ensure cookies with illegal characters are not sent to okhttp - https://github.com/facebook/react-native/commit/04028bf2169b01f79bd86ecd6b0d8aa5f99599f1
- Update app icons to match recent Android releases - https://github.com/facebook/react-native/commit/94393f8652c414806fc861c214ad36e9ac1b6114
- Better error messages for `ReadableNativeMap` - https://github.com/facebook/react-native/commit/30d06b42862fc5e8704e109db652d62f86f8eabc
- Update Fresco to v1.9.0, okhttp3 to v3.10.0 - https://github.com/facebook/react-native/commit/6b07602915157f54c39adbf0f9746ac056ad2d13
- Add tint color to inline icons - https://github.com/facebook/react-native/commit/e8e2a6e4102c1ba0ee3d068769e47fa61c160524
- Fix antialiasing rounded background - https://github.com/facebook/react-native/commit/7500b3ec839ada6d8e1f7a88d30743dfb0ad7e70
- `react-native link` will now replace '/' by '_' when linking projects. If you previously linked scoped packages, they will get linked again. - https://github.com/facebook/react-native/commit/dbd47592a18ed09ee6e94c79bed16d63be625af6
- New project template now uses project-wide properties - https://github.com/facebook/react-native/commit/5ae80f91fb54f8b6947dc60b2d98ee73ccd04da0

---

### Fixed: bugs that have been resolved

- `VirtualizedList` now accounts for `ListHeaderComponent` length when calculating offset - https://github.com/facebook/react-native/commit/537731f8a52d5adbeaadb44bd9edcbd98e8455e0
- Prevent showing a hidden status bar when opening modals - https://github.com/facebook/react-native/commit/076b1cea3563cae30e11d63cc100ceaed9082692
- Fix crash when reloading while Perf Monitor is enabled - https://github.com/facebook/react-native/commit/4fcd9970bd2dfb24890bc87e9c82e16dab71ec09
- Fixed concurrency issue in remote debugger - https://github.com/facebook/react-native/commit/e5aa5b7c508c5e0e51f7abfcee350e27bef24ba2
- Fix `Modal` + `FlatList` scrolling - https://github.com/facebook/react-native/commit/8799047dd0bc8dd93f05fa97d4b9a59f7dfeb324
- Fix bug in `RCTNetworking` where not all tasks/handlers were being cleared during invalidation - https://github.com/facebook/react-native/commit/b8051720344f3716e964eaf7cfdd2a91dc703602
- Fix keyboard handling with `keyboardShouldPersistTaps: never` - https://github.com/facebook/react-native/commit/ffe6c110f7ce33460fe0399ccbda16a6adbe90ca
- Fix Responder Logic in `Text` - https://github.com/facebook/react-native/commit/e2ce22b823661a7dcf6b70a825921a2910383bd1
- Fix `VirtualizedSectionList` lint warnings - https://github.com/facebook/react-native/commit/26a1eba1cef853b0dab7aad5731699c06d36b781
- Fix `VirtualizedSectionList:ItemWithSeparators` - https://github.com/facebook/react-native/commit/488a4c7e1c86ac5900ff9194106511fbf5a8e3cb
- Fix `TextInput`'s initial layout measurements - https://github.com/facebook/react-native/commit/c6b4f9f2ce59bc757d9e211f46294faa03df55c6
- Fix `requireNativeComponent` check - https://github.com/facebook/react-native/commit/1c90a2b47b420a4b6aa16a55a344cc08f0eacbe3
- Fix `TextInput` autocapitalization bug - https://github.com/facebook/react-native/commit/ff70ecf868cf12fc66b45dc1496391d0a1e9011f
- Add missing events to `ViewPropTypes` - https://github.com/facebook/react-native/commit/41a940392cea497bc5eb627b24083d0211d1eb89
- Add missing Jest mock in `StatusBarManager` - https://github.com/facebook/react-native/commit/4a2c560768abb2d8407900fdb2fbe4971ae00a1c
- Add Flow declaration for Metro module - https://github.com/facebook/react-native/commit/1853e1519030caaeeb7f31017d98823aa5696daf
- Fix type for `ReactNative.NativeComponent` (1/2) - https://github.com/facebook/react-native/commit/de11ba2a5ee90929dbc67d914de59bdd2ebc29ca
- Fix type for `ReactNative.NativeComponent` (2/2) - https://github.com/facebook/react-native/commit/752863629d63bca6d96a101bfeccc4e7ad3e953e
- Move Image PropTypes to new file - https://github.com/facebook/react-native/commit/67656991b32075e8b4a99c6409b0a131206c6941
- Tests: Fix JUnit report location when running Jest - https://github.com/facebook/react-native/commit/85fc98d437c08cdec883a73161e120478737ba72
- Tests: Fix ReactImagePropertyTest SoLoader failures (#19607) - https://github.com/facebook/react-native/commit/a52d84d7e1cdb287f2877c4d85f2e9866c248d43
- Tests: Fix jest snapshot testing on Windows - https://github.com/facebook/react-native/commit/216bce31632480ce70cc03b1b2a57ec12440afd7
- Fixes "Cannot resolve module" errors in new `react-native init` projects - https://github.com/facebook/react-native/commit/27a497dd5ae51b6a7fdf3df7504f9082bdfae61e
- Haste hotfix for `react-native-windows` - https://github.com/facebook/react-native/commit/600747ffd17022e2077f74f345ee6ee26f6dd49b

#### iOS specific fixes

- Fix undefined_arch error in Xcode 10 beta - 3861dbef5b34734283563e28b454b68d3265d21a
- Make `react-native run-ios` command play nicely with multiple Xcode versions - https://github.com/facebook/react-native/commit/302699a4721d8e721bc222909f92b754eb14140d
- Correct fishhook import - https://github.com/facebook/react-native/commit/ca515e99a39dcadbbfb653205e2929dec7e7096b
- Fix bug where a Backspace event was emitted when entering characters after clearing a text in `TextInput` by an empty string - https://github.com/facebook/react-native/commit/1ffb2b63be4c4af331fece0b4286e5c92b1e575d 
- Expose `InputAccessoryView` so it can be imported - https://github.com/facebook/react-native/commit/80fc415cf179ffe26d020bc8d6e4451352da94fd
- Fix `InputAccessoryView` safe area comformance - https://github.com/facebook/react-native/commit/490f22ae72ba43fa9364ce0f6c238744c07ac830
- Fix use of C++ syntax in header file - https://github.com/facebook/react-native/commit/bfcfe7961db0970e2575eafe2f3c9c668bd8940d
- Fix install step when running `run-ios` - https://github.com/facebook/react-native/commit/0934c1778f0e3c0b691e1a3ca2df1d486eb905dd
- Fix `run-ios` not turning on Simulator - https://github.com/facebook/react-native/commit/9736ddc061e9c4291df8a3185c7f9d6f73e435c7
- Use correct library reference for Fishhook. This fixes the build for the new Xcode build system, on both Xcode 9 and Xcode 10 - https://github.com/facebook/react-native/commit/a8b74576da6f1a42fde4e39f97e88c8f45a3a51d
- Add missing `onChange` event definition to `DatePickerIOS` - https://github.com/facebook/react-native/commit/3b53091869b673ea33a4af34242e2227ca944768
- Fix crash during Archive phase on Xcode 9.3 - https://github.com/facebook/react-native/commit/344c205070d5ad670c97984dd86ec9ac13c73f81
- `RNTesterPods`: Add missing folly include - https://github.com/facebook/react-native/commit/128c9343c464f3e7898d6e245f135f8bdf6caa6a
- `RNTesterPods`: folly::Optional's `has_value()` to `hasValue()` until folly is upgraded - https://github.com/facebook/react-native/commit/128c9343c464f3e7898d6e245f135f8bdf6caa6a
- `RNTesterPods`: Fix import for `RCTTestAttributes.h` - https://github.com/facebook/react-native/commit/128c9343c464f3e7898d6e245f135f8bdf6caa6a
- `RNTesterPods`: Fix `conversions.h` to use namespaced includes - https://github.com/facebook/react-native/commit/128c9343c464f3e7898d6e245f135f8bdf6caa6a
- Fix or mark enum conversions surfaced by `-Wenum-conversion` - https://github.com/facebook/react-native/commit/b8f30db0ae21d5f96547702abbf50aefa93b1094
- Fix CocoaPods integration without DevSupport subspec - https://github.com/facebook/react-native/commit/c09d509c2b8a5a02701829e1f0ace8081ce64277
- Update Yoga to handle being in a Xcode framework project - https://github.com/facebook/react-native/commit/cf036dbc7af16a8453c115372694dc51e8086fcf
- Fix Blob memory leak - https://github.com/facebook/react-native/commit/122b3791ede095345f44666691aa9ce5aa7f725a
- Avoid double reload event when reloading JS - https://github.com/facebook/react-native/commit/b348aa14d483cc6b33ba92637647c4987c9478c1
- Suppres spurious warning about RCTCxxModule - https://github.com/facebook/react-native/commit/af76473c2e344c13ecac054b5a5568a0b94128e5

#### Android specific fixes

- Fix extreme `TextInput` slowness on Android - https://github.com/facebook/react-native/commit/1b4187fc414352cd3724e2d4df2009f5a045fe3f
- Correct draw path dimensions while doing even border, fixes blurred borders - https://github.com/facebook/react-native/commit/c5ca26a0e5c0660196300ee34d6007c63879611f
- Don't pass additional arguments to `requireNativeComponent` in `.android.js` files - https://github.com/facebook/react-native/commit/a51e8b19cc4dc36dee42ac95278b883c06b2e40f
- Prevent `RefreshControl` from getting stuck when a parent is scrolled horizontally - https://github.com/facebook/react-native/commit/33ffa79a51d4db9ba69148861f2da304646175cd
- Prevent crash due to unsupported ellipsize mode - https://github.com/facebook/react-native/commit/85e33aaf908996e99220bff4a2bdbbdf7c0d12b0
- Fix okhttp3 response handling in `DevServerHelper` - https://github.com/facebook/react-native/commit/56d48bd9ecd2d0f08625259121312531064a09f2
- Fix `ReactInstanceManager` unmountApplication to support `ReactRootView` recycling - https://github.com/facebook/react-native/commit/4a9b2a73021fb547febe1fa193c3effb7ff8da4e
- Fix `NullPointerException` when emiting event using `UIManagerModule` - https://github.com/facebook/react-native/commit/291c01f4ffe614760852e36b05d78b42cb4271df
- Fix link to Android build guide - https://github.com/facebook/react-native/commit/57e7556b8db61e5fcc3ccea56c1b163b82a091a6
- Fix Android open source test failures - https://github.com/facebook/react-native/commit/3e0ebc76632238f21c60caa92c7a2b5ee8102b71
- Fix view indices with LayoutAnimation - https://github.com/facebook/react-native/commit/d8fcdb9bd7a308ed70caeac1b53da0a05abe452f
- Fix originalNode memory leak - https://github.com/facebook/react-native/commit/8102e35271ab68e0525a9c60d86a855bbeef9c1a
- Fix `ScrollView` with a `TextInput` - https://github.com/facebook/react-native/commit/2f1421dec7cd3a35779caceac108e872033c7d72
- Disable onKeyPRess logic when handler not defined - https://github.com/facebook/react-native/commit/41975f75d96ef4b606b4618461bf24d5db063b77
- fix permission requests on pre-M android - https://github.com/facebook/react-native/commit/6d27bd182fa87cab0c68ca281c869b987cbd2ca6

---

### Removed: features that have been removed; these are breaking

- Deprecate `focusTextInput` and `blurTextInput` - https://github.com/facebook/react-native/commit/ce3b7b8204dad0fd62a76a0ce66472eca4b25bc8

#### Android specific removals

- Remove native extensions - https://github.com/facebook/react-native/commit/7c5845a5a26592598c9380df078766a680a23f06
- Remove Fresco ProGuard rules - https://github.com/facebook/react-native/commit/07df36557c8cbbaee5e870460162aa725a606ff4

#### iOS specific removals

- Removed deprecated `UIActionSheetDelegate` methods - https://github.com/facebook/react-native/commit/5863b564f84b9fe97b256f8cde0f7f2e1db9b641
