#安卓
[Matrix](https://sspai.com/matrix)  是少数派的写作社区，我们主张分享真实的产品体验，有实用价值的经验与思考。我们会不定期挑选 Matrix 最优质的文章，展示来自用户的最真实的体验和观点。 

文章代表作者个人观点，少数派仅对标题和排版略作修改。

---

在很多人的传统观念中，想在手机上做一些超越用户级别权限的事情，一般来说都绕不开解锁 Bootloader、刷入 Magisk 并获取 root 权限等操作。

对我而言也是如此——Magisk 此前的 [动荡](https://sspai.com/post/69945) 让我开始重新审视使用 Magisk 这件事情本身，加之那段时间使用欧版 OneUI 在不刷入 Magisk 的情况下也获得了极为不错的自定义体验，这些经历都让我与曾经的「玩机必备」Magisk 渐行渐远。

取而代之的，是另一个无需 root、门槛更低的开源项目，也是今天文章的主角：[Shizuku](https://github.com/RikkaApps/Shizuku)。

## 如何启动 Shizuku

和 Magisk 殊途同归，我们也可以将 Shizuku 理解为另一种与系统交互并达成定制需求的「桥梁」。

虽然它出自国人开发者，近几年它的名头也渐渐被国外开发者和用户所熟知。它最优秀的地方，用开发者的话来说，在于直接与 system server 进行交互，为部分需要更高权限的应用提供了更高效的系统级接口，并且只需 adb 调试即可开启，无需进行 Bootloader 解锁、刷入 Magisk 等「硬核」操作。

换句话说，对比传统的 root 权限方式，Shizuku 执行更快、上手门槛更低，也不会向用户要求高于实际需求的 root 权限，在我看来是更适合玩家用户的折腾方式。

Android 11 之后，我们的手机其实就具备了「自己调试自己」的能力。一项名为「无线调试」的功能藏在「开发者选项」中，只要设备连接到某个 Wi-Fi 网络即可通过 ADB 无线调试的方式自行「套娃」，无需外接电脑或其余 USB 设备。

以 Shizuku 为例，从 Google Play 商店中下载安装 Shizuku 后，免 root 完成配置的方法与此前我们介绍过的 [Repainter](https://sspai.com/post/72269) 应用类似：

1.  确保手机已开启「开发者选项」；
2.  在 Shizuku 中选择「通过无线调试启动」，然后点击「配对」按钮跳转至开发者选项中；
3.  此时我们需要在开发者选项中找到「USB 调试/无线调试」功能，开启无线调试后，选择「使用配对码配对设备」；
4.  此时 Shizuku 会通过弹出通知的方式提示检测到配对码，输入开发者选项提供的配对码并点击发送，即可完成配对。

![](https://cdn.sspai.com/editor/u_/ca27qndb34tfqgrhk1n0.png?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

此后每一次设备重启或 Shizuku 失效，我们都可以通过同样的流程重新启动 Shizuku，值得一提的是，虽然听上去比较麻烦，但无线调试配对状态是可以保存的，所以我们每次只用重新启动无线 ADB 调试即可，配对流程可以省略。

另外这里还有个快速开启无线调试的小技巧：开发者选项中的部分选项是可以放入快捷操作面板的，其中就包括了「无线调试」「关闭传感器」等，可以在开发者选项中的「快捷设置开发者图块」中勾选。

![](https://cdn.sspai.com/editor/u_/ca27qnlb34tfqrohjot0.png?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

> Tips：以上类似的无线调试授权，同样适用于黑阈等应用。

## 它能帮你做什么？

走完上述步骤成功运行 Shizuku 进程后，我们便能借助它帮助第三方应用获取到更高的权限了——但这只是个模糊的意向，这个「更高权限」到底能够解决什么样的具体需求呢？

这里我们不妨举几个例子。

### 停用应用

涉及应用：

-   [冰箱](https://sspai.com/app/Ice%20Box%20%E5%86%B0%E7%AE%B1)
-   [雹](https://github.com/aistra0528/Hail)
-   [小黑屋](https://www.coolapk.com/apk/web1n.stopapp)

在 Android 上，借助应用管理器可以将应用处于「停用」或者说「冻结」的状态，在这个状态下应用不会有任何活动，达成类似「卸载」的效果同时，还能随时启用。这个功能非常适用于外卖、购物、订票、健身等低使用频率场景，你也可以像我一样周末一键停用飞书、微信，被停用的应用将无法正常推送通知，手机因此更轻快、生活也更加清净。

Shizuku 能向冰箱、小黑屋、雹等工具提供 API 支持，而且比起传统 root 方式下需要工具不停发起命令、逐个处理文本来获取执行结果的方式更快捷高效——哪怕你的设备已经 root，也推荐使用 Shizuku 方式。

至于工具本身，这三款工具各有千秋：冰箱较为老牌，功能上比较完善：支持以语音助手的形式快捷呼出冰箱抽屉，也支持分 Tab 冻结应用；雹则是一款免费的开源应用，且已经适配 Matrial You Design，更加透明也更加新潮。

三款均支持自动冻结功能，有内购付费的两款也都支持免费试用。

![](https://cdn.sspai.com/editor/u_/ca27qntb34tfqrohjotg.png?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

![](https://cdn.sspai.com/editor/u_/ca27qo5b34tfqgrhk1ng.png?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

冰箱的多 Tab 功能深得我心；雹的开源免费特性也不错

### App Ops 权限管理

涉及应用：

-   [App Ops](https://sspai.com/post/61348)
-   权限狗

权限管理功能近年来往往和手机系统主打的隐私保护特性挂钩，但厂商们强调这个功能的同时却并没有让这个功能变得更好用，批量设置、模板套用等需求依然鲜有受到照顾，更不用说许多细分、冷门的权限并没有开放供用户设置。App Ops 类的应用在我看来则是一种补充和加强。通过它们，我们能够穷尽权限管理功能的所有可能。

这里同样需要 Shizuku 提权方可使用，如前文所说，执行效率也比 root 模式略胜一筹。

**关联阅读：**[在权限管理上跑过 iOS 14 和 Android 11：App Ops 4.0 上手指南](https://sspai.com/post/61348)

这里主要介绍 App Ops 这款应用，与 Shizuku 出自同一开发者之手，不仅拥有权限模板、权限备份和恢复、批量设置功能，在常驻后台的情况下可以提供类似 iOS 上的剪贴板监视器，配合「读取剪贴板内容」「修改剪贴板内容」两项权限，**在剪贴板方面隐私防护上甚至可以比 iOS 做得更到位**。

「新应用自动套用模板」则可以让权限设置更懒人友好一些，设置好权限的同时让我尽可能地少操心，一次配置之后我已经鲜少手动打开 App Ops 了。总体而言，在 App Ops 中，设置权限不是用户和系统打架，而更像是让用户声明意志、让系统贯彻执行。

![](https://cdn.sspai.com/editor/u_/ca27qodb34tfqt7q07ug.png?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

![](https://cdn.sspai.com/editor/u_/ca27qolb34tfqt7q07v0.png?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

另外，在 App Ops 中特别常用、同时也值得设置为模板批量套用给国内「毒瘤应用」的一项权限设置是：「严格限制在后台运行」。无论是 Android 9 还是 Android 13，系统都会更多约束应用的后台行为。

### 静默/批量安装应用

**涉及应用：**

-   [Aurora Store](https://auroraoss.com/)
-   [Swift Backup](https://play.google.com/store/apps/details?id=org.swiftapps.swiftbackup&hl=en_US&gl=US)
-   R installer
-   SAI

因为允许侧载应用（也就是开放用户自行安装应用包），Android 上除了 Play 商店与厂商提供的官方应用商店，还有类似 Aurora Store、F-Droid、FFUpdater 等各有特色的第三方应用商店和仓库。

可惜的是这些「第三方」名号的商店不够老字牌，本质上还是在分发安装包。因此在安装应用时，一个一个应用手动安装的流程也是难免，需要一次安装的应用较多时，步骤则会更加繁琐、需要我们时刻留意和操作。

Shizuku 可以提供更高的「静默安装」权限，但这需要应用本身适配和接入 Shizuku。获取静默安装权限后，应用本身可以负责批量下载，这就使得「快速批量安装应用」成为了现实。

以少数派介绍多次的 Swift Backup 这款备份利器来说，虽然非 root 模式下无法接触应用数据，不过能批量把一台手机上安装的所有第三方应用转移到另一台手机上已经方便许多，美团、盒马、淘宝等服务类应用对我来说只需要简单登录一下即刻使用。另外，Swift Backup 也支持安装 Play 商店的 .aab 形式的应用捆绑包格式。

![](https://cdn.sspai.com/editor/u_/ca27qotb34tfqgrhk1o0.gif)

再大胆点：如果直接替换系统的 Package installer 安装包解析器，并给予 Shizuku 权限，岂不是可以全局生效、对任何应用包静默安装？国内的开发者们也注意到了这个方案，并开发出 R installer 这款静默安装应用的应用。对于国行用户来说，使用 R installer 也可避免系统自带应用安装器的各种牛皮藓广告。

### 更换 Android 12 的系统主题色

-   Repainter

得益于 Material You 新设计语言的引入，Android 12 也终于在系统层面供用户选择主题色彩。系统接口的出现也意味着 Hack 的可能，从 Android 12 测试版开始就深度探索系统接口的独立开发者 @[Danny Lin](https://twitter.com/kdrag0n)，也以此为契机开发出了更为通用的工具：Repainter，同时提供了传统的 root 方式以及 Shizuku 方式。

更详细的介绍与使用体验可以参照少数派此前的文章：

-   [App+1 | Android 12 装机必备，免 root 实现 Material You 二次定制：Repainter](https://sspai.com/post/72269)

### 分应用强制暗色主题

-   [DarQ](https://github.com/KieronQuinn/DarQ)

暗色主题从 Android 10 开始推广，到今天已有两三个年头了，大部分应用都完成了对暗色主题的适配。如果还有部分「刺头」不肯适配，可以尝试在开发者选项中开启「强制黑暗模式」选项来通过智能反色达成效果。美中不足的是，这个选项开启后会在所有应用里生效。能否精细一些，只对部分应用生效？

![](https://cdn.sspai.com/editor/u_/ca27qptb34tfqrohjou0.png?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

DarQ 是一款可以借助 Shizuku API 来分应用强制黑暗模式的工具，对于像 DevCheck 这样把暗色主题当作付费点的应用也同样好使。并且 DarQ 还支持通过地理位置或时区来决定是否强制应用深色主题。

## 结语

需要注意的事，Shizuku 与 Magisk 并不是互为替代的方式，后者对用户来说更硬核、要求更高，当然能实现的功能也更多，前者只是借用系统自带的调试功能完成提权并供第三方应用调用。如果两者搭配使用，Shizuku 也不必每次重启后重新授权、也减少了第三方应用滥用 root 权限的可能，是更完美的方案。