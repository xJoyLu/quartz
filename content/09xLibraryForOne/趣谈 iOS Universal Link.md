作者：iHTCboy

> 本文对 iOS Universal Link（通用链接）的浅入浅出介绍，从产品的角度来了解其发展历程。
> 
> 1、了解 Universal Link 背后的故事
> 
> 2、学习 Universal Link 功能的使用
> 
> 3、总结 Universal Link 产品的思考

### 一、前言

说起 Universal Link（通用链接），对于有过 iOS 开发的同学，一定有用上过。目前在申请微信分享或登陆时，需要配置 Universal Link 链接。对于 Universal Link，大家应该都了解：

-   苹果 WWDC 2015 提出的 iOS 9 的新功能。
-   方便地通过打开一个 https 链接来直接启动 App (手机有安装 App 的情况下)。
-   实现 web-app 的无缝链接时，能够提供极佳的用户体验。

但是，反过来说，**为什么需要 Universal Link ?** 这就是本文想要趣谈的一个内容。以下内容，是基于之前在团队分享的内容整理而成。

### 二、为什么需要 Universal Link ?

我们知道一个新事物的出现，肯定不是凭空出现，同理，Universal Link 的出现，肯定是基于某个原因或者基础而产生。所以，Universal Link 基于 `Scheme` 基础上而提出来的。

#### URL Scheme

URL Scheme 一般用在在一个 App 里跳转到另一个 App，属于应用间的跳转。当然在浏览器(也可以理解为是 App) web 页面也可以通过 `scheme://` 跳转到 App，但是这种方式在每次跳转的时候都会弹框询问，如果设备中没有安装此 App 则会直接弹出错误提示，体验不友好。大家对以下 scheme 应该不会陌生：

```http
scheme://

weixin://dl/moments（朋友圈）
weixin://scanqrcode（微信扫码） 
alipayqr://platformapi/startapp?saId=10000007（支付宝扫码） 
shoebox:// （Apple Pay）
复制代码
```

##### 为什么会出现 URL Scheme ？

那么，另一个问题又来了，**为什么会出现 URL Scheme ？**

![iOSUniversalLink-6.jpeg](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/30b4fb52b2894d2299007f3e4ad2892f~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

在当年 iPhoneOS 出来时，就已经是有沙盒机制，导致二个 App 之间无法读取对方的沙盒空间，无法直接通讯，所以，苹果提供了 `Apple URL Scheme Reference` 来解决自家的 app 无法交互的问题。

举例来说，在 Safari 浏览器看到某个网页上的电话号码，能不能直接调起拨打电话？我们知道可以这样编码：

```html
HTML link:
<a href="tel:1-408-555-5555">1-408-555-5555</a>

Native app URL string:
tel:1-408-555-5555
复制代码
```

![iOSUniversalLink-7.jpeg](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7cf94fa957cd497c8c7af432c2c9b016~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

可以看苹果的文档看到，URL Schemes 是跟 iPhoneOS 开放给开发者，详细的苹果 URL Schemes 可以文档：[About Apple URL Schemes](https://link.juejin.cn?target=https%3A%2F%2Fdeveloper.apple.com%2Flibrary%2Farchive%2Ffeaturedarticles%2FiPhoneURLScheme_Reference%2FIntroduction%2FIntroduction.html%23%2F%2Fapple_ref%2Fdoc%2Fuid%2FTP40007899-CH1-SW1 "https://developer.apple.com/library/archive/featuredarticles/iPhoneURLScheme_Reference/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007899-CH1-SW1")。

![iOSUniversalLink-9.jpeg](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/cca4940f040b4722bd7e3ec743113591~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

使用 URL Schemes 最多的 App 应该是效率工具类，因为它们有工作流的需求，所以它们把 URL Schemes 玩出了很多花样，包含 `callback-URL` 回调功能。

##### Scheme 缺点是什么 ?

出现 Universal Link，那么说明 URL Schemes 有什么不足呢？那可以反过来说，Universal Link 有什么优点呢？

#### Universal Link 优点

Universal Link 优点，主要有 4 个：

1.  通用性
2.  灵活性
3.  安全性
4.  隐私性

![iOSUniversalLink-13.jpeg](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/153642d338fd408ca03e29fe7ad562fb~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

**通用性**：一个 URL 对你的网站和 App 都通用，Universal Links 是标准的 URL 格式，而自定义 URL Scheme 可能理解为特殊 URL 方案，默认只有你的 App 能解析，浏览器无法解析。

![iOSUniversalLink-15.jpeg](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2def6845ab4d486393cb2bc5d706d077~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

**灵活性**：即使未安装你的 App，Universal Links 也可以使用。未安装你的应用程序时，打开链接，Safari 中打开显示你网站的内容，是符合用户预期的体验，同时，网页可以显示跳转 AppStore 下载的引导，进一步的提升用户体验。

![iOSUniversalLink-14.jpeg](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2b5fb1cca1ae49a48f09729021a2b02f~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

**安全性**：只有开发者自己的网络域名配置了 apple-app-site-association，才能调用对应的 App。而 URL Scheme 配置的 Scheme，任意的 App 都可以配置相同的 Scheme，无法保证开发者 App 的安全调用。另外，当用户安装你的 App 时，iOS 会检查你已上传到网络服务器的文件配置，以确保只有你的网站允许调用您的 App。

![iOSUniversalLink-16.jpeg](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6864fb333af542b7bb6ec6e052e7b98f~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

**隐私性**：很久以前，大家都可以利用 Scheme 检查 App 是否安装，这样有什么作用呢？其实，当你知道用户都安装了什么应用后，可以分析用户的喜好或习惯，当然，目前。另一方面，很多 App 会冒充注册知名的 App scheme 从而拦截调合法 App 的 scheme 调起。

> 注：iOS 9 开始苹果把 URL Schemes 改为白名单机制，也就是只有配置了白名单的 scheme 才可正常检查其他应用是否安装。同时，最多只能设置 50 个不同的 Schemes 白名单（超出 50 个的 schemes 调用 canOpenURL 返回 NO）。

![iOSUniversalLink-17.jpeg](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/11c2c960915b4bde8c2796fd4990af23~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

另外，微信创建应用时，必须配置 Universal Link 链接，详细见文档：[微信开放平台发布新版本SDK，请开发者尽快更新](https://link.juejin.cn?target=https%3A%2F%2Fdevelopers.weixin.qq.com%2Fcommunity%2Fdevelop%2Fdoc%2F00062412e00e4878f8290f35457801 "https://developers.weixin.qq.com/community/develop/doc/00062412e00e4878f8290f35457801")。从安全性和隐私性来说，微信是做的最好和最前卫，连海外 Facebook、Google 的 SDK 现在都还没有提出 Universal Link 的想法。

#### Universal Link 配置

-   只支持 iOS 9+
-   拥有一个域名
-   通过 SSL 访问域名(即支持HTTPS)
-   上传一个 JSON 文件到域名下(名为 `apple-app-site-association` 的json格式文件)

关于 Universal Link 的配置，网上已经有很多教程，这里就不再赘述了。具体可以教程官方文档： [Support Universal Links](https://link.juejin.cn?target=https%3A%2F%2Fdeveloper.apple.com%2Flibrary%2Farchive%2Fdocumentation%2FGeneral%2FConceptual%2FAppSearch%2FUniversalLinks.html%23%2F%2Fapple_ref%2Fdoc%2Fuid%2FTP40016308-CH12-SW1 "https://developer.apple.com/library/archive/documentation/General/Conceptual/AppSearch/UniversalLinks.html#//apple_ref/doc/uid/TP40016308-CH12-SW1")、[Supporting Universal Links in Your App](https://link.juejin.cn?target=https%3A%2F%2Fdeveloper.apple.com%2Fdocumentation%2Fxcode%2Fsupporting-universal-links-in-your-app "https://developer.apple.com/documentation/xcode/supporting-universal-links-in-your-app")。

![iOSUniversalLink-19.jpeg](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5a7c55f0bd584537b12cb38cad99b920~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

![iOSUniversalLink-20.jpeg](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2d76277e59d744b4a49e7db766e8e0b6~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

![iOSUniversalLink-21.jpeg](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9ad23c0b18d64e5c8bd41004c9b0d546~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

![iOSUniversalLink-22.jpeg](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/299842f4aa7d4f81a6a674454fffdcfb~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

#### Universal Link 坑点

虽然苹果提供 [search.developer.apple.com/appsearch-v…](https://link.juejin.cn?target=https%3A%2F%2Fsearch.developer.apple.com%2Fappsearch-validation-tool%2F "https://search.developer.apple.com/appsearch-validation-tool/") 网页让开发者检查 Universal Link 配置是否正常，但是检查不正常的链接，Universal Link 可能是正常的。最大的坑就是必须要跨域，比如配置 Universal Link 链接为：`https://applink.app.com`，那么不能直接在页面中调用此链接来唤起 App，必然是其它二级域名，所以，一般 Universal Link 配置链接是用一个单独的二级域名，与业务域名分开。

最后，最常用的检查配置是否正常的方式有2个： ![iOSUniversalLink-25.jpeg](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8b01daa0858d46b296205925101165c3~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

#### Universal Link 特性回顾

最后，回顾一下，Universal Link 这几年以来的新特性。

![iOSUniversalLink-26.jpeg](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/52f8ba067f6b42db85a40cb48676fcbe~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?) 在 2015 年 iOS 9 推出 Universal Link 功能，在 2017 年在 tvOS 端推出。

![iOSUniversalLink-27.jpeg](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3ac40f994b0b4d17a07b3002fea8191d~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?) 直到 2019年，支持精细化地址匹配，可以多个 App 共用一套配置、路径等。

![iOSUniversalLink-28.jpeg](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/deeff3624a054cfa92e44e9ea563d462~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?) 举例来说，可以通配符匹配。

-   `*`：星号匹配 0 个或多个字符，并且贪婪地匹配。它将匹配尽可能多的字符。
-   `?`：问号匹配一个字符。
-   `?*`：要匹配至少一个字符，请使用问号，后跟星号。

![iOSUniversalLink-29.jpeg](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c76ca41cbe514975a67231b4e7c11aef~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

支持 macOS 10.15 以上，需要注意，Mac 的 App，如果是从 Mac AppStore 下载的 App，默认Universal Link 已经生效，而开发者自己分发的 App 则至少需要打开一次之后才能生效。

![iOSUniversalLink-30.jpeg](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/38ee9fcc96864be68d15cdf57f3a89cb~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?) 2020 年，苹果发布了 SwiftUI，跨平台开发的 UI 框架（支持 iOS、macOS、tvOS、watchOS），所以，如果自然的也要支持 watchOS 啦。需要注意的是，如果 Universal Link 无效，则 watchOS 不能处理，会提示错误信息。因为虽然从 watchOS 5 开始支持 WebKit，但至今 watchOS 还没有内置 Safari 浏览器。哈哈，不知道大家是否期待支持~

![iOSUniversalLink-31.jpeg](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c4156937cc3942219eab2f921031956f~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?) 同时，支持大小写忽略的模式匹配，通过配置 `"caseSensitive": false`，来取消大小写敏感。解决前端不同页面或者大小写的问题。

![iOSUniversalLink-32.jpeg](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e80f31f98f7d4c47ba2b19b29ab3b024~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?) Unicode 模式的支持，比如中文 `蚂蚁上树`，默认情况下需要 ulr encode 才能读取。通过 `"percentEncoded": false` 这样用什么语言都直接显示，方便显示和维护，也减少了链接长度。

![iOSUniversalLink-33.jpeg](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2283bd2fb1ed45f1b94d0638dbde952c~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?) 最后一个重点功能，替代变量的支持，比如 App 在多国家地区出售不同产品，那么可能某个国家或地区不销售某个产品，放在以前就需要写一堆的 `/en_US/`、 `/fr_CA/` 不能的语言地区标识。

![iOSUniversalLink-34.jpeg](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/08bef4825f7544a281f08932cea3331a~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?) 现在，苹果默认提供了常用的变量，举例来说，用 `$(alpha)` 来表示 `[ "A","a", "B", "b", "C", ... "Z", "z" ]` 内任意的字符。其它同理。

![iOSUniversalLink-35.jpeg](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5c86f9d06a764538b203ae5898a80915~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?) 举例来说，通过字段 `"substitutionVariables":` 来自定义字符集，然后可以套用到 `"components":` 里，用 `$()` 来包含替换。

如上图中，`"/$(lang)_CA/$(Canadian food)/", "percentEncoded": false` 表示匹配任意语言的加拿大下的 `Canadian food` 包含的产品，并且是用 Unicode 编码，因为最后一个产品是 `"tête-de-violon"` 非英文字符。同理，第二个包含 `"exclude": true`，表示排除此路径。

![iOSUniversalLink-36.jpeg](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3efd6541a7484546af6ed1257f29b8b6~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?) 原来的 Universal Link 默认是用户安装应用时就通过 App 里配置的 URL 请求 `apple-app-site-association` 配置文件内容。但可能因为开发者网站的部署距离用户远近不同，导致访问速度无法保障，所以，苹果改为通过 Apple CDN 来请求 apple-app-site-association 配置文件并缓存起来，来针对不用地区的用户，加速配置文件的获取。

![iOSUniversalLink-37.jpeg](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/43d33cbe5aba46e4ae481674b577919c~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?) 最后，苹果提供绕过 CDN 下载配置文件的方法，也是方便开发者进行测试 Universal Link。具体来说，就是在设置中的 `Developer` 下 `Associated Domains Development`，然后在 Xcode 配置 `associated-domains` Universal Link 链接时，拼接 `?mode=developer`，这样表示开发者模块，此时的 Universal Link 可以是内网部署，不需要外网部署，非常的方便调试。

### 三、总结

最后，我们从产品的角度来总结一下 `URL Scheme` 和 `Universal Link` 的功能发展。

![iOSUniversalLink-39.jpeg](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9e78fbeb5b754894997adcbbd88e271a~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

URL Scheme 从最初的打破 App 之间无联系的沟通，到效率工具 App 的重度依赖，其中 Workflow App 当年最为流行，后来被苹果收购。正好刚刚说的，被苹果收购后可以获取更多的系统级权限，其实对于效率类 App 是非常利好的！后来，苹果把 Workflow 改名 Shortcuts（捷径），并且能与 Siri 交互。

![iOSUniversalLink-40.jpeg](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/fc6ca235e0164263be2d40966f00f5fc~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?) 举例来说，Shortcuts 能读取 NFC 卡的权限，并且可以打开所有的 App！不需要依赖 URL Scheme，打开所有的 App！所以，URL Scheme 的作用，对于 Shortcuts 来说，根本不需要依赖了。

![iOSUniversalLink-41.jpeg](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/890db8adf548465fbd739ec63d9f08cd~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?) 当然，快捷打开 App，不得不说到 3D Touch，可能从苹果来说，这是一个创新的交互方式，但是用户并没有习惯起来。隐藏式的交互设计，客观来讲，对于用户体验确实不友好。

![iOSUniversalLink-42.jpeg](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4588b4d90578461ea3b7ff15fb2e237f~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?) 当然，最后 URL Scheme 还是会长存！因为第三方 App 之间无法直接交互。除了交互，就是打开 App 某个功能或者路径，利用 PWA 添加到主屏幕也是一种方案，但是对于一般用户需要教导，不太好推广。

![iOSUniversalLink-43.jpeg](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/296bdbdba04e43ad95953757c6cf8579~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?) 最后，Universal Link 总结来说，通用性、安全性、灵活性、隐私性，对于开发者来说，其他人无法伪造，所以的配置都由开发者来掌握。简单来说，通过域名和后台控制，可以随时调整，对用户无影响。

![iOSUniversalLink-44.jpeg](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1ef264711d594915aa06cc9a85947ec8~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?) 举例来说，知乎在 web 页面，利用 Universal Link 显示 “App 内打开”，而顶部是利用 [Smart App Banners](https://link.juejin.cn?target=https%3A%2F%2Fdeveloper.apple.com%2Fdocumentation%2Fwebkit%2Fpromoting_apps_with_smart_app_banners "https://developer.apple.com/documentation/webkit/promoting_apps_with_smart_app_banners") 在用户安装 App 和未安装 App 时，展示打开或者显示（点击时打开 App，或者打开 AppStore 显示）。当然，知乎还用了 URL Scheme 兜底，最后，就是显示 Universal Link 的引导安装的 web 落地页面。

![iOSUniversalLink-45.jpeg](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1d61ec59f68f439b9794f09686f028d6~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

Handoff 也需要使用 Universal Link 的配置文件来验证权限，Shared Web Credentials 也是优化 web 和 app 之间共享账号登陆。

![iOSUniversalLink-46.jpeg](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9fad60c9659f4fe1bd36e5fc3846b7ed~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

去年苹果推出的小程序 [App Clips](https://link.juejin.cn?target=https%3A%2F%2Fdeveloper.apple.com%2Fvideos%2Fplay%2Fwwdc2020%2F10146%2F "https://developer.apple.com/videos/play/wwdc2020/10146/")（轻 App）也是使用 apple-app-site-association 来配置权限。

![iOSUniversalLink-47.jpeg](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c92d7fc35e5046ae842ee41ce9a437bf~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

今年推出的 [in-app events](https://link.juejin.cn?target=https%3A%2F%2Fdeveloper.apple.com%2Fvideos%2Fplay%2Fwwdc2021%2F10171 "https://developer.apple.com/videos/play/wwdc2021/10171") AppStore 商店 App 内事件功能，也需要配置 Universal Link 。

最后的总结，我们说了 URL Scheme 和 Universal Link 的来历，从目前来说，Universal Link 并不能完全替换 URL Scheme，但 Universal Link 因为其优点，苹果把越来越多的功能权限验证，放到了 Universal Link 配置上，相信未来还会有更多 Universal Link。所以，了解这些功能的出现的背后原因和解决的问题，对于我们掌握事物都有帮助，希望大家有所收获，如果觉得可以，欢迎点赞转发啊~

欢迎大家一起在评论区交流~

> 欢迎关注我们，了解更多 iOS 和 Apple 的动态~

### 四、参考引用

-   [About Apple URL Schemes](https://link.juejin.cn?target=https%3A%2F%2Fdeveloper.apple.com%2Flibrary%2Farchive%2Ffeaturedarticles%2FiPhoneURLScheme_Reference%2FIntroduction%2FIntroduction.html%23%2F%2Fapple_ref%2Fdoc%2Fuid%2FTP40007899-CH1-SW1 "https://developer.apple.com/library/archive/featuredarticles/iPhoneURLScheme_Reference/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007899-CH1-SW1")
-   [URL Schemes 使用详解 - 少数派](https://link.juejin.cn?target=https%3A%2F%2Fsspai.com%2Fpost%2F31500 "https://sspai.com/post/31500")
-   [入门 iOS 自动化：读懂 URL Schemes - 少数派](https://link.juejin.cn?target=https%3A%2F%2Fsspai.com%2Fpost%2F44591 "https://sspai.com/post/44591")
-   [微信开放平台发布新版本SDK，请开发者尽快更新 | 微信开放社区](https://link.juejin.cn?target=https%3A%2F%2Fdevelopers.weixin.qq.com%2Fcommunity%2Fdevelop%2Fdoc%2F00062412e00e4878f8290f35457801 "https://developers.weixin.qq.com/community/develop/doc/00062412e00e4878f8290f35457801")
-   [App Search Programming Guide: Support Universal Links](https://link.juejin.cn?target=https%3A%2F%2Fdeveloper.apple.com%2Flibrary%2Farchive%2Fdocumentation%2FGeneral%2FConceptual%2FAppSearch%2FUniversalLinks.html%23%2F%2Fapple_ref%2Fdoc%2Fuid%2FTP40016308-CH12-SW1 "https://developer.apple.com/library/archive/documentation/General/Conceptual/AppSearch/UniversalLinks.html#//apple_ref/doc/uid/TP40016308-CH12-SW1")
-   [Universal Links - Apple Developer](https://link.juejin.cn?target=https%3A%2F%2Fdeveloper.apple.com%2Fios%2Funiversal-links%2F "https://developer.apple.com/ios/universal-links/")
-   [Supporting Universal Links in Your App | Apple Developer Documentation](https://link.juejin.cn?target=https%3A%2F%2Fdeveloper.apple.com%2Fdocumentation%2Fxcode%2Fsupporting-universal-links-in-your-app "https://developer.apple.com/documentation/xcode/supporting-universal-links-in-your-app")
-   [Allowing Apps and Websites to Link to Your Content | Apple Developer Documentation](https://link.juejin.cn?target=https%3A%2F%2Fdeveloper.apple.com%2Fdocumentation%2Fxcode%2Fallowing-apps-and-websites-to-link-to-your-content "https://developer.apple.com/documentation/xcode/allowing-apps-and-websites-to-link-to-your-content")
-   [What's new in Universal Links - WWDC20](https://link.juejin.cn?target=https%3A%2F%2Fdeveloper.apple.com%2Fvideos%2Fplay%2Fwwdc2020%2F10098%2F "https://developer.apple.com/videos/play/wwdc2020/10098/")
-   [What's New in Universal Links - WWDC19](https://link.juejin.cn?target=https%3A%2F%2Fdeveloper.apple.com%2Fvideos%2Fplay%2Fwwdc2019%2F717%2F "https://developer.apple.com/videos/play/wwdc2019/717/")
-   [Extend Your App’s Presence with Deep Linking - WWDC17](https://link.juejin.cn?target=https%3A%2F%2Fdeveloper.apple.com%2Fvideos%2Fplay%2Fwwdc2017%2F250%2F "https://developer.apple.com/videos/play/wwdc2017/250/")
-   [Universal Links 新特性 － 小专栏](https://link.juejin.cn?target=https%3A%2F%2Fxiaozhuanlan.com%2Ftopic%2F3019548672 "https://xiaozhuanlan.com/topic/3019548672")
-   [WWDC20 10098 - What's new in Universal Links － 小专栏](https://link.juejin.cn?target=https%3A%2F%2Fxiaozhuanlan.com%2Ftopic%2F1973850246 "https://xiaozhuanlan.com/topic/1973850246")
-   [Workflow Help](https://link.juejin.cn?target=https%3A%2F%2Fhelp.apple.com%2Fworkflow%2F "https://help.apple.com/workflow/")
-   [快捷指令使用手册 - Apple 支持](https://link.juejin.cn?target=https%3A%2F%2Fsupport.apple.com%2Fzh-cn%2Fguide%2Fshortcuts%2Fwelcome%2Fios "https://support.apple.com/zh-cn/guide/shortcuts/welcome/ios")
-   [Promoting Apps with Smart App Banners | Apple Developer Documentation](https://link.juejin.cn?target=https%3A%2F%2Fdeveloper.apple.com%2Fdocumentation%2Fwebkit%2Fpromoting_apps_with_smart_app_banners "https://developer.apple.com/documentation/webkit/promoting_apps_with_smart_app_banners")
-   [Configure and link your App Clips - WWDC20 - Videos - Apple Developer](https://link.juejin.cn?target=https%3A%2F%2Fdeveloper.apple.com%2Fvideos%2Fplay%2Fwwdc2020%2F10146%2F "https://developer.apple.com/videos/play/wwdc2020/10146/")
-   [Meet in-app events on the App Store - WWDC21 - Videos - Apple Developer](https://link.juejin.cn?target=https%3A%2F%2Fdeveloper.apple.com%2Fvideos%2Fplay%2Fwwdc2021%2F10171 "https://developer.apple.com/videos/play/wwdc2021/10171")

  
作者：37手游iOS技术运营团队  
链接：https://juejin.cn/post/7041091910626181157  
来源：稀土掘金  
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。