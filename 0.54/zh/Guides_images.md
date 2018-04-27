---
id: images
title: 图像
---

## 静态图像资源

`React Native` 提供了一个统一的方式来管理iOS和Android应用中的图片。要往应用程序中添加一个静态图片，只需把图片文件放在RN工程文件夹中某处，然后像下面这样去引用它：

```javascript
<Image source={require('./my-icon.png')} />
```

图像名称的解析（查找）方式与解析JS模块的方式相同。 在上面的示例中，打包程序将在需要它的组件的相同文件夹中查找 my-icon.png。 此外，如果您有`my-icon.ios.png`和`my-icon.android.png`，则打包程序将为该平台选择正确的文件。

您还可以使用 `@2x` 和 `@3x` 后缀,来为不同的屏幕密度提供图像。 例如下列的文件结构：

```
.
├── button.js
└── img
    ├── check@2x.png
    └── check@3x.png
```

则在 `button.js` 里有这样的代码：

```javascript
<Image source={require('./img/check.png')} />
```

Packager会打包所有的图片资源并且依据屏幕精度提供对应的资源。譬如说，iPhone 7会使用 `check@2x.png` ，而在 iPhone 7 Plus上则会使用 `check@3x.png`。如果没有图片恰好满足屏幕分辨率，则会自动选中最接近的图片。

注：在windows操作系统下进行开发调试时，如果你添加了一个新的图像文件，那么可能需要重启 `packager` 。

这样带来的好处如下：

- 在 ios 与 android 上有着一致的文件管理系统。
- 图像资源与 `javascript`代码资源可放置于同一文件夹中，组件彼此之间保持独立。
- 无需占用全局命名空间，则完全不同担心图片名字冲突问题。
- 只有实际被用到（比如被require）的图像文件才会被编译打包至APP文件。
- 在开发中，增加或修改图片并不需要重新编译，只需要像修改js代码一样刷新你的模拟器即可。
- `packager`可以知道图像文件的具体尺寸，无需在代码中再次声明尺寸。
- 使用`npm`分发组件或库可以包含图像文件。

注：事实上，你必须明确require中图片的名字（译者注：不能使用变量代替，因为因为require是在编译时期执行，而非运行时期执行）

```javascript
// GOOD
<Image source={require('./my-icon.png')} />;

// BAD
var icon = this.props.active ? 'my-icon-active' : 'my-icon-inactive';
<Image source={require('./' + icon + '.png')} />;

// GOOD
var icon = this.props.active
  ? require('./my-icon-active.png')
  : require('./my-icon-inactive.png');
<Image source={icon} />;
```

请注意通过此种方式(require)引入的图像文件包含了尺寸信息(width,height),如果你需要其能够动态缩放大小（例如：Flex），则需要在它的style属性中手动设置`{ width: undefined, height: undefined }`。

## 静态非图像资源

`require` 语法在项目中亦可以用于静态加载音频、视频或者文档文件。在RN中，大多数的文件类型都支持，包括：`.mp3`, `.wav`, `.mp4`, `.mov`, `.html` 和 `.pdf`。浏览 [packager defaults](https://github.com/facebook/react-native/blob/master/local-cli/util/Config.js#L68) 查看完整列表。

您可以通过创建包配置文件来添加对其他文件类型的支持（请参阅[packager config file](https://github.com/facebook/metro/blob/master/packages/metro/src/defaults.js#L14-L44) 来获取完整的属性列表）。

需要注意的是视频必须指定尺寸（使用绝对定位）而不能使用 `flexGrow`，因为当前React-native并不能获取非图像资源的尺寸。 对于直接链接到Xcode或Android资源文件夹的视频，不会出现此限制。

## 使用 Hybrid App 的资源

如果你构建了一个混合APP程序(一部分UI使用`React-native`开发,而另一部分UI使用原生开发)，你依旧可以使用`packager`进行图像资源的打包。

对于使用 `xcode的asset类目` 或从 `安卓drawable目录` 中引入的图像资源，在使用时请不要带上后缀名：

```javascript
<Image source={{uri: 'app_icon'}} style={{width: 40, height: 40}} />
```

对于Android资源文件夹中的图片，请使用路径：`asset:/`：

```javascript
<Image source={{uri: 'asset:/app_icon.png'}} style={{width: 40, height: 40}} />
```

这些方法在最后编译时均**没有安全检查**，您必须保证您的图像资源在应用中能正常使用，同时，亦需要指定其具体尺寸。

## 网络图像

很多要在App中显示的图片并不能在编译的时候获得，又或者有时候需要动态载入来减少打包后的二进制文件的大小。这些时候，与静态资源不同的是，你必须要手动指定图片尺寸。同时我们强烈建议你使用`https`以满足 [App Transport Security](running-on-device.md#app-transport-security) 的要求。

```javascript
// GOOD
<Image source={{uri: 'https://facebook.github.io/react/logo-og.png'}}
       style={{width: 400, height: 400}} />

// BAD
<Image source={{uri: 'https://facebook.github.io/react/logo-og.png'}} />
```

### 请求网络图片

如果您想要将`HTTP-Verb`，`Headers`或`Body`与图像请求一起发出，可以通过在Image对象上定义这些属性来执行此操作：

```javascript
<Image
  source={{
    uri: 'https://facebook.github.io/react/logo-og.png',
    method: 'POST',
    headers: {
      Pragma: 'no-cache',
    },
    body: 'Your Body goes here',
  }}
  style={{width: 400, height: 400}}
/>
```

## Uri数据图像

通常您可能会从`REST API`调用中获取编码的图像数据。 您可以使用`'data'`uri方案来使用这些图像。与获取网络资源相同，您必须手动指定图像的尺寸

> 这种方式仅仅适用于非常小的动态图像，比如数据库列表中的图标。

```javascript
// include at least width and height!
<Image
  style={{
    width: 51,
    height: 51,
    resizeMode: Image.resizeMode.contain,
  }}
  source={{
    uri:
      'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADMAAAAzCAYAAAA6oTAqAAAAEXRFWHRTb2Z0d2FyZQBwbmdjcnVzaEB1SfMAAABQSURBVGje7dSxCQBACARB+2/ab8BEeQNhFi6WSYzYLYudDQYGBgYGBgYGBgYGBgYGBgZmcvDqYGBgmhivGQYGBgYGBgYGBgYGBgYGBgbmQw+P/eMrC5UTVAAAAABJRU5ErkJggg==',
  }}
/>
```

### 缓存控制 (iOS Only)

在某些情况下你可能仅仅想展示一张已经在本地缓存的图片，例如一个低分辨率的占位符，直到高分辨率的图片可用。在其他情况下你不关心图片是否是过时的，并愿意显示过时的图片，以节省带宽。缓存资源属性给你控制网络层与缓存交互的方式。

- `default`：使用原生平台默认策略。
- `reload`：URL的数据将从原始地址加载。不使用现有的缓存数据。
- `force-cache`：现有的缓存数据将用于满足请求，忽略其期限或到期日。如果缓存中没有对应请求的数据，则从原始地址加载。
- `only-if-cached`：现有的缓存数据将用于满足请求，忽略其期限或到期日。如果缓存中没有对应请求的数据，则不尝试从原始地址加载，并且认为请求是失败的。

```javascript
<Image
  source={{
    uri: 'https://facebook.github.io/react/logo-og.png',
    cache: 'only-if-cached',
  }}
  style={{width: 400, height: 400}}
/>
```

## 本地文件系统中的图片

有关如何使用在 `Images.xcassets` 以外的本地资源，请参考 [CameraRoll](cameraroll.md)。

### 最适合相册的图片

iOS会为同一张图片在相册中保存多个不同尺寸的副本。为了性能考虑，从这些副本中挑出最合适的尺寸显得尤为重要。对于一处 200x200 大小的缩略图，当然不应该选择最高质量的3264x2448大小的图片。如果恰好有匹配的尺寸，那么`React Native`会自动为你选择。如果没有，则会选择最接近的尺寸进行缩放，但也至少缩放到比所需尺寸大出50%，以使图片看起来仍然足够清晰。这一切过程都是自动完成的，所以你不用操心自己去完成这些繁琐（容易出错）的代码。

## 为什么不在所有情况下都自动指定尺寸呢?

**在浏览器中** 如果你不手动设定图片的大小，那么浏览器首先将渲染一个 0*0 大小的占位元素，在下载完图片后浏览器将基于正确的尺寸来呈现（渲染）图片。这样做的最大问题在于UI组件会由于图片加载完成后位置发生变化（跳动），严重影响了用户体验。

**在React Native中** 我们有意的规避了这种方式。可这种方式将导致开发人员需要付出更多的工作来提前知晓远程图像资源的尺寸，但我们相信此种方式将带来更好的用户体验。不过如果通过 `require('./my-icon.png')` 方法从打包好的应用资源文件中加载图片资源，则**无需指定尺寸**，因为React-Native会自动读取其尺寸。

如下所示，引用 `require('./my-icon.png')` 的实际输出结果是：

```javascript
{"__packager_asset":true,"uri":"my-icon.png","width":591,"height":573}
```

## 图像的属性（source）是一个对象

在 `React Native`之中，一个有趣的决定是将 `src`的属性命名为 `source`，并且不支持字符串。而是一个带有 `uri` 属性的对象。 

```javascript
<Image source={{uri: 'something.jpg'}} />
```

深层次的考虑是，这样可以使我们在对象中添加一些元数据`(metadata)`。假设你在使用`require('./my-icon.png')`，那么我们就会在其中添加真实文件路径以及尺寸等信息（这只是举个例子，未来的版本中require的具体行为可能会变化）。此外这也是考虑了未来的扩展性，比如我们可能会加入精灵图（sprites）的支持：在输出`{uri: ...}`的基础上，我们可以进一步输出裁切信息`{uri: ..., crop: {left: 10, top: 50, width: 20, height: 40}}`，这样理论上就可以在现有的代码中无缝支持精灵图的切分。

对于开发者来说，则可以在其中标注一些有用的属性，例如图片的尺寸，这样可以使图片自己去计算将要显示的尺寸（而不必在样式中写死）。请在这一数据结构中自由发挥，存储你可能需要的任何图片相关的信息。

## 背景图片的嵌套

熟悉网络的开发人员的一项常见功能请求是背景图像。 为了处理这种用例，可以使用 `<ImageBackground>` 组件，该组件具有与`<Image>`相同的`props`（属性），把需要背景图的子组件嵌入其中即可。

在某些情况下，您可能不想使用 `<ImageBackground>`，因为实现非常简单。 请参阅 `<ImageBackground>` 的 [源代码](https://github.com/facebook/react-native/blob/master/Libraries/Image/ImageBackground.js) 以获取更多信息，并在需要时创建您自己的自定义组件。

```javascript
return (
  <ImageBackground source={...}>
    <Text>Inside</Text>
  </ImageBackground>
);
```

## iOS边框圆角样式

请注意下列边框圆角样式目前在iOS的图片组件上还不支持：

* `borderTopLeftRadius`
* `borderTopRightRadius`
* `borderBottomLeftRadius`
* `borderBottomRightRadius`

## 异线程解码图片

图片解码有可能会需要超过一帧的时间。这是在`web`页上这是页面掉帧的一大因素，因为解码是在主线程中完成的。然而在`React Native`中，图片解码则是在另一线程中完成的。在实际开发中，一般对图片还没下载完成时的场景都做了处理（添加loading等），而图片解码时显示的占位符只占用几帧时间，并不需要你改动代码去额外处理。
