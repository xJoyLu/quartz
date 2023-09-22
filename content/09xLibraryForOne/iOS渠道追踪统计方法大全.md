说起 iOS 的渠道统计，不少人会想到苹果官方的 App 分析功能（iTunes Connect），但实际操作中我们会发现，这个服务的统计维度还不够全面，许多广告主和运营人员更关心的是各个推广渠道实际带来的安装量、注册量等数据，毕竟这对渠道引流的分析价值更大。iOS的“渠道”通常是指那些在其它 App 或者网页内部，提供到达 App Store 的链接的页面。因此，在 iOS 中追踪发行渠道，主要是追踪进入 App Store 相关页面的渠道信息。

从技术角度来看，也就是在用户**首次下载时不仅要获取下载来源，还要实现参数传递，**简单来说，就是用户第一次下载后，我能得知后续的注册、活跃、付费等操作行为。或者在此基础上，实现场景还原，帮助用户在首次打开 App 后直接跳转进指定页面，而不是首页。

**方案一：苹果官方自带的统计工具** **[iTunes Connect](https://itunesconnect.apple.com/login)**

![](https://cdn.sspai.com/2019/07/19/951cd693aab38d0671eb7266ceb4786b.png?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

登录 iTunes Connect ，在“App 分析”中，能很方便的查看 App 的展示次数、购买量等基础数据，但无法获取更加详细的安装量、注册量等运营数据。

当然，往往 App 推广的渠道会有很多同时进行，怎么对多个渠道的来源做分析呢？同样在“App分析”的“来源”中点击“营销活动”，右上角有个“生成营销活动链接”，进入后就能自定义给每个渠道生成对应的唯一标识。

![](https://cdn.sspai.com/2019/07/19/13646573a8f84a0e2d5221baad7d6a0e.jpg?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

![](https://cdn.sspai.com/2019/07/19/ec2edde843e5a450a275ac58e311959b.jpg?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

这种方法虽然可以追踪到多个渠道的来源，但存在以下几个问题：

1.  只有当营销活动启动后超过一天时间（最长72个小时）后才能显示相关数据；
2.  至少有 5 个 App 购买量归因于此营销活动时，营销活动才会在“App 分析”中显示；
3.  无法兼容 Android 和 iOS企业签名，采用不同的统计方法可能会让数据统一性较差；
4.  iOS 8.0 及以上版本的用户可以选择是否将自己的应用使用情况的数据发送给Apple。

**方案二：使用 SFSafariViewController 传递参数**

SFSafariViewController 是 iOS 9.0 出现的，可以通过 Safari 对应的 cookier 传递参数，跨App与Safari共享数据。但是 openurl 失败率还是很高，并且有系统版本、浏览器等限制，比如微信等第三方 App 的内置浏览器就不能很好实现。

**方案三：通过 IDFA 进行追踪，比如** **[Google Analytics](https://developers.google.cn/analytics/devguides/platform/)**

常用的比如谷歌官方的 Google Analytics，它的获取原理就是通过获取设备的 IDFA ，来作为唯一标示符号，然后根据你的渠道来源提供数据，通过比对的方式进行渠道定位。弊端在于，用户重置系统，或者关闭广告跟踪的话，这种方法就会失效。

苹果设备设置里都会有一个开关用于限制广告跟踪：

![](https://cdn.sspai.com/2019/07/19/6d49375d7ff601f2502eb6b8b19d6db1.png?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

 目前用户的隐私保护意识也在逐渐觉醒，只要用户手握这个开关，IDFA 的统计误差就始终存在。

另一方面，Google Analytics 的 iOS 安装跟踪功能仅适用于通过移动广告网络（例如投放应用内广告的AdMob）投放的广告。也就是如果渠道是从线下扫二维码或者web上的推广链接下载是不能通过这种方法跟踪到的，这时就需要其它工具作为补充。

![](https://cdn.sspai.com/2019/07/19/dd8fc1dd7b267f026749fc8555fc4a65.png?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

 **方案四：通过模糊特征匹配的方式进行追踪**

用户点击下载链接，会跳转到 App Store 里，这个过程会触发一个服务端的请求，服务器来记录这次点击的设备信息，包括 ip 地址、机型等。同时，被推广 App 这边，也可以记录用户激活 App 时设备的一些基本信息，并上传至服务器。结合下载和激活的时间差，再结合设备的 IP 地址和机型等信息，大概可以模糊地识别出同一个用户先点击了下载链接，再激活了 App，从而确定下载渠道。这种方式在面对用户量大的渠道时，准确率就会下降不少。

**方案五：采用第三方 SDK 追踪，比如** **[openinstall](https://www.openinstall.io/)** 

openinstall 基本原理：

![](https://cdn.sspai.com/2019/07/19/d04f1aded18e761196e67b4a142b1f8f.png?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

1.  开发者在分享的 h5 页面上集成 openinstall web sdk，发布分享链接时在url上动态的拼接任意的自定义参数（如推广渠道号，邀请码，游戏房间号等等）；
2.  当某一终端访问该 h5 页面时，openinstall web sdk 将同时确定该设备的个性化信息和采集自定义参数，上传至 openinstall 服务器， 待用户通过该 h5 页面安装 App 后首次打开时，使用 openinstall Android/iOS sdk 从 openinstall 服务器再取回暂存的自定义参数。

在推广渠道相当多的情况下，通过分发 h5 落地页给不同渠道，从每个渠道来的用户，没有任何感知的情况下，后台可以统计到他激活及注册时的渠道 ID （甚至其他任意参数）。实际误差是较低的，相比其他方法精准度更高。

这种方法没有 iTunes Connect 的诸多限制，也很好的补充了 Google Analytics 不能统计网页下载渠道的弊端，理论上可以同时生成无上限的渠道链接进行统计，由于是国内产品，还能实时反馈数据情况。

**总结：**

我的建议是，如果自己的业务既有网站又有 App 的话，Google Analytics 的一系列产品都可以使用，毕竟都用同一种统计工具，可以保证数据的统一性，方便数据分析。

当然，从权威性来看，苹果官方的 iTunes Connect 自然更加值得信赖，但上文提到的弊端需要适当斟酌。

两者在使用中都可以用 openinstall 来补充弊端，如果产品主要是面对移动端，openinstall 甚至可以兼容安卓的统计，在市场运营中也能保证数据的统一性。