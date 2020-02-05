## [0.60]

This feature release of React Native includes many milestone changes for the platform. Please refer to the [blog post](https://facebook.github.io/react-native/blog/2019/07/03/version-60) for selected details. For upgrading users, some of the progress comes with breaking changes; manual intervention may be required for your app. We're also aware that existing CocoaPods integrations using `use_frameworks` are not out-of-the-box compatible with this version, but please consider [various workarounds](https://github.com/facebook/react-native/issues/25349) while we prepare a long-term solution for a future release. If you're interested in helping evaluate our next release (0.61), subscribe to the dedicated issue [here](https://github.com/react-native-community/react-native-releases/issues/130).

Have you ever considered contributing to React Native itself? Be sure to check out [Contributing to React Native](https://github.com/facebook/react-native/blob/master/CONTRIBUTING.md).

### Added

- CLI autolinking support ([5954880](https://github.com/facebook/react-native/commit/5954880), [da7d3df](https://github.com/facebook/react-native/commit/da7d3df) by [@zhongwuzw](https://github.com/zhongwuzw) and [@hramos](https://github.com/hramos))
- New Intro screen ([6b393b2](https://github.com/facebook/react-native/commit/6b393b2), [233fddb](https://github.com/facebook/react-native/commit/233fddb), [fe88e9e](https://github.com/facebook/react-native/commit/fe88e9e), [aa926e3](https://github.com/facebook/react-native/commit/aa926e3), [a9e8a71](https://github.com/facebook/react-native/commit/a9e8a71), [ad4a5d9](https://github.com/facebook/react-native/commit/ad4a5d9), and [0245fd7](https://github.com/facebook/react-native/commit/0245fd7) by [@cpojer](https://github.com/cpojer), [@eliperkins](https://github.com/eliperkins), [@lucasbento](https://github.com/lucasbento), [@orta](https://github.com/orta), [@adamshurson](https://github.com/adamshurson), [@karanpratapsingh](https://github.com/karanpratapsingh) and [@glauberfc](https://github.com/glauberfc))
- Add enhanced accessibility actions support ([14b4668](https://github.com/facebook/react-native/commit/14b4668) by [@xuelgong](https://github.com/xuelgong))
- Add additional accessibility roles and states ([1aeac1c](https://github.com/facebook/react-native/commit/1aeac1c))
- Add `isReduceMotionEnabled()` plus `reduceMotionChanged` to `AccessibilityInfo` ([0090ab3](https://github.com/facebook/react-native/commit/0090ab3) by [@estevaolucas](https://github.com/estevaolucas)])
- Add support for cancelling fetch requests with `AbortController` ([h5e36b0c](https://github.com/facebook/react-native/commit/5e36b0c) by [@janicduplessis](https://github.com/janicduplessis))

#### Android specific

- Enable views to be nested within **Text**; this brings feature parity to Android, but be aware that it [has some limitations](https://github.com/facebook/react-native/commit/a2a03bc68ba062a96a6971d3791d291f49794dfd) ([a2285b1](https://github.com/facebook/react-native/commit/a2285b1) by [@rigdern](https://github.com/rigdern))
- Add a `touchSoundDisabled` prop to **Button**, **Touchable**, and **TouchableWithoutFeedback** ([45e77c8](https://github.com/facebook/react-native/commit/45e77c8) by [@yurykorzun](https://github.com/yurykorzun))

#### iOS specific

- Add `announceForAccessibility` and `announcementFinished` APIs for making screen reader announcemenets ([cfe0032](https://github.com/facebook/react-native/commit/cfe0032) by [@rigdern](https://github.com/rigdern))
- Ability to force network requests to use WiFi using the `allowsCellularAccess` property. This can ensure that network requests are sent over WiFi if communicating with a local hardware device and is accomplished by setting a flag. Default behavior of allowing network connections over cellular networks when available is unchanged. ([01c70f2](https://github.com/facebook/react-native/commit/01c70f2) and [916186a](https://github.com/facebook/react-native/commit/916186a) by [@bondparkerbond](https://github.com/bondparkerbond)and [@zhongwuzw](https://github.com/zhongwuzw))
- `$RN_CACHE_DIR` can now be used to manually specify the iOS build cache directory ([845eee4](https://github.com/facebook/react-native/commit/845eee4) by [@hramos](https://github.com/hramos))

### Changed

- *BREAKING* Migrated to AndroidX; please see [this thread](https://github.com/react-native-community/discussions-and-proposals/issues/129#issuecomment-503829184) for more details on this change
- Cleanup **RedBox** message and stack output; it's now far easier to understand ([49d26eb](https://github.com/facebook/react-native/commit/49d26eb) by [@thymikee](https://github.com/thymikee))
- Add default `scrollEventThrottle` value to **Animated.FlatList** and **Animated.SectionList**; this now behaves consistently with **Animated.ScrollView** ([933e65e](https://github.com/facebook/react-native/commit/933e65e) by [@janicduplessis](https://github.com/janicduplessis))
- Remove invariant on nested sibling **VirtualizedLists** without unique listKey props; they now trigger a **RedBox** ([af5633b](https://github.com/facebook/react-native/commit/af5633b))
- **FlatList** and **VirtualizedList**'s default `keyExtractor` now checks `item.id` and `item.key` ([de0d7cf](https://github.com/facebook/react-native/commit/de0d7cf) by [@sahrens](https://github.com/sahrens))
- **SectionList**'s `scrollToLocation` on iOS now counts `itemIndex` like Android; both platforms are now consistent, and the `itemIndex` value 0 now represents scrolling to the first heading ([248a108](https://github.com/facebook/react-native/commit/248a108) by [@vonovak](https://github.com/vonovak))
- Slightly speedup core initialization by moving native version check to DEV only ([5bb2277](https://github.com/facebook/react-native/commit/5bb2277) by [@mmmulani](https://github.com/mmmulani))
- `react` is now at v16.8.6 ([53cec2d](https://github.com/facebook/react-native/commit/53cec2d), [ee681b7](https://github.com/facebook/react-native/commit/ee681b7), and [6001acb](https://github.com/facebook/react-native/commit/6001acb) by [@kelset](https://github.com/kelset), [@mdvacca](https://github.com/mdvacca), [@gaearon](https://github.com/gaearon))
- `react-native-community/cli` is now at v2.0.0 (by [@thymikee](https://github.com/thymikee))
- `flow` is now at v0.98 ([0e1dfd4](https://github.com/facebook/react-native/commit/0e1dfd4) by [@nmote](https://github.com/nmote))
- `prettier` is now at v1.17.0 ([ff9f8f3](https://github.com/facebook/react-native/commit/ff9f8f3))
- `metro` packages are now at v0.54.1 ([7ff3874](https://github.com/facebook/react-native/commit/7ff3874), [343f0a1](https://github.com/facebook/react-native/commit/343f0a1) by [@motiz88](https://github.com/motiz88))
- Replace patched fetch polyfill with `whatwg-fetch@3.0` ([5447196](https://github.com/facebook/react-native/commit/5447196) by [@janicduplessis](https://github.com/janicduplessis))

#### Android specific

- Use class canonical name for `PARTIAL_WAKE_LOCK` tag ([88dbb45](https://github.com/facebook/react-native/commit/88dbb45) by [@timwangdev](https://github.com/timwangdev))

#### iOS specific

- *BREAKING*: Split React.podspec into separate podspecs for each Xcode project; your libraries will need to update for this change as well to avoid CocoaPods build errors ([2321b3f](https://github.com/facebook/react-native/commit/2321b3f) by [@fson](https://github.com/fson))
- Improve handling of native module exceptions; they are now propagated to crash reporting tools with the context and callstack ([629708b](https://github.com/facebook/react-native/commit/629708b) by [@pvinis](https://github.com/pvinis))
- Switch **Slider** `onSlidingComplete` event to a non-bubbling event on iOS to match Android ([7927437](https://github.com/facebook/react-native/commit/7927437) by [@rickhanlonii](https://github.com/rickhanlonii))

### Deprecated

- **StatusBar** is no longer deprecated; thank you for the feedback ([a203ebe](https://github.com/facebook/react-native/commit/a203ebe) by [@cpojer](https://github.com/cpojer))

### Removed

- **NetInfo** has been removed; its replacement is now available via the [react-native-community/netinfo](https://github.com/react-native-community/react-native-netinfo) package ([5a30c2a](https://github.com/facebook/react-native/commit/5a30c2a) by [@cpojer](https://github.com/cpojer))
- **WebView** has been removed; its replacement is now available via the [react-native-community/webview](https://github.com/react-native-community/react-native-webview) package ([](https://github.com/facebook/react-native/commit/6ca438a), [1ca9a95](https://github.com/facebook/react-native/commit/1ca9a95), and [954f715](https://github.com/facebook/react-native/commit/954f715) by [@cpojer](https://github.com/cpojer) and [@thorbenprimke](https://github.com/thorbenprimke))
- **Geolocation** has been removed; its replacement is now available via the [react-native-community/geolocation](https://github.com/react-native-community/react-native-geolocation) package ([17dbf98](https://github.com/facebook/react-native/commit/17dbf98) and [9834c58](https://github.com/facebook/react-native/commit/9834c58) by [@cpojer](https://github.com/cpojer) and [@mmmulani](https://github.com/mmmulani))

### Fixed

- Fix `Animated.Value` value after animation if component was re-mounted ([b3f7d53](https://github.com/facebook/react-native/commit/b3f7d53) by [@michalchudziak](https://github.com/michalchudziak))
- Consistent reporting native module name on crash on native side ([d6c33f9](https://github.com/facebook/react-native/commit/d6c33f9) and [b79d7db](https://github.com/facebook/react-native/commit/b79d7db) by [@DimitryDushkin](https://github.com/DimitryDushkin))
- Handle null filenames in symbolicated stack trace gracefully in **ExceptionsManager** ([2e8d39b](https://github.com/facebook/react-native/commit/2e8d39b) by [@motiz88](https://github.com/motiz88))
- Fix HasteImpl platform name regex ([28e0de0](https://github.com/facebook/react-native/commit/28e0de0) by [@CaptainNic](https://github.com/CaptainNic))
- Fix a JS memory leak in Blob handling; this resolves multiple leaks around `fetch` ([c5c79e5](https://github.com/facebook/react-native/commit/c5c79e5) and [9ef5107](https://github.com/facebook/react-native/commit/9ef5107) by [@janicduplessis](https://github.com/janicduplessis))
- **SectionList**'s `scrollToLocation` now scrolls to the top of the sticky header as expected ([d376a44](https://github.com/facebook/react-native/commit/d376a44) by [@danilobuerger](https://github.com/danilobuerger))

#### Android specific

- Fix duplicate resource error in Android build ([962437f](https://github.com/facebook/react-native/commit/962437f) and [eb534bc](https://github.com/facebook/react-native/commit/eb534bc) by [@mikehardy](https://github.com/mikehardy) and [@Dbroqua](https://github.com/Dbroqua))
- Reorder operations of native view hierarchy ([5f027ec](https://github.com/facebook/react-native/commit/5f027ec) by [@lunaleaps](https://github.com/lunaleaps))
- Fix performance regression from new custom fonts implementation ([fd6386a](https://github.com/facebook/react-native/commit/fd6386a) by [@dulmandakh](https://github.com/dulmandakh))
- Fix internal test case around disabled state of buttons ([70e2ab2](https://github.com/facebook/react-native/commit/70e2ab2))
- Fix extra call of **PickerAndroid**'s `onValueChange` on initialization; now it is only called when `selectedValue` changes ([82148da](https://github.com/facebook/react-native/commit/82148da) by [@a-c-sreedhar-reddy](https://github.com/a-c-sreedhar-reddy))
- Fix **PickerAndroid** will reset selected value during items update ([310cc38](https://github.com/facebook/react-native/commit/310cc38) by [@Kudo](https://github.com/Kudo))
- Fix unexpected PARTIAL_WAKE_LOCK when no headless tasks registered. ([bdb1d43](https://github.com/facebook/react-native/commit/bdb1d43) by [@timwangdev](https://github.com/timwangdev))
- Fix calling **TextInput**'s `onKeyPress` method when the user types an emoji ([a5c57b4](https://github.com/facebook/react-native/commit/a5c57b4))
- Fix value of **TextInput**'s `onSelectionChange` start and end arguments by normalizing them ([2ad3bb2](https://github.com/facebook/react-native/commit/2ad3bb2) by [@uqmessias](https://github.com/uqmessias))
- In `Linking.getInitialURL` method, use the `InteractionManager` to wait for the current activity to finish initializing ([c802d0b](https://github.com/facebook/react-native/commit/c802d0b) by [@mu29](https://github.com/mu29))
- Disable delta bundles on the first app run ([e4aff42](https://github.com/facebook/react-native/commit/e4aff42) by [@wojteg1337](https://github.com/wojteg1337))
- In **DatePickerAndroid**, work around Android Nougat bug displaying the wrong the spinner mode ([bb060d6](https://github.com/facebook/react-native/commit/bb060d6) by [@luancurti](https://github.com/luancurti))
- Fix crash in Animated Interpolation when inputMin === inputMax ([7abfd23](https://github.com/facebook/react-native/commit/7abfd23) by [@olegbl](https://github.com/olegbl))
- Fix symbolication for **RedBox** and **YellowBox** when using delta bundling ([a05e9f8](https://github.com/facebook/react-native/commit/a05e9f8) by [@motiz88](https://github.com/motiz88))
- Fix **CameraRoll** crash on mime type guessing ([ebeb893](https://github.com/facebook/react-native/commit/ebeb893) by [@Sroka](https://github.com/Sroka))

#### iOS specific

- Call designated initializer for SurfaceHostingProxyRootView ([3c125e8](https://github.com/facebook/react-native/commit/3c125e8) by [@zhongwuzw](https://github.com/zhongwuzw))
- Fix **RedBox** JS symbolication when adding JS engine tag to the message ([920632c](https://github.com/facebook/react-native/commit/920632c) by [@motiz88](https://github.com/motiz88))
- Fix **TextInput**'s `onSelectionChange` behavior in single line text inputs ([fc8008e](https://github.com/facebook/react-native/commit/fc8008e) by [@zhongwuzw](https://github.com/zhongwuzw))
- Fix accesibility problem with **TextInput** Clear Button ([4e37d37](https://github.com/facebook/react-native/commit/4e37d37) by [@shergin](https://github.com/shergin))
- Fix `renderingMode` not applied to GIF **Image**s ([75380aa](https://github.com/facebook/react-native/commit/75380aa) by [@zhongwuzw](https://github.com/zhongwuzw))
- Fix **ScrollView** `centerContent` not work in some cases ([2cdf969](https://github.com/facebook/react-native/commit/2cdf969) by [@zhongwuzw](https://github.com/zhongwuzw))
- Fix crash on performance logger ([5d3d398](https://github.com/facebook/react-native/commit/5d3d398) by [@zhigang1992](https://github.com/zhigang1992))
- Do not run packager in Release mode ([4ea6204](https://github.com/facebook/react-native/commit/4ea6204) by [@lucasbento](https://github.com/lucasbento))
- Fix `code` and `reason` arguments being ignored when calling `WebSocket.close` ([0ac2171](https://github.com/facebook/react-native/commit/0ac2171) by [@jeanregisser](https://github.com/jeanregisser))
- Fix return value of `Linking.openURL()` ([4a5d0bd](https://github.com/facebook/react-native/commit/4a5d0bd) by [@thib92](https://github.com/thib92))
- When an accessibilityLabel can't be discerned, return `nil` instead of `@""` ([d4ff5ed](https://github.com/facebook/react-native/commit/d4ff5ed) by [@sammy-SC](https://github.com/sammy-SC))
- Fix Xcode build when the project's path contains whitespace ([f0770b6](https://github.com/facebook/react-native/commit/f0770b6))
- Move accessibility props to UIView+React ([9261035](https://github.com/facebook/react-native/commit/9261035) by [@janicduplessis](https://github.com/janicduplessis))
