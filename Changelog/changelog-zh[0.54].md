## [0.54]

> 译者注：由于个人水平有限，另外翻译changelog需要阅读大量PR，翻译可能有不准确的地方，望谅解。如果发现有翻译不准确的地方，可以留言或是于Github上提交:[react-native-docsZh](https://github.com/wlfcss/react-native-docsZh)。

欢迎来到2018年2月发布的 React Native 版本更新！ 由React Native团队和社区完成的工作都包含在此版本中，在假期后这里也有诸多改变。 感谢来自87位贡献者的270次提交，感谢你们！ 以下是该版本的要点：

- 期待已久的 **Blob** 改进：包含 upload（上传），download（下载），fetch locally 等等
- Sticky headers now work on inverted Lists
- Update to the newest React, which deprecated some lifecycle methods and added new ones – expect Yellowbox until React Native is updated
- `Space-evenly` is now there (sorry for the confusion with 0.52's release notes)
- A lot of under-the-covers work on Yoga, iOS's **Text** and **TextInput**, and a ton of other areas
- Multiple crash fixes

The changelog is arranged by the customary added, removed, changed, and fixed plus internal; the changes are also organized by platform.

### Added

- ✨ **Blob**s now can be: made from Strings, loaded by File using a FileReader API, uploaded and downloaded via `XMLHttpRequest#fetch`, and fetched on files to a local blob consistently ([be56a3e](https://github.com/facebook/react-native/commit/be56a3e) and [854c233](https://github.com/facebook/react-native/commit/854c233) by [@satya164](https://github.com/satya164) and [@fkgozali](https://github.com/fkgozali))
- Dynamic node_module dependencies are now supported ([b5e19ad](https://github.com/facebook/react-native/commit/b5e19ad) by [@jeanlauliac](https://github.com/jeanlauliac))
- Support sticky headers for inverted Lists with `invertStickyHeaders` ([ecaca80](https://github.com/facebook/react-native/commit/ecaca80) by [@janicduplessis](https://github.com/janicduplessis))
- `space-evenly` is now supported (sorry for the confusion with 0.52 notes) ([b1cdb7d](https://github.com/facebook/react-native/commit/b1cdb7d) by [@gedeagas](https://github.com/gedeagas))
- Platform plugins can participate in RNConfig, `link`, and `unlink` – keep an eye on [react-native-window's use of it](https://github.com/Microsoft/react-native-windows/pull/1601)! ([a40bfa7](https://github.com/facebook/react-native/commit/a40bfa7) by [@rozele](https://github.com/rozele))
- Add `minify` flag to react-native bundle command ([3f969cb](https://github.com/facebook/react-native/commit/3f969cb) by [@tomduncalf](https://github.com/tomduncalf))

#### VR Specific Additions

- Added **ScrollView** support ([6fa039d](https://github.com/facebook/react-native/commit/6fa039d) by [@MartinSherburn](https://github.com/MartinSherburn))

#### Android Specific Additions

- Bundle download progress is now shown like iOS ([675f142](https://github.com/facebook/react-native/commit/675f142) by [@janicduplessis](https://github.com/janicduplessis))
- Add back ability to customise OkHttp client ([22efd95](https://github.com/facebook/react-native/commit/22efd95) by [@cdlewis](https://github.com/cdlewis))

#### iOS specific additions

- **ScrollView** now supports smooth bi-directional content loading and takes new prop `maintainVisibleContentPosition` ([cae7179](https://github.com/facebook/react-native/commit/cae7179) and [65184ec](https://github.com/facebook/react-native/commit/65184ec) by [@sahrens](https://github.com/sahrens))
- Allow substituting a default font handler ([a9c684a](https://github.com/facebook/react-native/commit/a9c684a) by [@mmmulani](https://github.com/mmmulani))
- Add `accessibilityElementsHidden` prop ([3128816](https://github.com/facebook/react-native/commit/3128816) by [@aputinski](https://github.com/aputinski))
- Add EXTRA_PACKAGER_ARGS extensibility point on `scripts/react-native-xcode.sh` (PR rev [2122140](https://github.com/facebook/react-native/commit/2122140) by [@brunolemos](https://github.com/brunolemos) with landing assists [b8c86b8](https://github.com/facebook/react-native/commit/b8c86b8) and [0d4ff1b](https://github.com/facebook/react-native/commit/0d4ff1b))

### Removed

- Remove internal `utf8` utility - use the **utf8** package now instead ([431670f](https://github.com/facebook/react-native/commit/431670f) by [@mathiasbynens](https://github.com/mathiasbynens))

#### iOS specific removals

- Removed outdated assertion in RCTShadowView related to breaking change in Yoga ([e3ff3cf](https://github.com/facebook/react-native/commit/e3ff3cf) by [@shergin](https://github.com/shergin))

#### Android specific removals

- Fix an issue when swapping to and from the `visible-password` or `phone-pad` keyboard types. ([164f6b6](https://github.com/facebook/react-native/commit/164f6b6) by [@BrandonWilliamsCS](https://github.com/BrandonWilliamsCS))
- Remove redundant config in AndroidManifest.xml ([d7a9ca2](https://github.com/facebook/react-native/commit/d7a9ca2) by [@gengjiawen](https://github.com/gengjiawen))

#### iOS specific removals

- Delete RCTBatchedBridge ([816d417](https://github.com/facebook/react-native/commit/816d417) by [@mhorowitz](https://github.com/mhorowitz))

### Changed

- Docs clarifications ([7abffc3](https://github.com/facebook/react-native/commit/7abffc3) by [@IgorGanapolsky](https://github.com/IgorGanapolsky))

#### iOS Specific Changes

- ⚡️ **Text** and **TextInput** have been re-implemented from the ground up for performance, flexibility, and reduced technical debt ([2716f53](https://github.com/facebook/react-native/commit/2716f53), [ef4214a](https://github.com/facebook/react-native/commit/ef4214a), [0009909](https://github.com/facebook/react-native/commit/0009909), [74963eb](https://github.com/facebook/react-native/commit/74963eb), [6c4ef28](https://github.com/facebook/react-native/commit/6c4ef28), [ebc9884](https://github.com/facebook/react-native/commit/ebc9884), [d7fa81f](https://github.com/facebook/react-native/commit/d7fa81f), [7d1ec7a](https://github.com/facebook/react-native/commit/7d1ec7a), [5264832](https://github.com/facebook/react-native/commit/5264832), [6bb8617](https://github.com/facebook/react-native/commit/6bb8617), [5dbb3c5](https://github.com/facebook/react-native/commit/5dbb3c5), [7e7d00a](https://github.com/facebook/react-native/commit/7e7d00a), [46fd864](https://github.com/facebook/react-native/commit/46fd864), [9dfa2e7](https://github.com/facebook/react-native/commit/9dfa2e7), [8a882fe](https://github.com/facebook/react-native/commit/8a882fe), and [0f9fc4b](https://github.com/facebook/react-native/commit/0f9fc4b) by [@shergin](https://github.com/shergin) and [@hovox](https://github.com/hovox))
- **Image**'s `resizeMode="center"` is now documented and has an example present ([be7037f](https://github.com/facebook/react-native/commit/be7037f) by [@motiz88](https://github.com/motiz88))
- Geolocation API no longer timeouts when `skipPermissionRequests: true` ([5c17db8](https://github.com/facebook/react-native/commit/5c17db8) by [@ngandhy](https://github.com/ngandhy))
- Rounding pixels is now done with an algorithm from Yoga rather than React Native, reducing debt and improving performance ([ceb1d1c](https://github.com/facebook/react-native/commit/ceb1d1c) and [114c258](https://github.com/facebook/react-native/commit/114c258) by [@shergin](https://github.com/shergin))

#### Android specific changes

- Numerous refactors around bundle handling and the `DevServerHelper` ([644123a](https://github.com/facebook/react-native/commit/644123a), [e756251](https://github.com/facebook/react-native/commit/e756251), [6e44356](https://github.com/facebook/react-native/commit/6e44356), [1019bda](https://github.com/facebook/react-native/commit/1019bda), [06d8f96](https://github.com/facebook/react-native/commit/06d8f96), [f88c9d6](https://github.com/facebook/react-native/commit/f88c9d6), and [108f966](https://github.com/facebook/react-native/commit/108f966) by [@davidaurelio](https://github.com/davidaurelio))

### Fixed

- Fix JS debugger issues related to CORS ([29f8354](https://github.com/facebook/react-native/commit/29f8354) by [@njbmartin](https://github.com/njbmartin))
- Keep the `.gitignore`d files during the `react-native-git-upgrade` process ([7492860](https://github.com/facebook/react-native/commit/7492860) by [@ncuillery](https://github.com/ncuillery))
- Fix re-render case on SwipeableRow ([a580a44](https://github.com/facebook/react-native/commit/a580a44))
- Fix display of syntax error messages when HMR is enabled ([2b80cdf](https://github.com/facebook/react-native/commit/2b80cdf) by [@ide](https://github.com/ide))
- Add fixtures to metro blacklist in order to let build succeed ([4194bb2](https://github.com/facebook/react-native/commit/4194bb2) by [@t4deu](https://github.com/t4deu))

#### Android specific fixes

- Don't crash when using decimal `Animated.modulo` values with `useNativeDriver: true` ([6c38972](https://github.com/facebook/react-native/commit/6c38972) by [@motiz88](https://github.com/motiz88))
- Don't crash when receiving unknown websocket IDs ([1a790f8](https://github.com/facebook/react-native/commit/1a790f8) by [@sunweiyang](https://github.com/sunweiyang))
- Dont crash when `NativeModules.UIManager.showPopupMenu` method calls error callback ([0c18ec5](https://github.com/facebook/react-native/commit/0c18ec5) by [@dryganets](https://github.com/dryganets))
- Maintain cursor position when **TextInput**'s `secureTextEntry` changes ([09b43e4](https://github.com/facebook/react-native/commit/09b43e4) by [@jainkuniya](https://github.com/jainkuniya))
- Race condition fix in Dialogs module ([d5e3f08](https://github.com/facebook/react-native/commit/d5e3f08) by [@dryganets](https://github.com/dryganets))
- Fix NPE in Android Switch during measure ([7b1915e](https://github.com/facebook/react-native/commit/7b1915e) by [@4ndroidev](https://github.com/4ndroidev))
- Fix initialScrollIndex ([ef596de](https://github.com/facebook/react-native/commit/ef596de) by [@olegbl](https://github.com/olegbl))
- Fix redbox style ([f363dfe](https://github.com/facebook/react-native/commit/f363dfe) by [@ayc1](https://github.com/ayc1))
- Fix crash due to mishandling of UTF-8 in progressive download. ([9024f56](https://github.com/facebook/react-native/commit/9024f56) by [@dryganets](https://github.com/dryganets))
- Fix crash because ClassCastException fix: getText() returns CharSequence not Spanned ([46cc490](https://github.com/facebook/react-native/commit/46cc490) by [@dryganets](https://github.com/dryganets))
- Fix and re-enable "view flattening" optimizations ([877f1cd](https://github.com/facebook/react-native/commit/877f1cd) by [@mdvacca](https://github.com/mdvacca))

#### iOS specific fixes

- Fix Crash when **CameraRoll** is getting assets from iCloud and no filename is provided ([2ae2436](https://github.com/facebook/react-native/commit/2ae2436) by [@pentarex](https://github.com/pentarex))
- Fix Xcode Archive task failing if project path contains whitespace ([8aa568e](https://github.com/facebook/react-native/commit/8aa568e) by [@jevakallio](https://github.com/jevakallio))
- `react-native link` has been fixed to correctly link iOS and tvOS targets ([a63fd37](https://github.com/facebook/react-native/commit/a63fd37) by [@dlowder-salesforce](https://github.com/dlowder-salesforce))
- `GLog` fix on case sensitive APFS macOS ([2fef1ba](https://github.com/facebook/react-native/commit/2fef1ba) by [@hovox](https://github.com/hovox))
- Fixed issue where you cannot launch tvOS app on Apple TV simulator ([afd988f](https://github.com/facebook/react-native/commit/afd988f))

### Internal work

- A **massive** amount of Yoga optimizations, cleanups, refactors, and test fixes ([62d0100](https://github.com/facebook/react-native/commit/62d0100), [1475fc4](https://github.com/facebook/react-native/commit/1475fc4), [9daa174](https://github.com/facebook/react-native/commit/9daa174), [d4517dd](https://github.com/facebook/react-native/commit/d4517dd), [ca91f0e](https://github.com/facebook/react-native/commit/ca91f0e), [34b7ec8](https://github.com/facebook/react-native/commit/34b7ec8), [fda861a](https://github.com/facebook/react-native/commit/fda861a), [9f7cedb](https://github.com/facebook/react-native/commit/9f7cedb), [ac1c8c2](https://github.com/facebook/react-native/commit/ac1c8c2), [fcf2c7c](https://github.com/facebook/react-native/commit/fcf2c7c), [2b27f1a](https://github.com/facebook/react-native/commit/2b27f1a), [210ae5b](https://github.com/facebook/react-native/commit/210ae5b), [8208858](https://github.com/facebook/react-native/commit/8208858), [7f94bff](https://github.com/facebook/react-native/commit/7f94bff), [bd7bf94](https://github.com/facebook/react-native/commit/bd7bf94), [2fe65b0](https://github.com/facebook/react-native/commit/2fe65b0), [9658d9f](https://github.com/facebook/react-native/commit/9658d9f), [ee5c91c](https://github.com/facebook/react-native/commit/ee5c91c), [64d530b](https://github.com/facebook/react-native/commit/64d530b), [400a29e](https://github.com/facebook/react-native/commit/400a29e), [f75e21f](https://github.com/facebook/react-native/commit/f75e21f), [528bbac](https://github.com/facebook/react-native/commit/528bbac), [be8e7c6](https://github.com/facebook/react-native/commit/be8e7c6), [d0f7d4d](https://github.com/facebook/react-native/commit/d0f7d4d), [4b4959a](https://github.com/facebook/react-native/commit/4b4959a), [fdef378](https://github.com/facebook/react-native/commit/fdef378), [831a1bb](https://github.com/facebook/react-native/commit/831a1bb), ([2a22d99](https://github.com/facebook/react-native/commit/2a22d99), [9f57ded](https://github.com/facebook/react-native/commit/9f57ded), and [ff2658c](https://github.com/facebook/react-native/commit/ff2658c) by [@priteshrnandgaonkar](https://github.com/priteshrnandgaonkar), [@passy](https://github.com/passy), [@ryu2](https://github.com/ryu2)), and others)
- 🚧 Lifecycle methods were renamed to be consistent with [React RFC6](https://github.com/reactjs/rfcs/blob/master/text/0006-static-lifecycle-methods.md) – note that there are Yellowbox warnings right now because of this, it's work-in-progress ([6f007e8](https://github.com/facebook/react-native/commit/6f007e8) by [@bvaughn](https://github.com/bvaughn))
- Some autogenerated mystery string files were added ([c7846c4](https://github.com/facebook/react-native/commit/c7846c4), [bb6fcea](https://github.com/facebook/react-native/commit/bb6fcea), [8bd00a2](https://github.com/facebook/react-native/commit/8bd00a2), [faa9519](https://github.com/facebook/react-native/commit/faa9519), [f49f793](https://github.com/facebook/react-native/commit/f49f793))
- Improvements to the cli's implementation ([2c5fbd7](https://github.com/facebook/react-native/commit/2c5fbd7), [752427b](https://github.com/facebook/react-native/commit/752427b), and [619a8c9](https://github.com/facebook/react-native/commit/619a8c9) by [@arcanis](https://github.com/arcanis), [@voideanvalue](https://github.com/voideanvalue), and [@rozele](https://github.com/rozele))
- Measure touch events from nearest "root view" ([a70fdac](https://github.com/facebook/react-native/commit/a70fdac) by [@mmmulani](https://github.com/mmmulani))
- Allow to attach the HMR server to an external http server ([8c6b816](https://github.com/facebook/react-native/commit/8c6b816) by [@rafeca](https://github.com/rafeca))
- Split folly/Memory out from headers-only targets in Buck ([b8e79a7](https://github.com/facebook/react-native/commit/b8e79a7) by [@mzlee](https://github.com/mzlee))
- Code cleanup of **ReactHorizontalScrollView** in Android ([71ec85f](https://github.com/facebook/react-native/commit/71ec85f) by [@mdvacca](https://github.com/mdvacca))
- Always create a debugger websocket connection when in iOS dev builds ([fa334ce](https://github.com/facebook/react-native/commit/fa334ce) by [@bnham](https://github.com/bnham))
- Make the React Native HMR client extend from the generic metro HMR client ([9a19867](https://github.com/facebook/react-native/commit/9a19867) by [@rafeca](https://github.com/rafeca))
- Removed use of xip.io ([40a8434](https://github.com/facebook/react-native/commit/40a8434) by [@jvranish](https://github.com/jvranish))
- Fix Buck dependencies ([cec2e80](https://github.com/facebook/react-native/commit/cec2e80), [4f6c157](https://github.com/facebook/react-native/commit/4f6c157) by [@swolchok](https://github.com/swolchok))
- Fix permissions on test script ([42c410a](https://github.com/facebook/react-native/commit/42c410a) by [@mzlee](https://github.com/mzlee))
- Better handling exception in loadScript() ([3fbf785](https://github.com/facebook/react-native/commit/3fbf785))
- Fix ESLint upgrade "parsing error" ([9d21496](https://github.com/facebook/react-native/commit/9d21496) by [@zertosh](https://github.com/zertosh))
- Fixing 🤡 in RCTSurfaceRootShadowView ([5fba82d](https://github.com/facebook/react-native/commit/5fba82d) by [@shergin](https://github.com/shergin))
- Handle invalidation error in RCTObjcExecutor ([493f3e8](https://github.com/facebook/react-native/commit/493f3e8) by [@fromcelticpark](https://github.com/fromcelticpark))
- Check for nullptr when accessing isInspectable method ([70d23e8](https://github.com/facebook/react-native/commit/70d23e8) by [@fromcelticpark](https://github.com/fromcelticpark))
- Introduce new Fabric API in RNAndroid ([2d35bde](https://github.com/facebook/react-native/commit/2d35bde) by [@mdvacca](https://github.com/mdvacca))
- Fixing Prepack model for latest global.nativeExtensions changes. ([01a58d1](https://github.com/facebook/react-native/commit/01a58d1) by [@NTillmann](https://github.com/NTillmann))
- General code cleanup: unused code and configurations ([e233646](https://github.com/facebook/react-native/commit/e233646) and [e701034](https://github.com/facebook/react-native/commit/e701034) by [@bvaughn](https://github.com/bvaughn) and others)
- Add support for finding multiple views with NativeIds using a single listener to Android ([f5efc46](https://github.com/facebook/react-native/commit/f5efc46) by [@axe-fb](https://github.com/axe-fb))
- Add CountingOutputStream ([a5e135a](https://github.com/facebook/react-native/commit/a5e135a) by [@hramos](https://github.com/hramos))
- Changes from Prettier ([b815eb5](https://github.com/facebook/react-native/commit/b815eb5), [e758cb7](https://github.com/facebook/react-native/commit/e758cb7), [bf9cabb](https://github.com/facebook/react-native/commit/bf9cabb), and [a5af841](https://github.com/facebook/react-native/commit/a5af841) by [@shergin](https://github.com/shergin))
- Typos in code ([8ffc16c](https://github.com/facebook/react-native/commit/8ffc16c) by [@ss18](https://github.com/ss18))
- Support for inherited events in view managers ([2afe7d4](https://github.com/facebook/react-native/commit/2afe7d4) by [@shergin](https://github.com/shergin))
- Flow types changes ([3fc33bb](https://github.com/facebook/react-native/commit/3fc33bb), [e485cde](https://github.com/facebook/react-native/commit/e485cde),  [83ed9d1](https://github.com/facebook/react-native/commit/83ed9d1), [52ffa5d](https://github.com/facebook/react-native/commit/52ffa5d), [d37cdd9](https://github.com/facebook/react-native/commit/d37cdd9), [6e7fb01](https://github.com/facebook/react-native/commit/6e7fb01), [d99ba70](https://github.com/facebook/react-native/commit/d99ba70), [bcfbdf4](https://github.com/facebook/react-native/commit/bcfbdf4), and [a1c479f](https://github.com/facebook/react-native/commit/a1c479f) by [@alexeylang](https://github.com/alexeylang), [@sahrens](https://github.com/sahrens), [@yungsters](https://github.com/yungsters), and [@zjj010104](https://github.com/zjj010104))
- Give IInspector a virtual destructor for correct InspectorImpl destruction ([2a3c37f](https://github.com/facebook/react-native/commit/2a3c37f) by [@toulouse](https://github.com/toulouse))
- Migrated `SourceCode` and `DeviceInfoModule` out of Native Modules ([47fe523](https://github.com/facebook/react-native/commit/47fe523) and [429fcc8](https://github.com/facebook/react-native/commit/429fcc8))
- Jest config change as part of bringing back support for the `assetPlugin` option in Metro ([af6450c](https://github.com/facebook/react-native/commit/af6450c) by [@ide](https://github.com/ide))
- Nested virtualized lists should receive recordInteration events ([ae2d5b1](https://github.com/facebook/react-native/commit/ae2d5b1))
- Upgrade connect dependency ([709ede7](https://github.com/facebook/react-native/commit/709ede7) by [@rafeca](https://github.com/rafeca))
- xplat/js: asyncRequire: redirect async modules to control modules ([5e11b88](https://github.com/facebook/react-native/commit/5e11b88) by [@jeanlauliac](https://github.com/jeanlauliac))
- More progress towards split bundle support ([1a1a956](https://github.com/facebook/react-native/commit/1a1a956) and [9e34cbd](https://github.com/facebook/react-native/commit/9e34cbd) by [@fromcelticpark](https://github.com/fromcelticpark))
- Implement bundle sync status ([88980f2](https://github.com/facebook/react-native/commit/88980f2))
- Various improvements to RCTSurface and RCTShadowView ([7d9e902](https://github.com/facebook/react-native/commit/7d9e902), [06ebaf2](https://github.com/facebook/react-native/commit/06ebaf2), [6882132](https://github.com/facebook/react-native/commit/6882132), and [193a2bd](https://github.com/facebook/react-native/commit/193a2bd) by [@shergin](https://github.com/shergin))
- Progress towards experimental ReactFabric and FabricUIManager ([b1e5c01](https://github.com/facebook/react-native/commit/b1e5c01), [fa0ac92](https://github.com/facebook/react-native/commit/fa0ac92), [94dac23](https://github.com/facebook/react-native/commit/94dac23) by [@fkgozali](https://github.com/fkgozali))
- (almost) kill fbjsc ([702b7e8](https://github.com/facebook/react-native/commit/702b7e8) by [@michalgr](https://github.com/michalgr))
- Refactored bridge ReadableNativeMap and ReadableNativeArray to add centralized accesses ([7891805](https://github.com/facebook/react-native/commit/7891805), [28be33a](https://github.com/facebook/react-native/commit/28be33a), and [5649aed](https://github.com/facebook/react-native/commit/5649aed))
- Removed unused core from Image.android.js ([ce3146a](https://github.com/facebook/react-native/commit/ce3146a) by [@shergin](https://github.com/shergin))
- Capture StackOverflowExceptions triggered when drawing a ReactViewGroup or ReactRootView and log more debugging information for it ([1aac962](https://github.com/facebook/react-native/commit/1aac962) and [4d3519c](https://github.com/facebook/react-native/commit/4d3519c) by [@mdvacca](https://github.com/mdvacca))
- `babel-preset-react-native`: only require plugins once ([df6c48c](https://github.com/facebook/react-native/commit/df6c48c) by [@davidaurelio](https://github.com/davidaurelio))
- Report module id as string and as double, in case of invalid values are passed to nativeRequire ([8f358a2](https://github.com/facebook/react-native/commit/8f358a2) by [@fromcelticpark](https://github.com/fromcelticpark))
- More work moving build configurations to Skylark ([d3db764](https://github.com/facebook/react-native/commit/d3db764), [869866c](https://github.com/facebook/react-native/commit/869866c), [a8c95d2](https://github.com/facebook/react-native/commit/a8c95d2), and [79a63d0](https://github.com/facebook/react-native/commit/79a63d0) by [@mzlee](https://github.com/mzlee), [@ttsugriy](https://github.com/ttsugriy), and others)
- `[RCTShadowView isHidden]` was removed ([c19bc79](https://github.com/facebook/react-native/commit/c19bc79) by [@shergin](https://github.com/shergin))
- Remove unused `packagerInstance` option and rename it to `server` ([bbbc18c](https://github.com/facebook/react-native/commit/bbbc18c))
- The blog has moved to [react-native-website](https://github.com/facebook/react-native-website/tree/master/website/blog) ([e16d673](https://github.com/facebook/react-native/commit/e16d673) by [@hramos](https://github.com/hramos))
- Remove SoLoaderShim, use SoLoader ([fc6dd78](https://github.com/facebook/react-native/commit/fc6dd78) by [@foghina](https://github.com/foghina))
- Removed broken link for 'Getting Help' in the README ([b3a306a](https://github.com/facebook/react-native/commit/b3a306a) by [@rickydam](https://github.com/rickydam))
- Changed to use boost-for-react-native cocoapod, which speeds up `pod install` a ton; this was in 0.53 originally but had to be re-added ([d40db3a](https://github.com/facebook/react-native/commit/d40db3a) by [@CFKevinRef](https://github.com/CFKevinRef))
- Remove fbobjc's RN copy ([af0c863](https://github.com/facebook/react-native/commit/af0c863))
- Measure time to create **ReactInstanceManager** ([6224ef5](https://github.com/facebook/react-native/commit/6224ef5) by [@alexeylang](https://github.com/alexeylang))
- Upgrade create-react-class to v15.6.3 ([74f3866](https://github.com/facebook/react-native/commit/74f3866) by [@bvaughn](https://github.com/bvaughn))
- Upgrade react-devtools to v3.1.0 ([8235a49](https://github.com/facebook/react-native/commit/8235a49) by [@bvaughn](https://github.com/bvaughn))
- Upgrade flow to v0.65.0 ([7aba456](https://github.com/facebook/react-native/commit/7aba456) and [298f3bb](https://github.com/facebook/react-native/commit/298f3bb) by [@avikchaudhuri](https://github.com/avikchaudhuri) and [@mroch](https://github.com/mroch))
- Upgrade Jest to v22.2.1 ([46f4d3e](https://github.com/facebook/react-native/commit/46f4d3e) and [24e521c](https://github.com/facebook/react-native/commit/24e521c) by [@mjesun](https://github.com/mjesun))
- Upgrade ESLint to v4.17.0 (plus update related deps) ([bba19e8](https://github.com/facebook/react-native/commit/bba19e8) by [@zertosh](https://github.com/zertosh))
- Upgrade React to v16.3.0-alpha.1 ([03d7b2a](https://github.com/facebook/react-native/commit/03d7b2a) and [5e80d95](https://github.com/facebook/react-native/commit/5e80d95) by [@grabbou](https://github.com/grabbou) and [@hramos](https://github.com/hramos))
- Synced React and ReactFabric render ([c7ed03a](https://github.com/facebook/react-native/commit/c7ed03a), [1382975](https://github.com/facebook/react-native/commit/1382975), and [d676746](https://github.com/facebook/react-native/commit/d676746) by [@bvaughn](https://github.com/bvaughn))
- Upgrade metro to v0.26.0 ([9e6f3b8](https://github.com/facebook/react-native/commit/9e6f3b8), [ce50f25](https://github.com/facebook/react-native/commit/ce50f25), [e9b83e6](https://github.com/facebook/react-native/commit/e9b83e6), [2fe7483](https://github.com/facebook/react-native/commit/2fe7483), [0f96ebd](https://github.com/facebook/react-native/commit/0f96ebd), [0de470e](https://github.com/facebook/react-native/commit/0de470e), [e8893a0](https://github.com/facebook/react-native/commit/e8893a0), and [f4fde9d](https://github.com/facebook/react-native/commit/f4fde9d) by [@rafeca](https://github.com/rafeca) and [@grabbou](https://github.com/grabbou))
- Add Context to Redbox report api ([e3c27f5](https://github.com/facebook/react-native/commit/e3c27f5) by [@ayc1](https://github.com/ayc1))
- GitHub bot commands have been disabled in the short term ([b973fe4](https://github.com/facebook/react-native/commit/b973fe4) by [@hramos](https://github.com/hramos))
- Various CI configuration changes ([17bd6c8](https://github.com/facebook/react-native/commit/17bd6c8), [51b6749](https://github.com/facebook/react-native/commit/51b6749), [a2f3ba8](https://github.com/facebook/react-native/commit/a2f3ba8), [2ef9b7f](https://github.com/facebook/react-native/commit/2ef9b7f), [40b1792](https://github.com/facebook/react-native/commit/40b1792), [613afba](https://github.com/facebook/react-native/commit/613afba), [da8bec9](https://github.com/facebook/react-native/commit/da8bec9), [fa11fae](https://github.com/facebook/react-native/commit/fa11fae), [f50af7f](https://github.com/facebook/react-native/commit/f50af7f), [9227ba7](https://github.com/facebook/react-native/commit/9227ba7), [365a4d4](https://github.com/facebook/react-native/commit/365a4d4), [b58d848](https://github.com/facebook/react-native/commit/b58d848), [c8e98bb](https://github.com/facebook/react-native/commit/c8e98bb), [f5975a9](https://github.com/facebook/react-native/commit/f5975a9), and [605a6e4](https://github.com/facebook/react-native/commit/605a6e4) by [@hramos](https://github.com/hramos), [@grabbou](https://github.com/grabbou), and [@dryganets](https://github.com/dryganets))
- Restore copyright header ([4f883bd](https://github.com/facebook/react-native/commit/4f883bd) by [@hramos](https://github.com/hramos))
- Trim docs that are already present in the open source docs site ([28d60b6](https://github.com/facebook/react-native/commit/28d60b6) by [@hramos](https://github.com/hramos))
- Fix obsolete instructions about editing docs ([2f46712](https://github.com/facebook/react-native/commit/2f46712) by [@ExplodingCabbage](https://github.com/ExplodingCabbage))
- Fix links to beginner friendly issues ([c355a34](https://github.com/facebook/react-native/commit/c355a34) by [@hotchemi](https://github.com/hotchemi))
- Typos in comments and log messages ([d2c5697](https://github.com/facebook/react-native/commit/d2c5697) by [@ss18](https://github.com/ss18))
- Don't run the Danger CI tool through Flow ([1ea3065](https://github.com/facebook/react-native/commit/1ea3065) by [@hramos](https://github.com/hramos))
- Namespace custom ESLint rules through eslint-plugin-lint ([488b682](https://github.com/facebook/react-native/commit/488b682) by [@zertosh](https://github.com/zertosh))

- ... and now we're at 0.54 🎉 ([67e67ec](https://github.com/facebook/react-native/commit/67e67ec), [21dd3dd](https://github.com/facebook/react-native/commit/21dd3dd), [49e35bd](https://github.com/facebook/react-native/commit/49e35bd), [829f675](https://github.com/facebook/react-native/commit/829f675), and [294d95a](https://github.com/facebook/react-native/commit/294d95a) by [@grabbou](https://github.com/grabbou) and [@hramos](https://github.com/hramos))