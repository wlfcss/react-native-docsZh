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
- Prettier 文件管理!
- 众多的错误修复.

### React Native 迭代进度

提要: Facebook内部团队目前正在[努力重构一些核心架构](http://rn.wlfcss.com/react-native/blog/2018/06/14/state-of-react-native-2018.html)这是一项 **正在进行的工作**，距离投入开源世界使用还需要一段时间，但我们觉得有必要让您知道前文中提到的重构大体内容是什么。

---

### 增加的新特性

- 更新(译者注：更新内容为于babelHelpers.js文件中添加自动脚本代码) `babelHelpers` 以支持 Babel 7 - [fbd1bea](https://github.com/facebook/react-native/commit/fbd1beaf666be9c09a380784f8c0cd34ba083a6b)
- `FlatList` 已兼容严格模式 - [a90d0e3](https://github.com/facebook/react-native/commit/a90d0e3614c467c33cf85bcbe65be71903d5aecc)
- 启用 `?.` 可选的链接操作符插件 - [aa6f394](https://github.com/facebook/react-native/commit/aa6f394c4236e5a4998c3be8ed61ec1bab950775)
- 支持 `flexWrap: 'wrap-reverse'` - [d69e550](https://github.com/facebook/react-native/commit/d69e55060fd76d91eccc45905d250a9fce4b2c49)
- 增加属性类型 `accessibilityTraits` 至 `Text`（译者注：为了修复 `VoiceOver` 无法正确识别标题的bug）- [654435d](https://github.com/facebook/react-native/commit/654435d1ed9e584e65fff601e1fa50591e042664)
- 为 templates 添加devDependencies支持（译者注：templates 可以有一个devDependencies.json文件，在里面申明依赖项和devDependencies，亦可保持与当前版本的兼容性。） - [c4ab03a](https://github.com/facebook/react-native/commit/c4ab03a18e75e6ed55444b5d86f3ceee435b9a78)
- 在 `SpringInterpolator` 中添加对springDamping的支持 - [1dde989](https://github.com/facebook/react-native/commit/1dde989919d2c272ca7fcaa5c4b2d9ee02c490a0)

#### Android 新增功能

- 为 build.gradle 添加 CRLF（回车符） 结尾的支持，以修正命令 `react-native link` 出错的问题 - [843cfc3](https://github.com/facebook/react-native/commit/843cfc3b202433aad9a236b1b623da7c45e1ac15)
- 添加一个包含数字0-9与小数点的输入键盘支持（译者注：对原生 inputType“numberDecimal” 支持） - [5b7a817](https://github.com/facebook/react-native/commit/5b7a817723e626453eedc800e71a4babd256218f)
- 增加了一种关闭 PopupMenu 元素的方式（译者注：当 Popupmenu 出现时触发屏幕方向改变[横屏/竖屏]，将自动关闭Popupmenu） - [353c070](https://github.com/facebook/react-native/commit/353c070be9e9a5528d2098db4df3f0dc02d758a9)
- 添加 `Image.defaultSource` 属性 （译者注：此属性为设置加载远程图像时显示的占位符图像[本地资源]）- https://github.com/facebook/react-native/commit/b0fa3228a77d89d6736da6fcae5dd32f74f3052c
- 添加支持 Image 对象新属性 resizeMode=repeat （译者注：[resizeMode]当组件尺寸和图片尺寸不成比例的时候如何调整图片的大小 [repeat]重复平铺图片直到填满容器。图片会维持原始尺寸）- [0459e4f](https://github.com/facebook/react-native/commit/0459e4ffaadb161598ce1a5b14c08d49a9257c9c)
- Yoga: 新增了一个不推荐使用的 `getParent`  API 变更方法 - [c3c5c3c](https://github.com/facebook/react-native/commit/c3c5c3cbce24a31f73ae6339e377ee76ca6401ad)

#### iOS 新增功能

- 新增对 Xcode 9.4 和 iOS 11.4 的支持(通过版本测试) - [c55bcd6](https://github.com/facebook/react-native/commit/c55bcd6ea729cdf57fc14a5478b7c2e3f6b2a94d)
- 添加对 Homebrew 安装的 Node 环境的支持 - [0964135](https://github.com/facebook/react-native/commit/0964135a178b459e06b44a49a4ecb0dd6c5bec9b)
- 添加对 textTransform 样式支持 - https://github.com/facebook/react-native/commit/8621d4b79731e13a0c6e397abd93c193c6219000
- 添加关于 Swift 使用方法的文档到 `RCTBridgeModule.h` 之中 - https://github.com/facebook/react-native/commit/ca898f4367083e0943603521a41c48dec403e6c9

---

### 修正: 功能变化

- 升级 React Native 依赖至 Babel 7 - [f8d6b97](https://github.com/facebook/react-native/commit/f8d6b97140cffe8d18b2558f94570c8d1b410d5c)
- 使用 `react-native init` 创建新项目将使用 Babel 7 - [e315ec9](https://github.com/facebook/react-native/commit/e315ec9891eb0bcb51afb0e797dbd49aa8f9ac71)
- 限制 `WebView` 的支持范围，现仅支持http及https （译者注：禁止用户使用其他的URL，比如 file:// ）: [634e7e1](https://github.com/facebook/react-native/commit/634e7e11e3ad39e0b13bf20cc7722c0cfd3c3e28), [23f8f7a](https://github.com/facebook/react-native/commit/23f8f7aecb1f21f4f5e44fb9e4a7456ea97935c9)
- Node 版本的最低要求升高到 node 8 - [c1e6f27](https://github.com/facebook/react-native/commit/c1e6f278237e84c8ed26d3d2eb45035f250e2d40)
- 升级 React 版本依赖至 v16.4.1, 并同步 React Renderer 版本至 ae14317 - [72d22e8](https://github.com/facebook/react-native/commit/72d22e8828feece1500487b9c28bb1df21b090f5)
- 更新新项目模板的Flow配置以修复由于 `@providesModule` 模块被移除导致的报错：`Cannot resolve module X` - [843a433](https://github.com/facebook/react-native/commit/843a433e87b0ccaa64ab70d07e22bffbabad8045)
- 升级 Flow 版本至 v0.75 - [3bed272](https://github.com/facebook/react-native/commit/3bed272a620ac806a6142327013265ea8138641a), [8aaf73b](https://github.com/facebook/react-native/commit/8aaf73b4b0bef0d224004b9f1b1c877d46493e71), [6264b69](https://github.com/facebook/react-native/commit/6264b6932a08e1cefd83c4536ff7839d91938730)
- 升级 Flow definitions (译者注：Upgrade Flow Definition in RN + Metro) - [f8b4850](https://github.com/facebook/react-native/commit/f8b4850425f115c8a23dead7ec0716b61663aed6)
- 升级 Prettier 版本至 v1.13.6 - [29fb2a8](https://github.com/facebook/react-native/commit/29fb2a8e90fa3811f9485d4b89d9dbcfffea93a6), [8aaf73b](https://github.com/facebook/react-native/commit/8aaf73b4b0bef0d224004b9f1b1c877d46493e71)
- 升级 Jest 版本至 v23.2.0 - [536c937＃DIFF-b9cfc7f2cdf78a7f4b91a753d10865a2](https://github.com/facebook/react-native/commit/536c9372692712b12317e657fc3e4263ecc70164#diff-b9cfc7f2cdf78a7f4b91a753d10865a2), [8aaf73b](https://github.com/facebook/react-native/commit/8aaf73b4b0bef0d224004b9f1b1c877d46493e71)
- 升级 Metro 版本至 v0.38 - [d081f83](https://github.com/facebook/react-native/commit/d081f83a0487ffbc7d19f8edc7532611b359dfc6)
- 现代化的 `YellowBox`（译者注：使用所谓 modern YellowBox 替换现有的 YellowBox，新特性包含：1.按时间倒序排序警告、2.按格式字符串分组警告[若存在]等等 ）- [d0219a0](https://github.com/facebook/react-native/commit/d0219a0301e59e8b0ef75dbd786318d4b4619f4c)
- 禁止 invariant/warning - [521fb6d](https://github.com/facebook/react-native/commit/521fb6d041167ec8a8d0e98ac606db1f27f0c5c8)
- 移除 原生 prop 类型检查（译者注：官方消息已确认propTypes将被完整的移除，类型检查将被Flow接管） - [8dc3ba0](https://github.com/facebook/react-native/commit/8dc3ba0444c94d9bbb66295b5af885bff9b9cd34)
- Add `$FlowFixMe` to invalid prop accesses where Flow wasn't complaining before - [f19ee28](https://github.com/facebook/react-native/commit/f19ee28e7d896aaacf26c6f850230019bdef0d3d)
- 为 `Image` 创建 Flow props - [8bac869](https://github.com/facebook/react-native/commit/8bac869f5d1f2ef42e707d0ec817afc6ac98b3b2)
- 为 `SegmentedControlIOS` 添加 Flow type  - [113f009](https://github.com/facebook/react-native/commit/113f009698dbd8f1b4c1048d77ff1eb373021083)
- 为 `ProgressViewIOS` 添加 Flow type - [c87701b](https://github.com/facebook/react-native/commit/c87701ba05a8524756e87c089eb92c8f3c81823e)
- 为 `PickerIOS` 添加 Flow type - [1c66cdc](https://github.com/facebook/react-native/commit/1c66cdc7e8ce8190dfbef76629601497446b2b0a)
- 为 `Switch` 添加 Flow type - [06052a2](https://github.com/facebook/react-native/commit/06052a2330fc9c1dd0d56c6bbe5a17703f80c6b9)
- 为 `Slider` 添加 Flow type - [cbe045a](https://github.com/facebook/react-native/commit/cbe045a95f1ca53d99ae521742a93299a53d6136)
- 为 `RefreshControl` 添加 Flow type - [891dfc3](https://github.com/facebook/react-native/commit/891dfc3da4b5825097aedf73ff04e8982c00aeff)
- 为 `ListView` 添加 Flow type for - [4b1ecb6](https://github.com/facebook/react-native/commit/4b1ecb62045fbb78764d1f51030f2253be705c5c)
- 为 `TextInput` 添加 Flow type for - [c8bcda8](https://github.com/facebook/react-native/commit/c8bcda8150278fde07331ca6958976b2b3395688)
- 为 `TouchableBounce` 添加 Flow type for - [8454a36](https://github.com/facebook/react-native/commit/8454a36b0bc54cb1e267bc264657cc693607da71)
- 为 `TouchableOpacity` 添加 Flow type - [44743c0](https://github.com/facebook/react-native/commit/44743c07ad672e39668f92a801578906ec92996a)
- 为 `TouchableHighlight` 添加 Flow type - [f0c18dc](https://github.com/facebook/react-native/commit/f0c18dc820537892dcc33d5aebbf4f52cf299b95)
- 为 `TouchableWithoutFeedback` 添加 Flow type - [0b79d1f](https://github.com/facebook/react-native/commit/0b79d1faa21eb3c29aeeba08ee0fb2ed62e6cc54)
- 为 `ScrollView` 添加 Flow type - [b127662](https://github.com/facebook/react-native/commit/b1276622791d5dbe4199bb075f473908c3e62b31)
- 为 `DatePickerIOS` 添加 Flow type - [97e572e](https://github.com/facebook/react-native/commit/97e572ea6d7b1fd829ca20f5d5c8ff970d88e68b)
- 为 `KeyboardAvoidingView` 添加 Flow type - [188b118](https://github.com/facebook/react-native/commit/188b118b6075be1614c553596b85d430767f2dbc)
- 为 `ActivityIndicator` 添加 Flow type - [0b71d1d](https://github.com/facebook/react-native/commit/0b71d1ddb03c036ed118574c105b0af505da19fc)
- 于 `TouchableBounce` 之中移除 `$FlowFixMe` - [ffda017](https://github.com/facebook/react-native/commit/ffda0178509ed92396f15db37a41d3d668ade4e6)
- 于 `ScrollView` 之中移除 `$FlowFixMe` - [af6e2eb](https://github.com/facebook/react-native/commit/af6e2eb02d3651f869b5436e68e61ef3ab3405a0)
- 于 `ListView` 之中移除 `$FlowFixMe` - [af6e2eb](https://github.com/facebook/react-native/commit/af6e2eb02d3651f869b5436e68e61ef3ab3405a0)
- 于 `Text` 之中移除 `$FlowFixMe` - [6042592](https://github.com/facebook/react-native/commit/6042592cf46787f089e76b661376705380607207)
- 于 `RTLExample` 之中移除 `$FlowFixMe` - [206ef54](https://github.com/facebook/react-native/commit/206ef54aa415e3e2bb0d48111104dfc372b97e0f)
- 于 `AppContainer` 之中移除 `$FlowFixMe` - [a956551](https://github.com/facebook/react-native/commit/a956551af73cf785ee4345e92e71fd5b17c5644e)
- 于 `Slider` 之中移除 `$FlowFixMe` - [1615f9d](https://github.com/facebook/react-native/commit/1615f9d16149c7082ce0e1485aa04a6f2108f7ba)
- `StyleSheet`: 新增支持边框尺寸变化的动画 - [3e3b10f](https://github.com/facebook/react-native/commit/3e3b10f4044ada7b523d363afb614720468c217f)
- 更新 `react-devtools-core` 与 `plist` 版本以修复由 `npm audit` 所报告的安全问题 - [3a1d949](https://github.com/facebook/react-native/commit/3a1d949906acb0c3b44d125d54d0c99305bbbb56)
- 更新 `Switch` 至 ES6 Class - [970caa4](https://github.com/facebook/react-native/commit/970caa4552d4ba87c1a954391535ff42b00832e7)
- 更新 `Slider` 至 ES6 Class - [5259450](https://github.com/facebook/react-native/commit/5259450c143f71c65e157d6b7d3f0e1655eb7aa1)
- 更新 `ActivityIndicator` 至 ES6 Class - [edd7acb](https://github.com/facebook/react-native/commit/edd7acbb1e6fe185600a19cc1cbb38feb16c85ad)
- 更新 `RefreshControl` 至 ES6 Class - [a35a238](https://github.com/facebook/react-native/commit/a35a23831789030e17f766f72d307ae315be107d)
- 更新 `KeyboardAvoidingView` 至 ES6 Class - [c017dcb](https://github.com/facebook/react-native/commit/c017dcb0f2903b49b2f21cc150226aeb7f5026ee)
- 更新 `DatePickerIOS` 至 ES6 Class - [f8c8231](https://github.com/facebook/react-native/commit/f8c8231706492b588331354d45b833aa21434e13)
- 更新 `Text` 至 ES6 Class - [ab92c00](https://github.com/facebook/react-native/commit/ab92c00245c0ce717819ddb0ab8b9204d4c13c34)
- 将 `context.isInAParentText` 替换为 `React.createContext` - [e1339bc](https://github.com/facebook/react-native/commit/e1339bc18303ca5394cd0c9dc97cededb2261581)
- 整理（清理） `Text` 的实现代码 - [06c05e7](https://github.com/facebook/react-native/commit/06c05e744d8af9582bde348210f254d76dae48b9)
- 更新 `Text` (内部实现方法)至 `React.forwardRef` - [e708010](https://github.com/facebook/react-native/commit/e708010d18f938e2d6b6424cfc9485d8e5dd2800)
- 更新 `View` (内部实现方法)至 `React.forwardRef` - [06c05e7](https://github.com/facebook/react-native/commit/3e534b9aab5156adac67762877b2457408fe8934)
- 在测试中移除 `genMockFunction` 与 `genMockFn` 并用 `fn` 代替 ([390ded8](https://github.com/facebook/react-native/commit/390ded871cb905d149e9c1f4a082e67a7ec7addb))
- 修正更新 `ViewProps` 代码 ([65c336f](https://github.com/facebook/react-native/commit/65c336f38f4afd43c8b5f81745abf38bd9b8ddbf))
- Spread `TVViewProps` into `ViewProps` instead of intersection ([bc658d3](https://github.com/facebook/react-native/commit/bc658d3c4405676643d952a126295dbc7fc26217))
- 允许在函数参数上使用尾随逗号 ([1e2de71](https://github.com/facebook/react-native/commit/1e2de712907e5fe0d17648f0ff5c81d4384ca85b))
- 使用 `let`/`const` 替代 `react-native-github`/`Libraries` ([8f5ebe5](https://github.com/facebook/react-native/commit/8f5ebe5952d0675b463137103a82f3fb0c26ae0d))
- 重构 jest 中的 `MockNativeMethods` ([5d4c542](https://github.com/facebook/react-native/commit/5d4c542c58d84bbe05f76bf01d9efdd9d438572c))
- 使用 `app.json` 中的 app name 来注册应用程序 ([57774a4](https://github.com/facebook/react-native/commit/57774a4a981e2f12cfe9b029447e34f203221b18))
- 建议使用 `git apply --reject` 以避免更新失败 ([4fbd244](https://github.com/facebook/react-native/commit/4fbd244b9a6b62e0efe1b4b5a7ec3de468f020f6))
- 将 `TouchHistoryMath` 从 React Repo 移动到 React Native ([06085d3](https://github.com/facebook/react-native/commit/06085d38366373f3135074dc14e2c9871ca4fe29))
- 重构 `RCTInputAccessoryView` ([c136c54](https://github.com/facebook/react-native/commit/c136c54ff0211e2bf149fab600cd6e295f9d19dd))
- 不要将 `ListEmptyComponent` 放入额外的 View 之中 ([db061ea](https://github.com/facebook/react-native/commit/db061ea8c7b78d7e9df4a450c9e7a24d9b2382b4))
- 将 `Text` PropTypes 实现独立到其专有文件中(TextPropTypes.js) ([cd8128b](https://github.com/facebook/react-native/commit/cd8128b2eccf6898cdf798a1e1be1f7a5762a0d4))
- 在 jest 之中模拟 `ReactNative.NativeComponent` 原生方法 ([3e9a371](https://github.com/facebook/react-native/commit/3e9a371ace5f25b2eb7a0d30177251f8a0c10ed9))
- 为 `View` 和 `VirtualizedList` 设置更为严格的类型限制 ([5035af8](https://github.com/facebook/react-native/commit/5035af80ecddb44e2a8444780f25f336b760bf32))
- 为 `ViewPropTypes` 添加可选值 ([f1316ca](https://github.com/facebook/react-native/commit/f1316cab6c351852ef1da9939d4c8f0244fb8a6f))
- 对于原生组件而言 propTypes 是可选的 ([dbdf43b](https://github.com/facebook/react-native/commit/dbdf43b428da19a9eba012753904bcf33339ea9a))
- 将 `Style` 重命名为 `DangerouslyImpreciseStyle` ([4895c64](https://github.com/facebook/react-native/commit/4895c645ea17ff939811f3d5ec6218cd4e31c5fb))
- *[BREAKING]* `requireNativeComponent` 的签名已简化为一个额外的可选项 ([820673e](https://github.com/facebook/react-native/commit/820673e), [b549e36](https://github.com/facebook/react-native/commit/b549e36), [28d3778](https://github.com/facebook/react-native/commit/28d3778), [1c90a2b](https://github.com/facebook/react-native/commit/1c90a2b), and [1ab7d49](https://github.com/facebook/react-native/commit/1ab7d49) by [@yungsters](https://github.com/yungsters))

### iOS 更改

- *[BREAKING]* WebViews 现在有且只能使用 `https` ; 请勿使用 `file://` ([634e7e1](https://github.com/facebook/react-native/commit/634e7e1) by [@mmmulani](https://github.com/mmmulani))
- iOS 9 是此版本RN所需的最低版本 ([f50df4f](https://github.com/facebook/react-native/commit/f50df4f5eca4b4324ff18a49dcf8be3694482b51))
- 更新 podspecs 以适应 iOS 9 ([092103e](https://github.com/facebook/react-native/commit/092103e7525e58e04346e0a1a16a67ca4f31c2e9))
- Xcode 9.4 现在用于运行测试 ([c55bcd6](https://github.com/facebook/react-native/commit/c55bcd6ea729cdf57fc14a5478b7c2e3f6b2a94d))
- 去除 iOS 11.3+ 上的控制台日志记录止 WebSocket 信息 ([8125be9](https://github.com/facebook/react-native/commit/8125be942bd5fd8fe851bad04ae6b9bcb0af4727))
- 暴露 `RCTFont` 的大小覆盖（以便于测试） ([6611fef](https://github.com/facebook/react-native/commit/6611fefef7559c4cd3d1824235d263bff210d5e2))

### Android 更改

- 现在使用 Android SDK 26 编译项目 ([065c5b6](https://github.com/facebook/react-native/commit/065c5b6590de18281a8c592a04240751c655c03c))
- 在新的 Android 项目中使用 Google Maven repo ([6d56a23](https://github.com/facebook/react-native/commit/6d56a234e3cf5984335ff2713236260fac977f5f))
- 将 Buck 升级为 v2018.03.26.01 ([1324e7b](https://github.com/facebook/react-native/commit/1324e7b5580db815471172cf6dd140124bd2f11a))
- 升级 gradle-plugin 至 2.3.3, 升级 gradle 至 3.5.1, 升级 gradle-download-task 至 3.4.3 ([699e5ee](https://github.com/facebook/react-native/commit/699e5eebe807d1ced660d2d2f39b5679d26925da))
- Bump NDK APP_PLATFORM to android-16 ([5ae9799](https://github.com/facebook/react-native/commit/5ae97990418db613cd67b1fb9070ece976d17dc7))
- Bump glog to 0.3.5 (added libc++ support) ([8bd4344](https://github.com/facebook/react-native/commit/8bd43449f0bdf5a5be1e29328810ae68e20c42af))
- `ReactFragmentActivity` 已被弃用，因为在 API-14 或更新级别时不需要 ([8ea8dd6](https://github.com/facebook/react-native/commit/8ea8dd6d48bc3db0b8255f320537e662e8fa2a09))
- 将 Android 点击声添加至 Touchables ([722f88c](https://github.com/facebook/react-native/commit/722f88ca9058c5d902c416b826a7a7ab347326b8))
- 默认 `underlineColorAndroid` 为透明 ([a3a98eb](https://github.com/facebook/react-native/commit/a3a98eb1c7fa0054a236d45421393874ce8ce558))
- `WebView` 在默认情况下禁用获取地理位置 ([23d61b3](https://github.com/facebook/react-native/commit/23d61b35fb6fdbfb84f77b6d99ff155a0ff868e6))
- 确保带有非法字符的 cookie 不会发送到 okhttp ([04028bf](https://github.com/facebook/react-native/commit/04028bf2169b01f79bd86ecd6b0d8aa5f99599f1))
- 更新应用图标以以适应新的Android版本 ([94393f8](https://github.com/facebook/react-native/commit/94393f8652c414806fc861c214ad36e9ac1b6114))
- 为 `ReadableNativeMap` 提供更好的错误提示 ([30d06b4](https://github.com/facebook/react-native/commit/30d06b42862fc5e8704e109db652d62f86f8eabc))
- 将 Fresco 更新为 v1.9.0, 将 okhttp3 更新为 v3.10.0 ([6b07602](https://github.com/facebook/react-native/commit/6b07602915157f54c39adbf0f9746ac056ad2d13))
- 为内联图标(inline icons)添加色调颜色 ([e8e2a6e](https://github.com/facebook/react-native/commit/e8e2a6e4102c1ba0ee3d068769e47fa61c160524))
- 修复抗锯齿圆形背景 ([7500b3e](https://github.com/facebook/react-native/commit/7500b3ec839ada6d8e1f7a88d30743dfb0ad7e70))
- `react-native link` 现在使用用 '/' 代替 '_' 在 link 依赖包时. 如果您以前链接过依赖包，它们将再次 link。 ([dbd4759](https://github.com/facebook/react-native/commit/dbd47592a18ed09ee6e94c79bed16d63be625af6))
- 新项目模板将使用现有项目范围(译者注：gradle文件中设置的属性)中的属性 ([5ae80f9](https://github.com/facebook/react-native/commit/5ae80f91fb54f8b6947dc60b2d98ee73ccd04da0))

---

### 修正: 已修复的错误

- `VirtualizedList` now accounts for `ListHeaderComponent` length when calculating offset ([537731f](https://github.com/facebook/react-native/commit/537731f8a52d5adbeaadb44bd9edcbd98e8455e0))
- 在打开模态窗(modals)时将阻止显示隐藏状态栏 ([076b1ce](https://github.com/facebook/react-native/commit/076b1cea3563cae30e11d63cc100ceaed9082692))
- 修复启用 Perf Monitor 重加载出现的崩溃问题 ([4fcd997](https://github.com/facebook/react-native/commit/4fcd9970bd2dfb24890bc87e9c82e16dab71ec09))
- 修复了远程调试器中的并发问题 ([e5aa5b7](https://github.com/facebook/react-native/commit/e5aa5b7c508c5e0e51f7abfcee350e27bef24ba2))
- 修复 `Modal` + `FlatList` 的滚动问题 ([8799047](https://github.com/facebook/react-native/commit/8799047dd0bc8dd93f05fa97d4b9a59f7dfeb324))
- 修复 `RCTNetworking` 在失效期间未清除所有 tasks/handlers 的错误 ([b805172](https://github.com/facebook/react-native/commit/b8051720344f3716e964eaf7cfdd2a91dc703602))
- 使用 `keyboardShouldPersistTaps: never` 修复键盘错误 ([ffe6c11](https://github.com/facebook/react-native/commit/ffe6c110f7ce33460fe0399ccbda16a6adbe90ca))
- 修复 `Text` 的响应逻辑 ([e2ce22b](https://github.com/facebook/react-native/commit/e2ce22b823661a7dcf6b70a825921a2910383bd1))
- 修复 `VirtualizedSectionList` lint 警告 ([26a1eba](https://github.com/facebook/react-native/commit/26a1eba1cef853b0dab7aad5731699c06d36b781))
- 修复 `VirtualizedSectionList:ItemWithSeparators` ([488a4c7](https://github.com/facebook/react-native/commit/488a4c7e1c86ac5900ff9194106511fbf5a8e3cb))
- 修复 `TextInput`的初始布局大小 ([c6b4f9f](https://github.com/facebook/react-native/commit/c6b4f9f2ce59bc757d9e211f46294faa03df55c6))
- 修复 `requireNativeComponent` 检查 ([1c90a2b](https://github.com/facebook/react-native/commit/1c90a2b47b420a4b6aa16a55a344cc08f0eacbe3))
- 修复 `TextInput` 自动大写功能的BUG ([ff70ecf](https://github.com/facebook/react-native/commit/ff70ecf868cf12fc66b45dc1496391d0a1e9011f))
- 为 `ViewPropTypes` 添加缺失的事件 ([41a9403](https://github.com/facebook/react-native/commit/41a940392cea497bc5eb627b24083d0211d1eb89))
- 在 `StatusBarManager` 中添加缺少的 jest 模拟 ([4a2c560](https://github.com/facebook/react-native/commit/4a2c560768abb2d8407900fdb2fbe4971ae00a1c))
- 为 Metro module 添加 Flow 声明 ([1853e15](https://github.com/facebook/react-native/commit/1853e1519030caaeeb7f31017d98823aa5696daf))
- 修复 `ReactNative.NativeComponent` 类型错误 (1/2) ([de11ba2](https://github.com/facebook/react-native/commit/de11ba2a5ee90929dbc67d914de59bdd2ebc29ca))
- 修复 `ReactNative.NativeComponent` 类型错误 (2/2) ([7528636](https://github.com/facebook/react-native/commit/752863629d63bca6d96a101bfeccc4e7ad3e953e))
- 将 Image PropTypes 相关代码独立到新文件(ImageProps.js) ([6765699](https://github.com/facebook/react-native/commit/67656991b32075e8b4a99c6409b0a131206c6941))
- 测试: Fix JUnit report location when running Jest ([85fc98d](https://github.com/facebook/react-native/commit/85fc98d437c08cdec883a73161e120478737ba72))
- 测试: Fix ReactImagePropertyTest SoLoader failures (#19607) ([a52d84d](https://github.com/facebook/react-native/commit/a52d84d7e1cdb287f2877c4d85f2e9866c248d43))
- 测试: Fix jest snapshot testing on Windows ([216bce3](https://github.com/facebook/react-native/commit/216bce31632480ce70cc03b1b2a57ec12440afd7))
- 修复 使用 `react-native init` 新建项目时出现的 "Cannot resolve module" 错误  ([27a497d](https://github.com/facebook/react-native/commit/27a497dd5ae51b6a7fdf3df7504f9082bdfae61e))
- 紧急修复关于 `react-native-windows` 的错误 ([600747f](https://github.com/facebook/react-native/commit/600747ffd17022e2077f74f345ee6ee26f6dd49b))

#### iOS 更改

- 修复在 Xcode 10 beta 版本中出现的 undefined_arch 错误 - 3861dbef5b34734283563e28b454b68d3265d21a
- 使 `react-native run-ios` 命令与多个 Xcode 版本可以更好的配合使用 ([302699a](https://github.com/facebook/react-native/commit/302699a4721d8e721bc222909f92b754eb14140d))
- 修正 fishhook 依赖引入 ([ca515e9](https://github.com/facebook/react-native/commit/ca515e99a39dcadbbfb653205e2929dec7e7096b))
- 修复 `TextInput` 组件在用空字符串清除文本后输入字符时发生的 Backspace 事件错误 ([1ffb2b6](https://github.com/facebook/react-native/commit/1ffb2b63be4c4af331fece0b4286e5c92b1e575d))
- 公开 `InputAccessoryView` 组件，修复其无法被 import 的错误 ([80fc415](https://github.com/facebook/react-native/commit/80fc415cf179ffe26d020bc8d6e4451352da94fd))
- 修复 `InputAccessoryView` 安全区域的一致性错误 ([490f22a](https://github.com/facebook/react-native/commit/490f22ae72ba43fa9364ce0f6c238744c07ac830))
- 修复头文件中使用C ++语法的问题 ([bfcfe79](https://github.com/facebook/react-native/commit/bfcfe7961db0970e2575eafe2f3c9c668bd8940d))
- 修复 `run-ios` 命令中安装步骤的bug ([0934c17](https://github.com/facebook/react-native/commit/0934c1778f0e3c0b691e1a3ca2df1d486eb905dd))
- 修复 `run-ios` 无法打开ios模拟器的bug ([9736ddc](https://github.com/facebook/react-native/commit/9736ddc061e9c4291df8a3185c7f9d6f73e435c7))
- 为 Fishhook 使用正确的依赖库。 这将修复 Xcode 9 和 Xcode 10 上的编译错误。 ([a8b7457](https://github.com/facebook/react-native/commit/a8b74576da6f1a42fde4e39f97e88c8f45a3a51d))
- 将缺少的 `onChange` 事件定义添加至 `DatePickerIOS` ([3b53091](https://github.com/facebook/react-native/commit/3b53091869b673ea33a4af34242e2227ca944768))
- 修复调用 Xcode 9.3 编译打包阶段引起的崩溃 ([344c205](https://github.com/facebook/react-native/commit/344c205070d5ad670c97984dd86ec9ac13c73f81))
- `RNTesterPods`: 添加缺少的依赖 ([128c934](https://github.com/facebook/react-native/commit/128c9343c464f3e7898d6e245f135f8bdf6caa6a))
- `RNTesterPods`: 将参数 `has_value()` 修正至 `hasValue()` ([128c934](https://github.com/facebook/react-native/commit/128c9343c464f3e7898d6e245f135f8bdf6caa6a))
- `RNTesterPods`: 修正引入的依赖 `RCTTestAttributes.h` ([128c934](https://github.com/facebook/react-native/commit/128c9343c464f3e7898d6e245f135f8bdf6caa6a))
- `RNTesterPods`: 修正 `conversions.h` 以使用正确的命名空间 ([128c934](https://github.com/facebook/react-native/commit/128c9343c464f3e7898d6e245f135f8bdf6caa6a))
- Fix or mark enum conversions surfaced by `-Wenum-conversion` ([b8f30db](https://github.com/facebook/react-native/commit/b8f30db0ae21d5f96547702abbf50aefa93b1094))
- 在缺少 DevSupport subspec 的情况下修正 CocoaPods 集成 ([c09d509](https://github.com/facebook/react-native/commit/c09d509c2b8a5a02701829e1f0ace8081ce64277))
- 更新 Yoga 以处理 Xcode 框架项目中的内容 ([cf036db](https://github.com/facebook/react-native/commit/cf036dbc7af16a8453c115372694dc51e8086fcf))
- 修正 Blob 内存泄露 ([122b379](https://github.com/facebook/react-native/commit/122b3791ede095345f44666691aa9ce5aa7f725a))
- 重加载 JS 时避免出现双重加载错误 ([b348aa1](https://github.com/facebook/react-native/commit/b348aa14d483cc6b33ba92637647c4987c9478c1))
- 取消关于 RCTCxxModule 的错误警告 ([af76473](https://github.com/facebook/react-native/commit/af76473c2e344c13ecac054b5a5568a0b94128e5))

#### Android 修正
- 修正 `TextInput` 在 Android 上的异常缓慢bug ([1b4187f](https://github.com/facebook/react-native/commit/1b4187fc414352cd3724e2d4df2009f5a045fe3f))
- 修正绘制边框的路径尺寸，避免出现边框模糊的情况 ([c5ca26a](https://github.com/facebook/react-native/commit/c5ca26a0e5c0660196300ee34d6007c63879611f))
- 不要在 `.android.js` 文件中向 `requireNativeComponent` 传递参数  ([a51e8b1](https://github.com/facebook/react-native/commit/a51e8b19cc4dc36dee42ac95278b883c06b2e40f))
- 当父级组件滚动时，避免 `RefreshControl` 被卡住  ([33ffa79](https://github.com/facebook/react-native/commit/33ffa79a51d4db9ba69148861f2da304646175cd))
- 防止不被支持的 ellipsize 模式导致应用崩溃 ([85e33aa](https://github.com/facebook/react-native/commit/85e33aaf908996e99220bff4a2bdbbdf7c0d12b0))
- 修复 `DevServerHelper` 中的 okhttp3 响应处理bug  ([56d48bd](https://github.com/facebook/react-native/commit/56d48bd9ecd2d0f08625259121312531064a09f2))
- 修复 `ReactInstanceManager` unmountApplication 以支持 `ReactRootView` 回收 ([4a9b2a7](https://github.com/facebook/react-native/commit/4a9b2a73021fb547febe1fa193c3effb7ff8da4e))
- Fix `NullPointerException` when emiting event using `UIManagerModule` ([291c01f](https://github.com/facebook/react-native/commit/291c01f4ffe614760852e36b05d78b42cb4271df))
- 修复 Android 构建向导的 link ([57e7556](https://github.com/facebook/react-native/commit/57e7556b8db61e5fcc3ccea56c1b163b82a091a6))
- Fix Android open source test failures ([3e0ebc7](https://github.com/facebook/react-native/commit/3e0ebc76632238f21c60caa92c7a2b5ee8102b71))
- 修复视图索引 LayoutAnimation ([d8fcdb9](https://github.com/facebook/react-native/commit/d8fcdb9bd7a308ed70caeac1b53da0a05abe452f))
- 修复 originalNode 内存泄露 ([8102e35](https://github.com/facebook/react-native/commit/8102e35271ab68e0525a9c60d86a855bbeef9c1a))
- 修复 `ScrollView` 中的 `TextInput` BUG ([2f1421d](https://github.com/facebook/react-native/commit/2f1421dec7cd3a35779caceac108e872033c7d72))
- Disable onKeyPRess logic when handler not defined ([41975f7](https://github.com/facebook/react-native/commit/41975f75d96ef4b606b4618461bf24d5db063b77))
- 在 pre-M android上修复权限请求 ([6d27bd1](https://github.com/facebook/react-native/commit/6d27bd182fa87cab0c68ca281c869b987cbd2ca6))

---

### 移除：已移除的功能

- 弃用 `focusTextInput` 和 `blurTextInput` ([ce3b7b8](https://github.com/facebook/react-native/commit/ce3b7b8204dad0fd62a76a0ce66472eca4b25bc8))
- *[BREAKING]* `ImageResizeMode` on `Image` is no longer exposed; check your usage of `resizeMode`; the same resize modes exist, but pass them as strings instead ([870775e](https://github.com/facebook/react-native/commit/870775e) by [@TheSavior](https://github.com/TheSavior))

#### Android 功能移除

- 移除原生扩展 ([7c5845a](https://github.com/facebook/react-native/commit/7c5845a5a26592598c9380df078766a680a23f06))
- 移除 Fresco ProGuard 规则 ([07df365](https://github.com/facebook/react-native/commit/07df36557c8cbbaee5e870460162aa725a606ff4))

#### iOS 功能移除

- 移除已弃用的 `UIActionSheetDelegate` 方法 ([5863b56](https://github.com/facebook/react-native/commit/5863b564f84b9fe97b256f8cde0f7f2e1db9b641))

---

### 已知的问题

在此版本的 RC 测试期间，部分问题还没有最终解决方案( [19827](https://github.com/facebook/react-native/issues/19827), [19763](https://github.com/facebook/react-native/issues/19763), [19859](https://github.com/facebook/react-native/issues/19859), [19955](https://github.com/facebook/react-native/issues/19955) )。 我们知道这些问题的存在，希望通过发布0.56.0版本，能促进开发人员找到最终的解决方案，从而实现更快的分辨率和更好的0.56.1版本。 因此，请在提交新问题之前检查已经提交的问题。

如果您使用Windows开发React Native应用程序，我们建议您特别关注这些[问题（issue）](https://github.com/facebook/react-native/issues/19953)，因为有很多关于 Win 10 和 RN 0.56 相关问题的报告。