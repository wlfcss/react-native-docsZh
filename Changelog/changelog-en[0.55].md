## [0.55]

Welcome to the March 2018 release of React Native ! Over 81 contributors made 247 commits since February. Thanks for another exciting release.

Here are a few highlights:

- React Native is now using the MIT license
- Android TV device support

[![RNAndroidTVDemo](http://img.youtube.com/vi/EzIQErHhY20/0.jpg)](http://www.youtube.com/watch?v=EzIQErHhY20)

- Animated tracking with native driver - check out the [silky smooth framerate](https://t.co/dE1KST1i3g)
- Lots of Flow improvements
- Bugfixes

### Added: new features

- Added support for animated tracking to native driver. Now you can use `useNativeDriver` flag with animations that track other `Animated.Values` ([b48f7e5](https://github.com/facebook/react-native/commit/b48f7e5) by [@kmagiera](https://github.com/kmagiera))
- There's a new UTFSequence module in the library for common Unicode sequences (Emoji!) ([54870e0](https://github.com/facebook/react-native/commit/54870e0) and [4761d5a](https://github.com/facebook/react-native/commit/4761d5a) by [@sahrens](https://github.com/sahrens))
- Added `contextMenuHidden` property for **TextInput** ([2dd2529](https://github.com/facebook/react-native/commit/2dd2529) by [@amhinson](https://github.com/amhinson))
- Add `testOnly_pressed` to **TouchableHighlight** for snapshot tests ([3756d41](https://github.com/facebook/react-native/commit/3756d41) by [@sahrens](https://github.com/sahrens))

#### Android specific additions

- Added support for Android TV devices ([b7bb2e5](https://github.com/facebook/react-native/commit/b7bb2e5) by [@krzysztofciombor](https://github.com/krzysztofciombor))
- Implemented style `letterSpacing` for **Text** and **TextInput** ([5898817](https://github.com/facebook/react-native/commit/5898817) by [@motiz88](https://github.com/motiz88))
- Bundle download progress is now shown [d06e143](https://github.com/facebook/react-native/commit/d06e143) by [@janicduplessis](https://github.com/janicduplessis))
- **AndroidInfoModule** now also returns Android ID ([216c8ec](https://github.com/facebook/react-native/commit/216c8ec) by [@L33tcodex0r](https://github.com/L33tcodex0r))

#### iOS specific additions

- Introducing **InputAccessoryView**, "a component which enables customization of the keyboard input accessory view" ([38197c8](https://github.com/facebook/react-native/commit/38197c8), [84ef7bc](https://github.com/facebook/react-native/commit/84ef7bc), and [6d9fe45](https://github.com/facebook/react-native/commit/6d9fe45) by [@PeteTheHeat](https://github.com/PeteTheHeat))
- `base-line` metric exposure for **Text** and **TextInput** ([51b3529](https://github.com/facebook/react-native/commit/51b3529), [0dbe183](https://github.com/facebook/react-native/commit/0dbe183), and [7630a61](https://github.com/facebook/react-native/commit/7630a61) by [@shergin](https://github.com/shergin))
- **DatePickerIOS** now has `initialDate` prop ([446ce49](https://github.com/facebook/react-native/commit/446ce49))
- Expose version via `RCTVersion.h`'s `RCTGetReactNativeVersion()` ([30469ed](https://github.com/facebook/react-native/commit/30469ed) by [@LeoNatan](https://github.com/LeoNatan))
- Allow running multiple simulators simultaneously with `react-native run-ios --simulator ...` ([2ad3407](https://github.com/facebook/react-native/commit/2ad3407) by [@koenpunt](https://github.com/koenpunt))
- Introduced **RCTSurfaceHostingProxyRootView** for migration to **RCTSurfaceHostingView** ([34b8876](https://github.com/facebook/react-native/commit/34b8876) by [@fkgozali](https://github.com/fkgozali))
- New UIManager API allowing intercept/delay mounting process ([402ae2f](https://github.com/facebook/react-native/commit/402ae2f) and [b90c1cf](https://github.com/facebook/react-native/commit/b90c1cf) by [@shergin](https://github.com/shergin))

### Changes: existing functionality that is now different

- React Native has now adopted the MIT license ([1490ab1](https://github.com/facebook/react-native/commit/1490ab1) and [26684cf](https://github.com/facebook/react-native/commit/26684cf) by [@sophiebits](https://github.com/sophiebits))
- The HelloWorld template now exclude `*.jsbundle` files from Git ([2123108](https://github.com/facebook/react-native/commit/2123108) by [@aneophyte](https://github.com/aneophyte))
- `react-native-git-upgrade` now shows files merged with conflicts in red ([e53a8f7](https://github.com/facebook/react-native/commit/e53a8f7) by [@alvinthen](https://github.com/alvinthen))
- `ResolvedAssetSource` type to have all read-only members ([4d0ee37](https://github.com/facebook/react-native/commit/4d0ee37) by [@sahrens](https://github.com/sahrens))
- Flow types improvements ([b6c7e55](https://github.com/facebook/react-native/commit/b6c7e55), [b98bf1e](https://github.com/facebook/react-native/commit/b98bf1e), [80c1839](https://github.com/facebook/react-native/commit/80c1839), [70a3ece](https://github.com/facebook/react-native/commit/70a3ece), [f734357](https://github.com/facebook/react-native/commit/f734357), [a817c64](https://github.com/facebook/react-native/commit/a817c64), [3fd82d3](https://github.com/facebook/react-native/commit/3fd82d3), [cd8128b](https://github.com/facebook/react-native/commit/cd8128b), [5035af8](https://github.com/facebook/react-native/commit/5035af8), [26734a8](https://github.com/facebook/react-native/commit/26734a8), [321ba06](https://github.com/facebook/react-native/commit/321ba06), [b6b80f6](https://github.com/facebook/react-native/commit/b6b80f6), [f1316ca](https://github.com/facebook/react-native/commit/f1316ca), [2520c64](https://github.com/facebook/react-native/commit/2520c64), [214da52](https://github.com/facebook/react-native/commit/214da52), [dbdf43b](https://github.com/facebook/react-native/commit/dbdf43b), [49396aa](https://github.com/facebook/react-native/commit/49396aa), [4895c64](https://github.com/facebook/react-native/commit/4895c64), [a3c07c9](https://github.com/facebook/react-native/commit/a3c07c9), [49ffc9f](https://github.com/facebook/react-native/commit/49ffc9f), and [c129457](https://github.com/facebook/react-native/commit/c129457) by [@TheSavior](https://github.com/TheSavior), [@yungsters](https://github.com/yungsters), and [@alex288ms](https://github.com/alex288ms))
- Better enable cross-platform support of WebSocket.js ([b9be289](https://github.com/facebook/react-native/commit/b9be289) by [@rozele](https://github.com/rozele))
- Better error handling in the CLI around making directories ([d2817f4](https://github.com/facebook/react-native/commit/d2817f4) by [@BridgeAR](https://github.com/BridgeAR))
- Verify that the component passed to createAnimatedComponent is not functional ([10b642a](https://github.com/facebook/react-native/commit/10b642a) by [@janicduplessis](https://github.com/janicduplessis))
- Don't truncate in the middle of an emoji ([9c8c597](https://github.com/facebook/react-native/commit/9c8c597) by [@Vince0613](https://github.com/Vince0613))
- Loosen Platform check to allow better code sharing for out-of-tree platforms ([84affbd](https://github.com/facebook/react-native/commit/84affbd))
- In CLI, fix issue with `isInstalled` check for Android and references to unregister ([ec88489](https://github.com/facebook/react-native/commit/ec88489) by [@rozele](https://github.com/rozele))

#### iOS specific changes

- tvOS `onPress` magnification animation now works via the `tvParallaxProperties` prop object taking `pressMagnification`, `pressDuration`, and `pressDelay` ([6c353fd](https://github.com/facebook/react-native/commit/6c353fd) by [@JulienKode](https://github.com/JulienKode))

### Fixed: bugs that have been resolved

- In **TouchableOpacity**, trigger animation on `opacity` upon change in `disabled` prop ([9366ce4](https://github.com/facebook/react-native/commit/9366ce4) by [@maxkomarychev](https://github.com/maxkomarychev))
- Fixed an issue encountered when using `react-native-vector-icons` ([a759a44](https://github.com/facebook/react-native/commit/a759a44) and [54dc11a](https://github.com/facebook/react-native/commit/54dc11a) by [@jeanlauliac](https://github.com/jeanlauliac) and [@t4deu](https://github.com/t4deu)))
- Add missing mock for Jest for `removeEventListener` method ([59c7b2c](https://github.com/facebook/react-native/commit/59c7b2c) by [@MoOx](https://github.com/MoOx))
- Fix main size calculation from the aspect ratio ([f751c34](https://github.com/facebook/react-native/commit/f751c34))
- Fix crash in Subscribable due to uglify-es ([b57a78c](https://github.com/facebook/react-native/commit/b57a78c) by [@iMagdy](https://github.com/iMagdy))
- Update `node-notifier` dependency to fix memory leak ([860fcd4](https://github.com/facebook/react-native/commit/860fcd4) by [@rickhanlonii](https://github.com/rickhanlonii))
- Fix issues with pollParams and link ([ca8ce83](https://github.com/facebook/react-native/commit/ca8ce83) by [@grabbou](https://github.com/grabbou))

#### iOS specific fixes

- DevLoadingView now supports the iPhone X screen shape ([47b36d3](https://github.com/facebook/react-native/commit/47b36d3) by [@mrtnrst](https://github.com/mrtnrst))
- Added bounds check to prevent ScrollView from scrolling to an offset which is out of bounds of the ScrollView ([16c9e5b](https://github.com/facebook/react-native/commit/16c9e5b) by [@siddhantsoni](https://github.com/siddhantsoni))
- **NetInfo** `isConnected` works again ([dbafc29](https://github.com/facebook/react-native/commit/dbafc29) by [@alburdette619](https://github.com/alburdette619))
- In **AlertIOS**, fix duplicate var name declaration ([6893a26](https://github.com/facebook/react-native/commit/6893a26))
- Permit `react-native run-ios --device [id]` by passing port when running on device ([f8fee0a](https://github.com/facebook/react-native/commit/f8fee0a) by [@jozan](https://github.com/jozan))
- Fixed issue with `run-ios` where `Entry, ":CFBundleIdentifier", Does Not Exist` was being received ([5447ca6](https://github.com/facebook/react-native/commit/5447ca6) by [@blackneck](https://github.com/blackneck))
- Fixed problem in Text measurement on iOS ([a534672](https://github.com/facebook/react-native/commit/a534672) by [@shergin](https://github.com/shergin))
- Fix crash when reloading in tvOS ([3a3d884](https://github.com/facebook/react-native/commit/3a3d884) by [@dlowder-salesforce](https://github.com/dlowder-salesforce))
- Fixed a bug with positioning of nested views inside **Text** ([7d20de4](https://github.com/facebook/react-native/commit/7d20de4) by [@shergin](https://github.com/shergin))
- Fix blob response parsing for empty body ([093a78d](https://github.com/facebook/react-native/commit/093a78d) by [@janicduplessis](https://github.com/janicduplessis))
- Fix tvOS react-native init release build ([3002c4e](https://github.com/facebook/react-native/commit/3002c4e) by [@dlowder-salesforce](https://github.com/dlowder-salesforce)
- Fix RedBox from bridge reload due is not re-registering its root view ([2e51fa5](https://github.com/facebook/react-native/commit/2e51fa5) by [@fkgozali](https://github.com/fkgozali))

#### Android specific fixes

- Fix: incorrect line-height calculation ([74e54cb](https://github.com/facebook/react-native/commit/74e54cb) by [@strindhaug](https://github.com/strindhaug))
- Fix crashes with TextInput introduced in 0.53 ([b60a727](https://github.com/facebook/react-native/commit/b60a727) by [@joshyhargreaves](https://github.com/joshyhargreaves))
- Update ReactAndroid build script to support gradle 2.3.0 ([d8bb990](https://github.com/facebook/react-native/commit/d8bb990))
- Allow "unexpected URL" exception to be caught on Android when using fetch ([da84eba](https://github.com/facebook/react-native/commit/da84eba) by [@jcurtis](https://github.com/jcurtis))
- Fix `onLayout` prop for **TextInput** ([8a073c1](https://github.com/facebook/react-native/commit/8a073c1) by [@rozele](https://github.com/rozele))
- Fix ViewPager when using native navigation ([a1295e1](https://github.com/facebook/react-native/commit/a1295e1) by [@ruiaraujo](https://github.com/ruiaraujo))
- Fix localization crash in **DevSettingsActivity** ([427e464](https://github.com/facebook/react-native/commit/427e464) by [@ayc1](https://github.com/ayc1))
- Fix pinch crash in touch-responsive views ([67c3ad4](https://github.com/facebook/react-native/commit/67c3ad4) by [@tobycox](https://github.com/tobycox))
- Fix IllegalStateException thrown in looped timing native animation ([ef9d1fb](https://github.com/facebook/react-native/commit/ef9d1fb) by [@kmagiera](https://github.com/kmagiera))
- Workaround android-only js module resolution issue ([c20e0f9](https://github.com/facebook/react-native/commit/c20e0f9) by [@fkgozali](https://github.com/fkgozali))
- Fix ReadableNativeMap.toHashMap() for nested maps and arrays ([8a6ab14](https://github.com/facebook/react-native/commit/8a6ab14) by [@esamelson](https://github.com/esamelson))
- Fix Android Sanity Buck version check ([e057322](https://github.com/facebook/react-native/commit/e057322) by [@hramos](https://github.com/hramos))
- Fixes the connection to Firestore by following whatwg.org's XMLHttpRequest send() method ([d52569c](https://github.com/facebook/react-native/commit/d52569c) by [@samsafay](https://github.com/samsafay))
- `invertStickyHeaders` can now be set from **SectionList** or **FlatList** ([3d69b5c](https://github.com/facebook/react-native/commit/3d69b5c) by [@dannycochran](https://github.com/dannycochran))

### Removed: features that have been removed; these are breaking

- Removed various types ([b58e377](https://github.com/facebook/react-native/commit/b58e377), [ee26d9b](https://github.com/facebook/react-native/commit/ee26d9b), [d89517d](https://github.com/facebook/react-native/commit/d89517d), [852084a](https://github.com/facebook/react-native/commit/852084a) by [@TheSavior](https://github.com/TheSavior))
- Deleted `Systrace.swizzleJSON()` ([3e141cb](https://github.com/facebook/react-native/commit/3e141cb) by [@yungsters](https://github.com/yungsters))

#### Android specific removals

- `ReactInstanceManager#registerAdditionalPackages` has been removed; Create UIManager interface and extract common classes in uimanager/common ([6b45fb2](https://github.com/facebook/react-native/commit/6b45fb2) by [@mdvacca](https://github.com/mdvacca))

#### iOS specific removals

- Remove callFunctionSync experimental APIs ([19a4a7d](https://github.com/facebook/react-native/commit/19a4a7d) by [@danzimm](https://github.com/danzimm))