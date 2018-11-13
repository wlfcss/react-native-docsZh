## [0.57]

Welcome to the 0.57 release of React Native! This release addresses a number of issues and has some exciting improvements. We again skipped a monthly release, focused on quality by extending the release candidate phase, and let some upstream packages reach stable for inclusion.

This release includes [599 commits by 73 different contributors](https://github.com/facebook/react-native/compare/0.56-stable...0.57-stable)! In response to feedback, we've prepared a changelog that contains only user-impacting changes. Please share your input and let us know how we can make this even more useful, and as always [let us know](https://github.com/react-native-community/react-native-releases/issues/34) if you have any feedback on this process.

### Highlights

#### New features

- Accessibility APIs now support accessibility hints, inverted colors, and easier usage of defining the element's role and states; read more at [@ziqichen6's excellent blog post](https://facebook.github.io/react-native/blog/2018/08/13/react-native-accessibility-updates)
- On iOS, `WKWebView` can now be used within the `WebView` component; read more at [@rsnara's awesome blog post](https://facebook.github.io/react-native/blog/2018/08/27/wkwebview)
- Better support for out-of-tree platforms. For details, please refer to [the discussion](https://github.com/react-native-community/discussions-and-proposals/issues/21) that the community used to get this up and running (there will be a new page in the docs dedicated to it too) - huge props to @empyrical for working on this!

#### Tooling updates

- Android tooling has been updated to match newer configuration requirements (SDK 27, gradle 4.4, and support library 27); building with Android plugin 3.2 doesn't work due to the gradle scripts, so **please** stay on Android Studio 3.1 for now
- Support Babel 7 stable landed! Be sure to read [here](https://blogs.msdn.microsoft.com/typescript/2018/08/27/typescript-and-babel-7/) about using TypeScript and check out the [Babel 7 migration guide](https://babeljs.io/docs/en/next/v7-migration) for help migrating.
- Metro has been upgraded (with Babel 7 and better transformer support), and in the next major release we plan on having two new features (ram bundles and inline requires) optional for you all to use - you can read how it will happen [here](https://github.com/react-native-community/discussions-and-proposals/blob/master/core-meetings/2018-09-metro-meeting.md); moreover, if you have a custom packager config, we recommend you read also the "updating to this version" section.
- Flow, React, and related packages have also been updated; this includes [working support](https://github.com/facebook/react-native/commit/cf5f3e97eb68c5bcf1d9f27261795d0221e27be4) for the [React Profiler](https://reactjs.org/blog/2018/09/10/introducing-the-react-profiler.html).

#### The Slimmening is happening

As mentioned a few times in the past, the core team is reviewing the repository to trim it to the base React Native features in order to make the whole ecosystem more maintainable (by using a *divide-et-impera* approach, the community will move faster and enable pull requests to be reviewed and merged quicker). This change requires extracting some components into their own separate repos and removing old, unused code ([details here](https://github.com/react-native-community/discussions-and-proposals/issues/6)).

0.57 is **not** directly affected by any changes, but we want you to know that:

- `WebView` will be moved to its own repo at [react-native-community/react-native-webview](https://github.com/react-native-community/react-native-webview). There is already a base implementation there. Help us out by giving that a try, and expect that `WebView` will be deprecated soon
- `NavigatorIOS` will be **fully** removed from the main codebase starting 0.58.0 (via [this commit](https://github.com/facebook/react-native/commit/0df92afc1caf96100013935d50bdde359b688658)); it is now deprecated

### Updating to this version

1. Upgrade the version of React Native in the `package.json` from `0.56.0` to `0.57.0`, and the React version to `16.5`
2. Change the babel-preset dependency from `"babel-preset-react-native": "^5",` to `"metro-react-native-babel-preset": "^0.45.0",`, then change the `.babelrc` configuration to:

   ```JSON
     {
       "presets": ["module:metro-react-native-babel-preset"]
     }
   ```

3. Ensure that you have all the babel dependencies to version `^7.0.0` (you may also need to add `"babel-core": "7.0.0-bridge.0"` as a yarn resolution to ensure retro-compatibility)
4. If you have a custom packager configuration via `rn-cli.config.js`, you probably need to update it to work with the updated Metro configuration structure (for full detail refer to Metro's [documentation](https://facebook.github.io/metro/docs/en/configuration)); here are some commonly encountered changes to `rn-cli.config.js`:

   ```diff
   -const blacklist = require('metro/src/blacklist')
   +const blacklist = require('metro-config/src/defaults/blacklist')

   // ...

   module.exports = {
   +  watchFolders: alternateRoots,
   +  resolver: {
   +    blacklistRE: blacklist
   +  },
   +  transformer: {
   +    babelTransformerPath: require.resolve('./scripts/transformer.js'),
   +  },
   -  getProjectRoots() {
   -    return [
   -      path.resolve(__dirname),
   -    ].concat(alternateRoots)
   -  },
   -  getBlacklistRE() {
   -    return blacklist;
   -  },
   -  transformModulePath: require.resolve('./scripts/transformer.js'),
   }
   ```

5. Run `yarn` to ensure that all the new dependencies have been installed

### Added: new features

- Add .nvmrc and ensure node version required is compatible with ESLint 5 ([30b9d81](https://github.com/facebook/react-native/commit/30b9d81) by [@slorber](https://github.com/slorber))
- Major improvements to accessibility features ([9f01e4c](https://github.com/facebook/react-native/commit/9f01e4c), [b5b704d](https://github.com/facebook/react-native/commit/b5b704d), [c36e8b3](https://github.com/facebook/react-native/commit/c36e8b3), [40f6998](https://github.com/facebook/react-native/commit/40f6998), [c1d0ccd](https://github.com/facebook/react-native/commit/c1d0ccd), [679bff2](https://github.com/facebook/react-native/commit/679bff2), [10b603f](https://github.com/facebook/react-native/commit/10b603f), [d9eeae9](https://github.com/facebook/react-native/commit/d9eeae9), [3cfa7ae](https://github.com/facebook/react-native/commit/3cfa7ae), [5acb721](https://github.com/facebook/react-native/commit/5acb721), [5741f77](https://github.com/facebook/react-native/commit/5741f77), [d0b86ec](https://github.com/facebook/react-native/commit/d0b86ec), [e739143](https://github.com/facebook/react-native/commit/e739143), [c27b495](https://github.com/facebook/react-native/commit/c27b495), [5aa040d](https://github.com/facebook/react-native/commit/5aa040d), [03036f7](https://github.com/facebook/react-native/commit/03036f7), [3bedc78](https://github.com/facebook/react-native/commit/3bedc78), [ca01290](https://github.com/facebook/react-native/commit/ca01290), [121e2e5](https://github.com/facebook/react-native/commit/121e2e5), [1bc5226](https://github.com/facebook/react-native/commit/1bc5226), [48b3d13](https://github.com/facebook/react-native/commit/48b3d13), [ef3d8b2](https://github.com/facebook/react-native/commit/ef3d8b2), [5f8b44f](https://github.com/facebook/react-native/commit/5f8b44f), [50e4001](https://github.com/facebook/react-native/commit/50e4001), and [f39d092](https://github.com/facebook/react-native/commit/f39d092) by [@ziqichen6](https://github.com/ziqichen6))
- Add `YogaNodeProperties` implementation based on `ByteBuffer` ([0c97e75](https://github.com/facebook/react-native/commit/0c97e75) and [23657cc](https://github.com/facebook/react-native/commit/23657cc) by [@davidaurelio](https://github.com/davidaurelio))
- Add `FlatList` and `SectionList` to Animated exports ([daa7c78](https://github.com/facebook/react-native/commit/daa7c78) by [@yunyu](https://github.com/yunyu))
- Adding new styling props to `FlatList`/`VirtualizedList` for `ListHeaderComponent` and `ListFooterComponent` ([a2675ce](https://github.com/facebook/react-native/commit/a2675ce))
- Added more info to Module Registry systraces ([c7fdd27](https://github.com/facebook/react-native/commit/c7fdd27) by [@axe-fb](https://github.com/axe-fb))
- Added support for out-of-tree platform plugins via a new `haste` field in `package.json`; read more in the [docs entry](https://facebook.github.io/react-native/docs/out-of-tree-platforms) ([6bcd51a](https://github.com/facebook/react-native/commit/6bcd51a) by [@empyrical](https://github.com/empyrical))
- Added `snapToOffsets` to `ScrollView` and made a number of fixes to `snapToInterval` as well ([ef7e99c](https://github.com/facebook/react-native/commit/ef7e99c) by [@olegbl](https://github.com/olegbl))

#### Android specific additions

- Allow registering custom packager command handlers ([b3ef1c3](https://github.com/facebook/react-native/commit/b3ef1c3) by [@fkgozali](https://github.com/fkgozali))
- Implement `AccessibilityInfo.setAccessibilityFocus` for Android ([be715ec](https://github.com/facebook/react-native/commit/be715ec) by [@draperunner](https://github.com/draperunner))
- Add Support for `overflow` style property ([b81c8b5](https://github.com/facebook/react-native/commit/b81c8b5) and [bbdc12e](https://github.com/facebook/react-native/commit/bbdc12e)by [@yungsters](https://github.com/yungsters))

#### iOS specific additions

- `WebView` can now use `WKWebView` internally if you pass `useWebKit={true}` ([e90d9ca](https://github.com/facebook/react-native/commit/e90d9ca), [9b3a6ec](https://github.com/facebook/react-native/commit/9b3a6ec), [f7f9d01](https://github.com/facebook/react-native/commit/f7f9d01), [94560ca](https://github.com/facebook/react-native/commit/94560ca), [06cce04](https://github.com/facebook/react-native/commit/06cce04), [1c3af59](https://github.com/facebook/react-native/commit/1c3af59), [5662598](https://github.com/facebook/react-native/commit/5662598), [1984f4b](https://github.com/facebook/react-native/commit/1984f4b), [1b73e76](https://github.com/facebook/react-native/commit/1b73e76), [d0b5a38](https://github.com/facebook/react-native/commit/d0b5a38), [0fa5bd8](https://github.com/facebook/react-native/commit/0fa5bd8), [527792a](https://github.com/facebook/react-native/commit/527792a), [ee971a7](https://github.com/facebook/react-native/commit/ee971a7), [d29c253](https://github.com/facebook/react-native/commit/d29c253), [0009d09](https://github.com/facebook/react-native/commit/0009d09), [078799f](https://github.com/facebook/react-native/commit/078799f), [f46dbc2](https://github.com/facebook/react-native/commit/f46dbc2), [262d286](https://github.com/facebook/react-native/commit/262d286), [959aacf](https://github.com/facebook/react-native/commit/959aacf), and [e0df3a1](https://github.com/facebook/react-native/commit/e0df3a1) by [@rsnara](https://github.com/rsnara))
- Add `accessibilityHint` for iOS ([253b29d](https://github.com/facebook/react-native/commit/253b29d) by [@draperunner](https://github.com/draperunner))

### Changes: existing functionality that is now different

- *[BREAKING]* In the CLI, `unbundle` is now `ram-bundle` ([ebf5aea](https://github.com/facebook/react-native/commit/ebf5aea) by [@jeanlauliac](https://github.com/jeanlauliac))
- Bump minimum Node version to 8.3 (#20236) ([e64e13f](https://github.com/facebook/react-native/commit/e64e13f) by [@hramos](https://github.com/hramos))
- Updated React ([70913a4](https://github.com/facebook/react-native/commit/70913a4), [b7bb25f](https://github.com/facebook/react-native/commit/b7bb25f), and [0b30129](https://github.com/facebook/react-native/commit/0b30129) by [@acdlite](https://github.com/acdlite), [@hramos](https://github.com/hramos), and [@yungsters](https://github.com/yungsters))
- Upgrade Flow to v0.76.0 ([eac34e3](https://github.com/facebook/react-native/commit/eac34e3) by [@gabelevi](https://github.com/gabelevi))
- Upgrade jest to 23.4.1 ([51cf9eb](https://github.com/facebook/react-native/commit/51cf9eb) by [@rafeca](https://github.com/rafeca))
- Upgrade babel-eslint to v9.0.0-beta.2 with better support for Flow ([abf1188](https://github.com/facebook/react-native/commit/abf1188) by [@rubennorte](https://github.com/rubennorte))
- Upgrade ESLint to 5.1.0 ([0f2f0ca](https://github.com/facebook/react-native/commit/0f2f0ca) by [@rubennorte](https://github.com/rubennorte))
- Upgrade Babel to v7.0.0 ([b9d1c83](https://github.com/facebook/react-native/commit/b9d1c83), [724c749](https://github.com/facebook/react-native/commit/724c749) by Peter van der Zee, and [9f83fcc](https://github.com/facebook/react-native/commit/9f83fcc) by [@rubennorte](https://github.com/rubennorte) and [@rafeca](https://github.com/rafeca))
- Metro is now at v0.45.0 ([169d683](https://github.com/facebook/react-native/commit/169d683), [bda84a3](https://github.com/facebook/react-native/commit/bda84a3), [5288656](https://github.com/facebook/react-native/commit/5288656), [1bfa422](https://github.com/facebook/react-native/commit/1bfa422), [96939ad](https://github.com/facebook/react-native/commit/96939ad) by [@CompuIves](https://github.com/CompuIves) and [@rafeca](https://github.com/rafeca))
- Hide pre-bundled notification when not on dev mode ([edf7100](https://github.com/facebook/react-native/commit/edf7100) by [@yancouto](https://github.com/yancouto))
- Refined `StyleSheet.compose` Flow Type ([50a481d](https://github.com/facebook/react-native/commit/50a481d) by [@yungsters](https://github.com/yungsters))
- Catch JS bundle load failure and prevent calls to JS after that ([201ba8c](https://github.com/facebook/react-native/commit/201ba8c) by [@fkgozali](https://github.com/fkgozali))
- Use new Metro configuration in react-native cli ([a32620d](https://github.com/facebook/react-native/commit/a32620d) and [aaf797a](https://github.com/facebook/react-native/commit/aaf797a) by [@CompuIves](https://github.com/CompuIves))
- Whitelist `react-native-dom` in haste/cli config defaults ([c4bcca6](https://github.com/facebook/react-native/commit/c4bcca6) by [@vincentriemer](https://github.com/vincentriemer))
- In the CLI, don't override `metro.config.js` settings ([3afe711](https://github.com/facebook/react-native/commit/3afe711) by [@rozele](https://github.com/rozele))

#### Android specific changes

- `Image` source without a uri now returns null ([28c7ccf](https://github.com/facebook/react-native/commit/28c7ccf) by [@himabindugadupudi](https://github.com/himabindugadupudi))
- `targetSdkVersion` is 26 ([bfb68c0](https://github.com/facebook/react-native/commit/bfb68c0) by [@dulmandakh](https://github.com/dulmandakh))
- Upgrade NDK to r17b ([6117a6c](https://github.com/facebook/react-native/commit/6117a6c) by [@dulmandakh](https://github.com/dulmandakh))
- Upgrade NDK toolchain to 4.9 ([ccdd450](https://github.com/facebook/react-native/commit/ccdd450) by [@dulmandakh](https://github.com/dulmandakh))
- Upgrade Android Support Library to version 27.1.1 and set compileSdkVersion to 27; buildToolsVersion comes along for the ride, too ([d9868f7](https://github.com/facebook/react-native/commit/d9868f7) and [5992f8d](https://github.com/facebook/react-native/commit/5992f8d) by [@dulmandakh](https://github.com/dulmandakh))
- Upgrade Android gradle plugin to 3.1.4, Gradle wrapper to 4.4 ([6eac2d4](https://github.com/facebook/react-native/commit/6eac2d4) and [33d20da](https://github.com/facebook/react-native/commit/33d20da) by [@gengjiawen](https://github.com/gengjiawen) and [@dulmandakh](https://github.com/dulmandakh))
- Upgrade to soloader 0.5.1 ([b6f2aad](https://github.com/facebook/react-native/commit/b6f2aad) by [@gengjiawen](https://github.com/gengjiawen))
- Upgrade mockito to 2.19.1 ([3ea803a](https://github.com/facebook/react-native/commit/3ea803a) by [@dulmandakh](https://github.com/dulmandakh))
- Upgrade glog to 0.3.5 ([b5fca80](https://github.com/facebook/react-native/commit/b5fca80) by [@dulmandakh](https://github.com/dulmandakh))

### Fixed: bugs that have been resolved

- Fixed builds on Windows machines ([3ac86c3](https://github.com/facebook/react-native/commit/3ac86c3) by [@rafeca](https://github.com/rafeca))
- Fixed building tvOS ([1f1ddd0](https://github.com/facebook/react-native/commit/1f1ddd0))
- Fixed `TextInputState`'s `currentlyFocusedField()` ([b4b594c](https://github.com/facebook/react-native/commit/b4b594c) by [@janicduplessis](https://github.com/janicduplessis))
- `<VirtualizedList>` fix for jumpy content when `initialScrollIndex` specified ([e0c7363](https://github.com/facebook/react-native/commit/e0c7363) by [@rbrosboel](https://github.com/rbrosboel))
- Fix local-cli assetRegistryPath and middlewares ([f05943d](https://github.com/facebook/react-native/commit/f05943d) by [@janicduplessis](https://github.com/janicduplessis))
- Fix issue with when all are `flexGrow` and `flexShrink` set to 0 except for one ([90a408e](https://github.com/facebook/react-native/commit/90a408e) by [@priteshrnandgaonkar](https://github.com/priteshrnandgaonkar))
- Fix react-native CLI's debugger UI path and metro host/port arg usage ([5067540](https://github.com/facebook/react-native/commit/5067540) by [@Kureev](https://github.com/Kureev))
- Hotfix to include `react-native-windows` in hasteImpl accepted paths ([5494274](https://github.com/facebook/react-native/commit/5494274) by [@rubennorte](https://github.com/rubennorte))
- Fix some classes of incorrect Flow errors for `Animated` ([db2159d](https://github.com/facebook/react-native/commit/db2159d) by [@yunyu](https://github.com/yunyu))
- Fixed a typo in DockerTests.md ([c1831d5](https://github.com/facebook/react-native/commit/c1831d5) by [@kant](https://github.com/kant))
- Fix invalid use of destructuring in jest preprocessor ([9d5bd50](https://github.com/facebook/react-native/commit/9d5bd50) by [@umairda](https://github.com/umairda))
- Fixed a CLI crash when using old versions of node ([9a4c21f](https://github.com/facebook/react-native/commit/9a4c21f) by [@keksipurkki](https://github.com/keksipurkki))

#### Android specific fixes

- Fix issue with AsyncStorage not behaving properly on Android 7+ ([1b09bd7](https://github.com/facebook/react-native/commit/1b09bd7))
- Fixed extreme `<TextInput>` slowness ([5017b86](https://github.com/facebook/react-native/commit/5017b86) by [@gnprice](https://github.com/gnprice))
- Fixed `<TextInput>` placeholder not being completely visible ([8402232](https://github.com/facebook/react-native/commit/8402232) and [86f24cc](https://github.com/facebook/react-native/commit/86f24cc) by [@jainkuniya](https://github.com/jainkuniya))
- Fix Horizontal `<ScrollView>`'s scroll position during layout changes with RTL content ([de57327](https://github.com/facebook/react-native/commit/de57327))
- Fix Horizontal `<ScrollView>` overflow issue ([d5465a9](https://github.com/facebook/react-native/commit/d5465a9))
- Fixing crash on SDK 15 on ReactTextInputLocalData ([1bb2bea](https://github.com/facebook/react-native/commit/1bb2bea))
- Fix Drawing Rect for ReactScrollView ([6a16bec](https://github.com/facebook/react-native/commit/6a16bec) by [@yungsters](https://github.com/yungsters))
- Fixed NoSuchKeyException Thrown From ReadableNativeMap bysafely unwrapping ReadableMap by defaulting to 0 if key not present ([1a6666a](https://github.com/facebook/react-native/commit/1a6666a) by [@Bhavik-P](https://github.com/Bhavik-P))
- Fixed runAndroid to enable the use of a package on port <> 8081 for Windows ([3cd0737](https://github.com/facebook/react-native/commit/3cd0737) by [@ihenshaw](https://github.com/ihenshaw))
- Don't crash on upload retry when trying to fetch on a varying quality network ([7a246e4](https://github.com/facebook/react-native/commit/7a246e4) by [@dryganets](https://github.com/dryganets))

#### iOS specific fixes

- Fix `TextInput.clear()` and `TextInput.setNativeProps({text: ''})` to work ([057d3ef](https://github.com/facebook/react-native/commit/057d3ef) by [@magicien](https://github.com/magicien))
- Correct fishhook import in RCTReconnectingWebSocket ([75a0273](https://github.com/facebook/react-native/commit/75a0273))
- Change in RCTImagePickerManager to handle crashes if height/width is nil ([82af7c9](https://github.com/facebook/react-native/commit/82af7c9) by [@abhi06276](https://github.com/abhi06276))
- Fix controlled `<TextInput>` on iOS when inputting in Chinese/Japanese ([892212b](https://github.com/facebook/react-native/commit/892212b) by [@mmmulani](https://github.com/mmmulani))
- Fixed `<ScrollView>` bug encountered with brownfield apps ([fab5fff](https://github.com/facebook/react-native/commit/fab5fff) by [@PeteTheHeat](https://github.com/PeteTheHeat))
- Fixed missing selection indicator lines on `<PickerIOS>` ([e592d6f](https://github.com/facebook/react-native/commit/e592d6f) by [@VSchlattinger](https://github.com/VSchlattinger))
- Fix crash in RCTImagePicker on iOS ([934c50f](https://github.com/facebook/react-native/commit/934c50f) by [@mmmulani](https://github.com/mmmulani))
- Fix `undefined_arch` error received when building in Xcode 10 beta ([e131fff](https://github.com/facebook/react-native/commit/e131fff) by [@futuun](https://github.com/futuun))
- Add support for connecting to the Packager when running the iOS app on device when using custom Debug configuration ([079bf3f](https://github.com/facebook/react-native/commit/079bf3f))
- Fixed RCTAnimation import for integrating with cocoapods ([7525f38](https://github.com/facebook/react-native/commit/7525f38) by [@LukeDurrant](https://github.com/LukeDurrant))

### Removed: features that have been removed; these are breaking

- *[BREAKING]* Removed `ScrollView.propTypes`; use flow or typescript for verifying correct prop usage instead ([5b6ff01](https://github.com/facebook/react-native/commit/5b6ff01) by [@sahrens](https://github.com/sahrens))

#### Android specific removals

- `ReactInstancePackage` is now deprecated; use `@link ReactPackage` or `@link LazyReactPackage` ([b938cd5](https://github.com/facebook/react-native/commit/b938cd5) by [@axe-fb](https://github.com/axe-fb))
