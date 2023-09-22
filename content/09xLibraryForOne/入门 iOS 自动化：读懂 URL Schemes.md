之前我写过一篇《[URL Schemes 使用详解](https://sspai.com/post/31500)》，其中把 URL Schemes 从功能上分为了 4 种：

1.  **基础 URL Schemes**：用于启动应用，比如：[drafts4://](drafts4://)；
2.  **复杂 URL Schemes**：用于直接打开应用的具体功能，比如：[drafts4://dictate](drafts4://dictate)；
3.  **变形 URL Schemes**：用于输入内容，含有第三方应用的特殊语法，比如：在 Launch Center Pro 里用这一条 `drafts4://create?text=[prompt]`；
4.  **x-callback-URL：**前面的 URL Schemes 只能执行一个动作，而 x-callback-URL 可以根据根据前一段 URL Schemes 的执行情况决定进一步的行动。

作为补充，在这篇文章，我来介绍一下 URL Schemes 正式的读法。包括每个部分是什么、符号都是什么意思，以及阅读文档时该从哪些地方入手，注意哪些细节。

订阅 [Power+](http://sspai.com/s/nMow) ，了解 URL Schemes 在 Launch Center Pro、Drafts、Bear、OmniFocus 等效率应用上的进阶用法。

## 概览

一个 URL Schemes 分为 Scheme、Action、Parameter、Value 这 4 个部分，中间用冒号 `:`、斜线 `/`、问号 `?`、等号 `=` 相连接。

拿 `things:///add?title=正文内容&note=备注` 来说：

1.  Scheme（链接头）是 `things`；
2.  Action（动作）是 `add`；
3.  Parameter（参数）是 `title` 和 `note`；
4.  Value（值）是 `正文内容` 和 `备注`。

另外在不同的部分之间有符号相连，它们也有一定的规则：

-   冒号`:`：在**链接头**和**命令**之间；

-   双斜杠 `//`：在**链接头和命令**之间，有时会是三斜杠 `///`；
-   问号 `?`：在**命令和参数**之间；
-   等号 `=`：在**参数和值**之间；
-   「和」符号 `&`：在**一组参数和另一组参数**之间。

接下来就来详细地讲一下这些部分，以及链接它们的符号。

## Scheme（链接头）

这个东西在 URL 里本来用来表示协议，比如 `http`、`https`、`ftp` 等。但是，在 iOS 的这些 URL 里它们就不是协议了，而是**启动一个应用的 URL**。

除此之外，通过 URL 执行的复杂命令都得以这一段 Scheme 为起始，鉴于没有官方的翻译，我暂且在此称其为「链接头」。

如果我们只是需要一个启动应用的 URL，那么「链接头+冒号」的部分就足够满足需求。比如 [things:](things:)、[omnifocus:](omnifocus:)、[spotify:](spotify:) 都可以直接跳转到相应应用。

## 文档阅读注意点：斜线数量

我们会发现一般的链接头后面都会加冒号和双斜线 `://`——比如 [weixin://](weixin://)——以至于我们会把链接头和这个双斜线看为一个整体。

然而这个双斜线其实是有特殊作用的。根据我的理解，在 iOS 上的 URL Schemes 中，跟在链接头后的双斜线 `//` 用于声明一个领域。这一点在支持 URL Schemes 的社交应用、支持 x-callback-URL 的应用都有一定的体现，还有一些特例。

### 在社交工具里的使用

最典型的用例是 Tweetbot 这样的社交应用，在它的 [URL Schemes 文档](https://tapbots.net/tweetbot3/support/url-schemes/)里，每一个 URL 的双斜线后面都有 `<screenname>` 这个部分。它的作用是，当你在 Tweetbot 登录了多个 Twitter 账户，可以用 <screenname>，来指定执行操作的是哪个账户。

一个使用情境：

1.  在 Tweetbot 里，我登录了 @JailbreakHum 和 @CheckedFM 这两个账户；
2.  我一般只看 @JailbreakHum 这个账户的时间线；
3.  所以我 Tweetbot 的首页是 @JailbreakHum 的时间线；
4.  这时我想直接使用 @CheckedFM 这个账户发推文；
5.  我可以用 `tweetbot://checkedfm/post` 这段 URL 直接把账户切换到 @CheckedFM，并弹出编写推文的界面。

在 Tweetbot 中，这个 `<screenname>`  的部分**可以不填**。如果不填，也就是留白的话，链接会变成 [tweetbot:///post](tweetbot:///post)，链接里是 3 条斜线，功能会变成是**使用当前正在使用的账户发推**。也就是说，它会使用 @JailbreakHum 这个账户发推，而不会切换到 @CheckedFM 发推。

这个逻辑同样适用于微博第三方客户端墨客。

### 在 x-callback-URL 中的使用

在这里我打算用 Drafts 来举例，如果我们想通过 URL Schemes 在 Drafts 里添加一个草稿，有 3 个可以用的 URL：

1.  双斜线 `//`，比如 [drafts4://create?text=A](drafts4://create?text=A)，
2.  三斜线 `///`，比如 [drafts4:///create?text=A](drafts4:///create?text=A)
3.  双斜线 + 内容 + 斜线 `//[Something]/`，[drafts4://x-callback-url/create?text=A](drafts4://x-callback-url/create?text=A)

这三种用法，都可以让 Drafts 生成一个新的草稿，内容为 `A`。那么它们的区别是什么？

在这个例子里，**最完整、也最不容易产生理解问题的用法**是最后这个：[drafts4://x-callback-url/create?text=A](drafts4://x-callback-url/create?text=A)。

而第二个用法 [drafts4:///create?text=A](drafts4:///create?text=A)，是省略掉了 `x-callback-url` 。在用不到 x-callback-URL 的情况下，把链接中的 `x-callback-URL` 省掉是比较通常的做法，[Things 的用法](https://support.culturedcode.com/customer/en/portal/articles/2803573-things-url-scheme)也是一样。

最后，是双斜线的情况，[drafts4://create?text=A](drafts4://create?text=A)。

这种用法其实应该是不太规范的。如果一个应用支持 x-callback-URL，并且用 `drafts4://x-callback-url/` 的形式来使用 x-callback-URL，那它要么要带上这个 `x-callback-URL` ，要么它把它省去，变成三斜线 `drafts4:///`。比如 Things 的 URL Schemes，要么带上这个 x-callback-URL，要么三斜线，如果用双斜线会被提示错误：

![](https://cdn.sspai.com/2018-03-07-Things%20URL%20%E6%8A%A5%E9%94%99%E6%8F%90%E7%A4%BA.png?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

Things URL 报错提示

但是 URL Schemes 的写法似乎并没有一个特别严格的标准，所以只要在功能上可用，我们也不用纠结对错。只是如果出现问题，可以在这里找一下原因。

### 其它的情况

除了社交应用和支持 x-callback-URL 的应用这两种比较典型的情况外，还有一些其它零散的找不到规律的情况，也会在三斜线之间加入内容。之前的微信和现在的支付宝就属于这种情况。

现在微信的 URL Schemes 已经几乎全部失效了，但是过去它的 URL Schemes 中总会带一个 `dl`，也就是 `weixin://dl/moments`（**打开朋友圈**）这样的。

支付宝的 URL Schemes 也有 `platformapi` 这个部分，比如**付款码**是：[alipayqr://platformapi/startapp?saId=20000056](alipayqr://platformapi/startapp?saId=20000056)。

最后，除了上述这三种情况，有相当一部分支持 URL Schemes 的应用不需要三斜线，只用双斜线就可以正常工作。

## Action（动作）

链接头和斜线之后，跟的是动作（Action）。动作在一些文档里1 也被称为「Command（命令）」。

一段 URL 里加上这个部分就说明它有具体的功能了，比如：[drafts4:///create?text=A](drafts4:///create?text=A) 里的「create」，它代表的**动作**就是「创建」，所以在 Drafts 中相应的**动作**就是新建笔记。

### 文档阅读注意点

一般的 URL Schemes 文档都是由**动作**来组织的，所以阅读文档时，可以先找自己需要的动作，再进行研究。比如 [Bear 的文档](http://www.bear-writer.com/faq/X-callback-url%20Scheme%20documentation/)里就以 `/动作名` 的形式给出了 12 个动作：

-   `/open-note` 是打开笔记
-   `/create` 是创建笔记
-   `/open-tag` 是打开标签
-   剩下 9 个就不一一列举了

在动作之后可以接参数（Parameter）也可以不接，比如 OmniFocus 打开 Inbox 的 URL Schemes 是 [omnifocus:///inbox](omnifocus:///inbox)，就没有接参数。如果要接参数的话，动作和参数之间，按规定由问号 `?` 连接。这个地方，更确切地说，应该是「参数以问号 `?` 为起始」，所以不接参数就不用带这个问号。

## Parameter（参数）和 Value（值）

在动作之后，是 Parameter（参数）和 Value（值），**参数是该程序的程序员决定的，值是用户根据自己需求填入的。**参数和值的中间用等号 `=` 连接，因为 `=` 在编程中多是赋值的意思。比如我们写 `A = 3`，就是**让 A 等于 3** 的意思，这就是赋值。

拿 [drafts4:///create?text=A](drafts4:///create?text=A) 来说，参数是「text」，值是「A」。「text」这个参数是开发者决定的，我们不能改，改了就无效了。而「A」这个值是我们用户决定的，可以写成任何我们需要的内容。

如果有两组参数，比如我们在 Things 中添加任务要添加**任务名**和**备注**，就要用「和」符号 `&` 来连接它们：[things:///add?title=任务名&notes=备注](things:///add?title=%E4%BB%BB%E5%8A%A1%E5%90%8D&notes=%E5%A4%87%E6%B3%A8&reveal=true)。

### Parameter（参数）文档阅读注意点

前面说过，文档一般是由动作组织的，**也就是一篇文档的文章中，大标题一般都是动作。**而接下来的中标题，一般都是参数，还拿 Bear 的文档举例子，在 「/create」下面，有「parameter」的字样，下面有 10 个参数：

-   `title`，笔记标题
-   `text`，笔记内容
-   `tags`，标签
-   ……

我们还会发现，在每个具体的参数后面，会有「optional（可选的）」和「required（必要的）」的字样。它们指示了执行这个动作，某个参数是不是必要的。

来看 [omnifocus:///add?name=买牛奶](omnifocus:///add?name=%E4%BB%BB%E5%8A%A1%E5%90%8D)，这里的「add」是动作名，后面跟了问号 `?`，再后面的「name」是参数名，后面跟了等号 `=`，最后的「买牛奶」是值。通过它我们可以建立一个任务名为「买牛奶」任务。

而这其中的参数「name」是 optional（可选的），也就是说我不用加参数，只用 [omnifocus:///add](omnifocus:///add) 也可以工作。点前面的连接，如果你有 OmniFocus 的话，就会发现打开了 OmniFocus 添加任务的界面，但是接下来需要自己填写内容。

## 小结

以上总结的是比较常见的 URL Schemes 使用方法，但是实际上 iOS 上的 URL Schemes 并没有特别严格的规范。写这篇文章时，我发现哪怕是知名应用的开发者在制作 URL Schemes 时，也会出现不大规范的地方，比如：

最开始提到的 Drafts 的三种斜线的情况，理论上 `drafts://create` 这种 URL 应该是不规范的，它自己[文档](https://agiletortoise.zendesk.com/hc/en-us/articles/202771400-Drafts-URL-Schemes)里都写了：「All URLs should begin with the base URL "drafts4://x-callback-url/[action]” where action is one of the actions listed below.」

OmniFocus 显示今天的任务时，可以直接用 `omnifocus:///today`，这种行为是把「today」当成了一个动作，理解可以理解，但不是特别舒服。而更规范的用法应该是 Things 的 `things:///show?id=today`，动作是「show」，即显示，显示什么呢？显示「today」里的内容。

Bear 在文档中，「/create」下的所有参数都是 optional，也就是说，哪怕我只填写「create」这个命令，也是应该有效的，因为所有参数都是选填嘛。但是实际上，`bear://x-callback-url/create` 这段 URL 是没效果的，不会触发「create」这个动作。更好的做法应该是 OmniFocus 那样，`omnifocus:///add` 也能触发添加任务的动作。

Spotify 的 URL Schemes 更是完全没有按照传统的规范来写，但是也可以正常使用，[查看文档](https://community.spotify.com/t5/Spotify-Answers/Spotify-Feature-amp-App-Shortcuts/ta-p/919201)。

iOS 开发者 [@陈某豪](https://twitter.com/chan__jh) 在 Power+ 本文下的评论中表示，其实只有链接头（配置文件中叫「HOST」）这个部分是苹果强制要求的，而其他部分则根据开发者的理解发挥，因此出现这种乱象。

不过，如果开发者能按照一定的规范，特别是知名应用们已经建立起的更 iOS 的思路去写 URL，会更有助于用户理解你的 URL 和文档。

另外，这篇文章没有涉及到 x-callback-URL 的细节。x-callback-URL 的文档毫无疑问也有一些特殊的地方，那是另一个主题，有机会我会再写一篇文章去说明。

---

订阅 [Power+](http://sspai.com/s/nMow) ，了解 URL Schemes 在 Launch Center Pro、Drafts、Bear、OmniFocus 等效率应用上的进阶用法：

-   [通过 Bear 来认识 Launch Center Pro 的进阶用法](http://sspai.com/s/Kj6B)
-   [通过 Bear 来认识 Drafts 的 [[line]] 用法](http://sspai.com/s/nOQW)
-   [从 OmniFocus 认识 Drafts 的 Prompt 用法](http://sspai.com/s/J7aL)