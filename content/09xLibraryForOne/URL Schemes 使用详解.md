编注：本文是 Hum 的早期作品（2015 年 10 月 10 日），文章属性较强，如果想要更快更系统地理解 URL Schemes 的使用，建议阅读 Hum 最近（2018 年 5 月 18 日）写的《[入门 iOS 自动化：读懂 URL Schemes](https://sspai.com/post/44591)》一文。

[![](https://cdn.sspai.com/attachment/origin/2015/10/10/286107.png?origin?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)](https://sspai.com/user/681230/posts)

> 用原生 iOS 的人分两种，懂 URL Schemes 的和不懂的。
> 
> 前者是「魔法师」，后者是「麻瓜」。

---

URL Schemes 应用在 iOS 上已经很久了。对于使用者来说，在沙盒机制下的 iOS 中，如果想做到一定程度上的自动化就不可避免地要用到 URL Schemes。但因为 URL Schemes 的使用方式不像传统 iOS 使用者接触到的图形界面那样可以直观地点来点去，造成了对它有兴趣的人（尤其是对英文有恐惧的人）一定程度上理解的困难。

而且大多数目前正在使用 URL Schemes 的人并不具备自己编写符合自己使用情境的 URL Schemes 的能力，于是他们更多的是跑到各种社交网站上去「求帮助」。所以当我们在搜索 URL Schemes 相关词条的时候，我们会看到那些社交网站上的人们分享出来的 URL Schemes 列表。新人们对此如获至宝，仿佛列表以外再无 URL Schemes，在列表中急切地搜索自己想要的应用，如果没有就一脸失望，如果有了就愉悦地复制粘贴。

实际上那些列表中的 URL Schemes 你都可以自己找到，那些你在用别人没在用的应用的 URL Schemes 也同样可以找到。更重要的是你要有能力通过 URL Schemes 为自己打造满足自己需求的自动化操作。

我希望通过这篇对 URL Schemes 的**使用方式**详细说明的文章，来解除想使用 URL Schemes 的朋友对它的疑惑，比如这些问题：

-   「什么是 URL Schemes 啊？」
-   「URL Schemes 怎么用啊？」
-   「从哪找我想用的应用的 URL Schemes 啊？」
-   「国内的 xx 软件支持不支持 URL Schemes 啊？」

都能在文章中找到答案。

文章目录（想看使用部分的可以直接跳转到[基本 URL ​Schemes](https://sspai.com/post/31500#04)）：

1.  [简介苹果的沙盒机制](https://sspai.com/post/31500#01)
2.  [URL Schemes 是什么](https://sspai.com/post/31500#02)
3.  [URL Schemes 的发展](https://sspai.com/post/31500#03)
4.  [基本 URL Schemes](https://sspai.com/post/31500#04)
5.  [复杂 URL Schemes](https://sspai.com/post/31500#05)
6.  [变形 URL Schemes](https://sspai.com/post/31500#06)
7.  [x-callback-URL](https://sspai.com/post/31500#07)
8.  [URL En/Decode（编码/解码）](https://sspai.com/post/31500#08)
9.  [如何查找以上各类 URL Schemes](https://sspai.com/post/31500#09)
10.  [URL Schemes 的衰败](https://sspai.com/post/31500#10)
11.  [结语](https://sspai.com/post/31500#11)

注：文中会提到使用 [Launch Center Pro](https://sspai.com/tag/Launch%20Center%20Pro)、[Drafts](https://sspai.com/tag/drafts/) 等应用的例子，它们都是同类应用中的最好选择，而支持 URL Schemes 是促成它们如此地位的不可忽视的原因。如果想深入了解 URL Schemes，这些应用恐怕是必不可少的。你可以在 [AppShopper](http://appshopper.com/) 这样的网站参考其以往价格，以便在你觉得价格合适的时候入手这些应用。

## 简介苹果的沙盒机制

_苹果选择沙盒来保障用户的隐私和安全，但沙盒也阻碍了应用间合理的信息共享，于是有了 URL Schemes 这个解决办法。_

一般来说，我们使用的智能设备上有许多我们的个人信息。比如：联系方式、银行卡/信用卡信息、支付宝/Paypal/各大商城的账户密码、照片甚至行程与位置信息等。

如果说，你设备上的每一个应用，不管是官方的还是你从任何商城安装的应用都可以随意地获取这些信息，那么你轻则收到骚扰信息和邮件、重则后果不堪设想。如何让这些信息不被其它应用随意使用，或者说，如何让这些信息仅在设备所有者本人知情并允许的情况下被使用，是所有智能设备与操作系统所要在乎的核心安全问题。

在 iOS 这个操作系统中，针对这个问题，苹果使用了名为「沙盒」的机制：应用只能访问它声明可能访问的资源。一切提交到 App Store 的应用都必须遵守这个机制。

在安全方面沙盒是个很好的解决办法，但是有些矫枉过正。敏感的个人信息我们不愿意透露，却不代表所有的信息我们都不想与其它应用共享。

比如说我们要一次性地（没错，只按一次）把多个事件放到日历中，这些事件包含日期时间以及持续时间等信息，如果 App 之间信息不能沟通，就无法做到这点。（在下文中的 [x-callback-URL 的部分](https://sspai.com/post/31500#07)会详述整个过程）

类似于一次性添加多个日历事件这样的，我们在使用智能设备的过程中会遇到很多不必要的重复的步骤。大多数人对这些重复的步骤是不自觉的，就像当自己电脑里有一批文件需要批量重命名的时候，他们机械地重复着重命名的过程。但是当我们掌握了这些设备运行的模式，或者有了一些工具，我们就能将这些重复的步骤全部节省下来。在 iOS 上，我们可以利用的工具就是 URL Schemes。

## URL Schemes 是什么

_通过对比网页链接来理解 iOS 上的 URL Schemes，应该就容易多了。_

URL Schemes 有两个单词：

-   URL，我们都很清楚，`http://www.apple.com` 就是个 URL，我们也叫它链接或网址；
-   Schemes，表示的是一个 URL 中的一个位置——最初始的位置，即 `://`之前的那段字符。比如 `http://www.apple.com` 这个网址的 `Schemes` 是 **http**。

根据我们上面对 URL Schemes 的使用，我们可以很轻易地理解，在以本地应用为主的 iOS 上，我们可以像定位一个网页一样，用一种特殊的 URL 来定位一个应用甚至应用里某个具体的功能。而定位这个应用的，就应该这个应用的 URL 的 Schemes 部分，也就是开头儿那部分。比如短信，就是 `sms:`

你可以完全按照理解一个网页的 URL ——也就是它的网址——的方式来理解一个 iOS 应用的 URL，拿苹果的网站和 iOS 上的微信来做个简单对比：

 

网页（苹果）

iOS 应用（微信）

网站首页/打开应用

http://www.apple.com

weixin://

子页面/具体功能

http://www.apple.com/mac/（Mac页面）

weixin://dl/moments（朋友圈）

在这里，`http://www.apple.com` 和 `weixin://` 都声明了这是谁的地盘。然后在 `http://www.apple.com` 后面加上 `/mac` 就跳转到从属于 `http://www.apple.com` 的一个网页（Mac 页）上；同样，在 `weixin://` 后面加上 `dl/moments` 就进入了微信的一个具体的功能——朋友圈。

**但是，两者还有几个重要的区别：**

1.  所有网页都一定有网址，不管是首页还是子页。但未必所有的应用都有自己的 URL Schemes，更不是每个应用的每个功能都有相应的 URL Schemes。实际上，现状是，大多数的应用只有用于打开应用的 URL Schemes，而有一些应用甚至没有用于打开应用的 URL Schemes。几乎没有所有功能都有对应 URL 的应用。**所以，不要说某某应用烂，不支持国内应用。一个 App 是否支持 URL Schemes 要看那个 App 的作者是否在自己的作品里添加了 URL Schemes 相关的代码。**
2.  一个网址只对应一个网页，但并非每个 URL Schemes 都只对应一款应用。这点是因为苹果没有对 URL Schemes 有不允许重复的硬性要求，所以曾经出现过[有 App 使用支付宝的 URL Schemes 拦截支付帐号和密码的事件](http://jbguide.me/2015/03/26/url-scheme-is-vulnerable/)。
3.  一般网页的 URL 比较好预测，而 iOS 上的 URL Schemes 因为没有统一标准，所以非常难猜，通过猜来获取 iOS 应用的 URL Schemes 是不现实的。

## URL Schemes 的发展

_URL Schemes 的发展过程可以说就是 iOS 效率工具类 App 的发展过程。_

起初的苹果建立的 [Apple URL Schemes](https://developer.apple.com/library/ios/featuredarticles/iPhoneURLScheme_Reference/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007899) 只是用于自用，里面只有邮件、电话、iTunes 搜索、Youtube 视频等一些内置服务的 URL。

个人认为 URL Schemes 第一次大火是在 2011 年末（如有异议欢迎指正），那个时期也是越狱的鼎盛时期，那个时期越狱后大家都会装的一个插件是 SBSettings[[1]](https://sspai.com/post/31500#fn:1 "see footnote")。越狱的人都知道每当新系统发布的时候，等待新系统的越狱发布是最撩人的，而这段时期那些「不越狱就能做到某种越狱功能」的应用经常一时间风头无两。

2011年 iOS 5 发布带来了通知中心，没过多久，出现了一大批使用 iOS 系统设置的 URL Schemes 的 App 神奇地完成了接近 SBSettings 的功能——它们可以让我们从通知中心直接跳转到某些 App 的特定界面，比如 Twitter 的发推界面。它们甚至还可以直接跳转到系统设置里的 Wi-Fi 选项。在这一批 App 中，就有如今效率软件霸主之一 [Launch Center Pro](https://sspai.com/tag/Launch%20Center%20Pro) 的前身——Launch Center。

![](https://cdn.sspai.com/attachment/origin/2015/10/10/286106.png?origin?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

但很快，这一批 App 被苹果火速下架，原因是「对通知中心的误用」。模糊的解释让开发者们摸不到头脑，这种不满一直延续到 [Launcher](https://sspai.com/post/tag/Launcher) 在 iOS 8 之后的下架事件。

总之，在这一批 App 被下架之后，玩票的都离开了，只留下了一个 Launch Center。作者似乎觉得 URL Schemes 大有可为，所以在不触碰红线（当时的红线是一不许动通知中心，二不许调用系统设置的界面）的基础上继续发力，在几个月（2012年7月）之后推出了 Launch Center Pro v1.0。

![](https://cdn.sspai.com/attachment/origin/2015/10/10/286108.jpeg?origin?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

另一个注意到 iOS 上的 URL Schemes 的作用的是 [Drafts](https://sspai.com/tag/drafts/) 的作者 [Greg Pierce](https://twitter.com/agiletortoise/)。不同于 Launch Center Pro，Greg Pierce 打造的是一个以输入文字为主的效率应用，它以一个笔记本的面目示人，所以被媒体称为「Launch Center for text」。

两者大的区别在于先选动作还是先输入。Launch Center Pro 的使用方法是：先打开动作，如果需要输入的话，你可以让它跳出来一个输入框，你来输入，输入完成后跳转到相应应用。Drafts 则是先在笔记本里把东西输入了，然后再选择动作，跳转到相应应用。

好像没什么大不了的嘛……吗？这里至少有两个重要的区别：

1.  Drafts 中输入过的内容会储存在笔记本中以留作备份，而 Launch Center Pro 里的则是动作运行完了就没了。
2.  Drafts 中输入过的内容可以通过 URL Schemes 进行多次使用或一次性发给多个应用或服务，而 Launch Center Pro 只能将输入内容发送到一个服务或应用。即除了剪切版外， Launch Center Pro 没有其它变量的概念。
3.  第三个区别不太重要：Launch Center Pro 里的输入框和 Drafts 的笔记本界面来比较很明显不是一个好的写作环境。

细节上的区别还有很多，两者适用的范围随着各自的发展扩大，因此重合的那部分功能也愈发的不起眼。Launch Center Pro 和 Drafts 从那以后成为效率类应用中的双雄，不断提出更多更灵活使用 iOS 上 URL Schemes 的办法。

比如 Launch Center Pro 提出了 List 的概念，将列表的想法融入到了 URL Schemes 中，列表的每一项可以是简单的字符，又可以是一串新的复杂的 URL。使用列表可以让我们每次的输入变为更轻松的选择，对于那些重复的任务更为高效。

而 Drafts 的作者直接不满 URL Schemes 只能跳出不能跳回的问题，和 [Marco Arment](http://www.marco.org/)、[Justin Williams](https://twitter.com/justin) 等人开发了 x-callback-URL 来做到跳出，并跳回这样的动作。

可以说这两款 App 对 URL Schemes 的推广和使用构思上的贡献是最突出的，现在 URL Schemes 越来越被 iOS 用户和开发者所重视，在我眼里，一款 App 是否完整系统地支持 URL Schemes 已经是判断它是否优秀的标志之一。

故事讲到这里，更重要的还是如何使用 URL Schemes。

_故事里没有提到 [Pythonista](https://itunes.apple.com/cn/app/pythonista/id528579881?ls=1&mt=8)、[Editorial](https://itunes.apple.com/cn/app/editorial/id673907758?mt=8) 跟 [Workflow](https://sspai.com/post/tag/workflow)，绝不是我认为这些 App 不够腕儿，而是它们做的事情重点已经不在于 URL Schemes 了。_

## 基本 URL Schemes

_基本 URL Schemes 的能力虽然简单有限，但使用情境却是最普遍的。_

我所谓的基本 URL Schemes，是指一个 URL 的 Schemes 部分，比如上文提到的微信的 `weixin:`。这个部分的唯一功能，就是打开相应应用，而不能够跳转到任何功能。

绝大多数所谓支持 URL Schemes 的应用，一般都是只有这么一个部分，它一般是这个应用的名称，比如 [OmniFocus](https://sspai.com/post/tag/Omnifocus) 这款应用，它的基本 URL Schemes 就是 `Omnifocus:`。如果应用的主名称是个中文名的话，它的 URL Schemes 也许会是应用名的拼音，比如 [墨客](https://sspai.com/post/tag/%E5%A2%A8%E5%AE%A2) 这款应用，它的基本 URL Schemes 是 `moke:`。

但，我前面提过了网页 URL 和 iOS 应用的 URL 的三个重要区别，其中第三项，就是 iOS 上的 URL Schemes 并不规范，一个应用的 URL 可以是各种各样的：

-   Coursera 的 URL 是：`coursera-mobile:`
-   Duet 这款游戏的 URL 是：`x-kumo-duet:`
-   Monument 这款游戏的 URL 是：`fb690517270143345:`
-   Feedly 的 URL 是：`fb129765800430121:`
-   扇贝新闻的 URL 是：`wx95962d02b9c3e2f7:`

它们目前并没有统一的规则，所以猜测一个应用的意义并不太大，你可以试试，但不要过于指望这种方式。下文会提到[如何查找一个应用的基本 URL Schemes](https://sspai.com/post/31500#09)，只要那个应用支持 URL Schemes 就能找到。

基本 URL Schemes 的能力虽然简单有限，但使用情境却是最普遍的。作为一个使用 Launch Center Pro 代替 Home Screen 的人，这样只能做到打开应用的基本 URL Schemes 对我来说也是很重要的。

## 复杂 URL Schemes

_掌握复杂 URL Schemes 你才算初步有了打造适应自己使用情境的自动化流程的能力。_

iOS 应用的复杂 URL Schemes 就像网站的子页面的链接一样，在首页网址的基础上进行延伸。前面苹果官网和微信对比的例子已经可以说明问题了，想不起来的可以再去回顾一下。

具体来看，复杂 URL Schemes 有两种：一种是直接打开某个应用的某个功能，另一种是打开某个功能后直接填写预设的字符。这同网页网址的原理也是类似的：

比如 Google Image 搜索的网址是：

https://image.google.com

这就是在它的主网址（Google.com）的基础上做了修改的子网页的网址。而如果我们搜索一个词条，网址实际上是：

http://images.google.com/images?q=关键字

iOS 上的 URL Schemes 同样遵循这个规则，比如你要打开 [Fantastical](https://sspai.com/post/tag/Fantastical) 这个应用，这是一个基本 URL Schemes：

Fantastical:

然后你想使用 URL Schemes 打开它的某个功能界面，比如直接打开 Fantastical 添加新事件的界面，那就需要这个界面的 URL Schemes：

fantastical2://parse?sentence

如果你想事先填好事件是什么，定在什么时候进行，只要在原有的 URL 的基础上再加上事件的描述：

fantastical2://parse?sentence=`事件描述`

就成为了一个更加实用的 URL Schemes，因为它不光直接让你进入了某个你需要的功能界面，还直接帮你填好了你需要的内容，而跳转到 Fantastical 以后，你需要的只是按一下完成。

![](https://cdn.sspai.com/attachment/origin/2015/10/10/286109.jpg?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

有了这样的 URL Schemes，应用之间才可以互相地协作。比如说，当我们在 [Mr. Reader](https://sspai.com/tag/Mr.%20Reader) 上看到一篇文章里面写了一个不错的软件的时候，我们可以利用 [OmniFocus](https://sspai.com/post/tag/OmniFocus) 的 URL Schemes 将文章名保存到任务名的部分，把链接保存到备注的部分。在 iOS 8 的 Share Sheet 出现之前，这是唯一在 App 间传输信息的方式。

复杂 URL Schemes 有一个特殊的用例是 `Jumpback`，字典类 App 用它的很多，比如[欧路词典](http://www.eudic.net/)。传统的使用欧陆字典查询单词的 URL Schemes 是：

eudic://dict/`想查的单词`

在这个基础上，加上一句 `Jumpback`：

eudic://dict/想查的单词?jumpback=指定`URL`

就能够做到查完单词以后，按左上角或左下角的返回按钮，回到你想要回到的 App。我们用下面这个 URL Schemes 来详细说明这个用例：

eudic://dict/[clipboard]?jumpback=launch:

这段 URL，做到的是：先复制你不会的单词，然后打开 Launch Center Pro 启动这个动作，跳转到欧陆词典的该单词的释义页面，当你确定了意思以后，按返回按钮，回到 Launch Center Pro。

并不是每个应用都有它的复杂 URL Schemes，但一般来说，有系统规范的复杂 URL Schemes 的应用都是同类应用中的佼佼者。

基本 URL Schemes 我们猜不中，对复杂 URL Schemes 靠猜就更不靠谱了。支持复杂 URL Schemes 的应用，比如上面提到的 [OmniFocus](https://sspai.com/post/tag/OmniFocus)，还有 [Due](https://sspai.com/post/tag/Due)、[Clear](https://sspai.com/post/tag/Clear)、[Launch Center Pro](https://sspai.com/tag/Launch%20Center%20Pro) 等等都会在自己的官网上有专门用来介绍自己的 URL Schemes 的网页，有些还会提供具体的范例，来帮助用户理解和使用自己应用的 URL Schemes。这方面的内容我们在后面的[查找部分](https://sspai.com/post/31500#09)再详述。

## 变形 URL Schemes

_在复杂 URL Schemes 的基础上更上一层楼。_

变形 URL Schemes 是指一些应用利用了 URL Schemes 的规则和 iOS 系统的一些内置功能，来拓充**复杂 URL Schemes**，并使其中需要输入字符或参数的部分可以预设或输入后再跳转，进一步减少步骤。

单纯使用 URL Schemes 是无法利用 iOS 内的一些基本功能的，比如说，输入和剪切板，你用一下 [iLauncher](https://sspai.com/tag/iLauncher) 这类的 App 你就知道，即便是复杂 URL Schemes，在跳转具体功能界面以外也是乏力的，因为你就算知道规则，也没办法每次都灵活地输入和调用剪切板，也就是无法应付任何变量，只能使用死的 URL。

所以有的应用就在 URL Schemes 的基础上，使用了一些方法来调用剪切板或给你一个输入框，做到先输入内容，然后 URL 的相应部分。

我们这里用 Launch Center Pro 来举几个简单的例子：

比如用 OmniFocus 的添加任务的复杂 URL Schemes：

OmniFocus:///add?name=`任务名`&note=`备注`

你看这里有两个变量——`任务名`和`备注`。如果你不能自己每次都做到输入这两个变量，那这条 URL 实际上没有意义，它只是会给你生成一个任务，任务名就叫做「任务名」这三个字，备注里填的就是「备注」这两个字。所以我们需要能够输入任务名和备注的内容，然后填写到 URL 的相应位置。

在 Launch Center Pro 里，输入框表示为`[prompt]`，你只要在变量部分填入这个输入框的表述方式，就会在运行动作时出现输入框让你输入内容，所以我们可以把上面那个 URL 改为：

OmniFocus:///add?name=[prompt]&note=[prompt]

这样在运行这个动作后，会先后出现两个输入框，第一个填进去的就是任务名，第二个填进去的就是备注。这样这个 URL 才对于使用者有了实际使用上的意义。

在 Launch Center Pro 里最后一条复制了的文本内容表示为`[clipboard]`，当你想用[欧陆词典](http://www.eudic.net/)直接搜索你刚才复制好了的不知道意思的单词的时候，就可以在 Launch Center Pro 里添加一个这样的动作：

eudic://dict/[clipboard]

这样每次打开这个动作就会直接跳转到那个单词的解释页面去。

Launch Center Pro 对复杂 URL 贡献比较大的一个思路是使用 `list（列表）`。在 iOS 这样只靠触控屏交互的图形界面上，「选择」比「输入」速度更快也更省事，尤其是对于那些你经常会输入的内容来说，从一个列表里选择它们要比每次都输入它们来得有效。比如说我们在使用 [1Password](https://sspai.com/post/tag/1Password) 的时候，搜索某一些服务（如邮箱、Evernote、Dropbox 等）的频率要明显地比另一些更高，这时候，把我们搜索频率较高的服务列一个列表就比每次都输入它们更有效率，在 Launch Center Pro 中，在 1Password 里建立一个列表的 URL 是这样：

onepassword://search/[list|Google=Google|Dropbox=Dropbox|Weibo=Weibo|输入=[prompt]]

在这里简单说明一下这个 URL 的 List 部分：

[list|Google=Google|Dropbox=Dropbox|微博=Weibo|输入=[prompt]]

首先有一个中括号`[]`，然后括号的最左边是 `list` 和一个分隔符 `|`，这三样元素声明了这是一个列表。然后是 `Google=Google`、`微博=Weibo` 等常用服务，等号左边，是显示在列表上的名称，而右边是填入 URL 的字符。最后一个 `输入=[prompt]`，左边同样是列表上的名称，右边是前面提到的输入框。最后这一部分是列表中没有你想要搜索的项目的时候手动输入用的。

![](https://cdn.sspai.com/attachment/origin/2015/10/10/286110.jpg?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

Launch Center Pro 的用法还有很多，对变形 URL Schemes 也有其它的贡献，包括文中提到的这些说明有些并不完整。除了 Launch Center Pro 以外，Drafts 等应用对变形 URL Schemes 也有自己的贡献，比如把 Drafts 中的一篇笔记的某一行或几行作为 URL 的元素安插在 URL 之中，也就是 `[[line|n]]` 这个 Tag 的用法等。但这篇文章的目的不是让大家完全掌握 Launch Center Pro 和 Drafts，而是全面了解 URL Schemes 的各种用法，所以在这里对这些效率应用的介绍都是点到为止。

## x-callback-URL

_第一次拓展 iOS 的自动化边界的创举，让你可以跳出去再跳回来，真正的可以串联多个步骤。_

回到上一个操作的应用这件事对我们来说不新鲜，Windows 上同时按下 `Alt` + `Tab` 这个快捷键你大概不知道做了多少次了。iOS 9 也加入了这个功能：

![](https://cdn.sspai.com/attachment/origin/2015/10/10/286111.jpg?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

从一个应用的界面跳转到了另一个应用后，就会在左上角看到回到上一个应用的字样，轻触就能返回到上一个应用。这样的事情我们在打造自己的自动化操作的时候毫无疑问也会想要做到，前面说过的 `Jumpback` 是一个选择，除此之外还有更强力的代替者——x-callback-URL，它还有 iOS 9 上「返回上个应用」这一功能不能代替的地方。但是不可否认的是，x-callback-URL 的使用情境比较少，使用难度却又比较高。

有了 x-callback-URL，我们就可以结合 Drafts 和 Fantastical 这样的应用里一次性添加多个事件；我们还可以结合 Due 跟墨客这样的应用做到提醒我们发微博，并直接把微博内容储存好，以便到时候可以一键发出去。

我们前面谈到的 URL Schemes 都只有**一个**目的，不管结果是什么，跳转完成后就会停留在跳转后的应用的界面。但在使用 URL Schemes 的时候，运行结果有时候可能成功（大多时候都成功啦，不然你做它干吗），有时候可能失败（比如你用墨客的 URL 搜索一个不存在的联系人），有时候我们也会手动将其取消（比如本来要添加个任务结果想想还是不添加了）。

如果我们还想让应用根据不同的结果有对应的反应，就要用到 x-callback-URL。比如当上一个 URL Schemes 运行成功以后，我是要回到跳转前的应用？还是要接另一个动作（接上另一段 URL Schemes，打开另一个应用的某个功能）？无论是跳转回上个应用还是打开另一个动作，只要你在运行完一个 URL Schemes 后还想再利用一段新的 URL Schemes 做下一件事，就要靠 x-callback-URL，它的固定语法是：

-   在一个 URL Schemes 后面接`&x-success`，表示前一个 URL 成功以后下一步做什么；
-   在一个 URL Schemes 后面接`&x-error`，表示前一个 URL 失败以后下一步做什么；
-   在一个 URL Schemes 后面接`&x-cancel`，表示取消前一个 URL 的操作结果后下一步做什么；
-   还有一个 `&x-source` 我们遇到了再说。

现在来举刚才提到的例子，x-callback-URL 的例子其实都非常复杂，做好心理准备：

### 用 Drafts 给 Fantastical 一次性添加多个事件

先回顾一下添加一个事件的复杂 URL Schemes：

[Fantastical](https://sspai.com/post/tag/Fantastical) 支持自然语言识别，可以从一句话里提取事件的名称和时间，自动添加到默认日历中，这非常适合使用 URL Schemes 来把任务发送过去，因为你只要输入一句「我什么时候办啥事儿」（事件日期要照顾下英文语法，事件名称可以用中文），它就能帮你添加到默认的日历里：

fantastical2://parse?sentence=去银座换 iPhone on this sunday at 15

你可以把上一个 URL 通过 Launch Center Pro 激活，也可以把空格全都替换成`%20`以后直接填入 Safari 的地址栏：

fantastical2://parse?sentence=去银座换%20iPhone%20on%20this%20sunday%20at%2015

跳转以后 Fantastical 里就会生成一个任务——去银座换 iPhone，时间是本周日下午三点：

![](https://cdn.sspai.com/attachment/origin/2015/10/10/286109.jpg?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

目前为止，实际上用的实际上还都是复杂 URL，具体到 Fantastical 这里，就是只能添加一个事件。但我们有时候并不只是加一个事件。比如，大学生在考试的时候时间不统一，每节课每个老师都会在自己的课上来公布自己这么课的考试时间，那么你可以把这些考试和时间先都记录在 Drafts 里，然后一并同时发到 Fantastical。

![](https://cdn.sspai.com/attachment/origin/2015/10/10/286112.jpg?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

这个过程实际上是把多个发送事件到 Fantastical 的 URL 绑在了一起，做到一个运行成功以后运行下一个，直到运行完，实现这样的 URL 就只有 x-callback-URL 才可以，具体的 URL 可以说很复杂，是这样的：

fantastical2://x-callback-url/parse?sentence=[[line|1]]&add=1&x-success={{drafts4://x-callback-url/runAction?text=[[line|2..]]&allowEmpty=NO&action=Events%20in%20Fantastical-Quick}}&x-cancel={{drafts4://}}

不要被吓到，我们来逐条分析这段 URL 就能轻松读懂它：

-   `fantastical2://x-callback-url/parse?sentence=` 这一句，你会发现比我们刚才用的 `fantastical2://parse?sentence=` 多了一截儿 `x-callback-url/`，原因是，当一个 App 的 URL 里使用了多出来的这一段儿 `x-callback-url/`，就是在声明，「各单位注意，我下面的 URL 要用到 x-callback-URL 了。」
-   紧接着是 `[[line|1]]`，这一段是 Drafts 的变形 URL，意味取文本中第一行的值。在这个动作中，我们看上面的截图，第一行是`微积分考试`那一条，那么就是把微积分这条先发到 Fantastical 里。

接下来我们要做的事是，把剩下几行也自动发到 Fantastical，并且在没有东西的时候自动停止动作。

-   所以我们接着来看下一个小部分`add=1`，这是 Fantastical 的语法，再加一项任务。
-   下一句的 `&x-success=` 就是 x-callback-URL 的标准声明了，即当上一步成功后，下一步做什么。

然后你会看到双层花括号`{{ }}`的出现。在 x-callback-URL 中[[2]](https://sspai.com/post/31500#fn:2 "see footnote")，出现在 `x-success` 这些固定语法之后的双层花括号意味着花括号之中应当是一个完整的动作，这个动作在上一个动作成功/取消/错误后进行。

在这里你可以这样理解：用双层花括号将一段 URL 包起来放到另一段 URL 中是为了不打乱原有的运行顺序。URL 的运行方式就像加减或者乘除这种同级运算，从左到右进行，如果你想给式子里再加一个式子且不把运算顺序和结果搞乱搞错，就要把后来的式子外面套一个括号放进去。

-   然后我们来看花括号内部的第一部分`drafts4://x-callback-url/`，熟悉的 x-callback-URL 声明又来了，就不多解释了~
-   下一个`runAction?`是 Drafts 的运行某个动作的起始声明，你看到一段 URL 里有这句，就代表 Drafts 要运行一个动作了，后面的不远处肯定能找到要运行的动作的名称。
-   接下来的这句`text=[[line|2..]]`并不是动作名称，而是动作的内容。`text=`是 Drafts 里的一个语法，等号后面决定了该动作使用的文本是什么。然后`[[line|2...]]`这句跟我们之前见过的`[[line|1]]`不太一样，如果数字 2 后面没有点点点，就特指的是第一句，但是如果有点点点了，意思就是对下面每行都重复该动作。
-   那么什么时候停呢？空白其实也是内容啊。所以你要告诉这个动作什么时候停，在这里用的是`&allowEmpty=NO`，这一句在 Drafts 的语法中意味：不允许发送空内容。
-   然后下一步的`&action=Events%20in%20Fantastical-Quick`，就承接前面我们提到的伏笔，提出了动作名，动作名是`Events%20in%20Fantastical-Quick`。为什么里面有这么多`%20`？为什么前面 Fantastical 的例子里见到了好多`%20`，而直接用 Launch Center Pro 为什么没有这些 `%20`？这个问题涉及到什么时候要在 URL 中使用编码，什么时候不使用的问题。我们后面会说到它。

按说整段 URL 已经结束了，但是我们看到最后还有一段儿 `&x-cancel={{drafts4://}}`，这里的 `x-cancel` 也是我们提到过的 x-callback-URL 的固定语法，它的意思是，当我们取消这个任务了做什么。然后看等号后面的内容，我们就知道，取消任务以后会回到（实际是打开）Drafts，但什么都不做。

这一整段的 x-callback-URL，如果想正常工作，必须要保存为 Drafts 中的一个动作，动作名要和 URL 中提到的 `Events in Fantastical-Quick` 一致，改的话两个都要改。这是最复杂的 URL Schemes 的一种形式之一：在一个 App （Fantastical）的 URL 中嵌套另一个 App（Drafts） 的 URL，同时 Drafts 的 URL 本身指涉的动作实际上还是不断自指的。

关于 x-callback-URL 这是一个比较有代表性的例子，我们也看到了它固定语法中的 `x-success` 跟 `x-cancel` 是怎么用的，固定语法中的另外两个里，`x-error` 的用法也与前两者类似。只有 `x-source` 还要再说下。

在 x-callback-URL 的四大固定语法中，`x-source` 是个很小众的用法。它一般和 `x-success` 连接，构成 `x-source=选项名&x-success={{URL}}`的格式。显示在 App 中则是在上一个动作完成后（一般是跳转后）给出一个选项，选项内容是你写在 URL 中的选项名和 `取消`，选择选项名后触发 `x-success` 后的 URL 里的动作，取消则停留在当前 App。也就是说，它给了你一个选择，在这一步到底是继续下一个动作还是停留在当前 App。

支持 `x-source` 的 App 不多，在这里用 Due 的 URL Schemes 来举个例子（无关部分已用省略号省略）：

due://......&x-source=墨客&x-success={{moke:}}

这段 URL 运行完，会出现的结果是跳转到 Due，执行省略号中的动作，动作执行完后，会出现这样一个菜单：

![](https://cdn.sspai.com/attachment/origin/2015/10/10/286114.jpg?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

如果选择墨客，就会跳转到墨客。如果选择取消，就会停留在 Due。

和其它类型的 URL Schemes 一样，x-callback-URL 的格式也并非完全统一。我们前面已经知道，一个应用在使用 x-callback-URL 的时候要先通过 `x-callback-url/` 声明，比如 Launch Center Pro 在用到 x-callback-URL 的时候要这样开始：

launch://x-callback-url/

但有的 App 会连自己其它部分的 URL 也修改了，比如 Instapaper 的是：

x-callback-instapaper://x-callback-url/add?…

所以想正确使用 x-callback-URL，还是要查看相应 App 的文档。

## URL 编码（Encode）

_编码还是不编码，这问题很容易。_

完全不知道 URL Schemes 的人对 URL 的编码和解码可能有些陌生，但是你一旦入门，你很快就会碰上一些问题，这些问题很有可能是该编码的部分没编码导致的。

比如玩效率 App 的入门人群最喜欢的一个 URL 大概就是百度搜索关键字的 URL：

http://www.baidu.com/s?wd=

等号后面可以用剪切板内容代替，或者输入个什么，然后就能直接在百度搜索关键字。但用 Workflow 做个动作以后，发现这 URL 不灵了，输入中文就跳转总失败，怎么回事儿？

还有上面的 Fantastical 的例子，那一片`%20`是啥？为什么有的时候要有时候不要？

这些都涉及 URL 什么时候要编码什么时候不需要的问题，而这问题并不难解决。

### 什么时候要编码？

URL 中的字符可以分为两类[[3]](https://sspai.com/post/31500#fn:3 "see footnote")，一部分可以在链接中正常显示，比如字母、数字还有`/`等一部分符号。除此之外，全部不能正常显示，需要进行编码才能够作为 URL 的一部分出现。比如空格，在 URL 中就必须表示为 `%20`转换的规则不用深究，网上有很多工具（比如 [URL 解码工具](http://tool.chinaz.com/Tools/URLEncode.aspx)）提供 URL 的编码和解码功能，可以把编码过的乱七八糟的 URL 解码为我们看得清爽的字符：

`Hi%2C+%E6%88%91%E6%98%AF+%40JailbreakHum` 转换为 `Hi, 我是 @JailbreakHum`

这些工具当然也可以反过来把我们常用的字符转换成可以在 URL 中使用的字符。

所以理论上，所有 URL 不支持的字符，都要编码。编码的任务也就是这么简单，把 URL 不支持的字符换位它支持的字符。既然如此，为什么有的时候不用编码？

### 为什么有的 App 不需要编码？

因为那些不用编码的时候，是 App 私下替你编了。就像在 [Workflow](https://sspai.com/post/tag/Workflow) 里，在 URL 下面接了一步 `URL Encode` 一样。这样一来，不管你在前面的输入框中输的内容是什么，URL 支持不支持，它都会试图给你编码。URL 支持的内容就忽略，不支持的就编码，然后再进行下一步。这样一来，省了你手动再编一次的麻烦。

实际上现在使用到 URL Schemes 的大部分 App，比如 Launch Center Pro 和 Drafts，都做到了自动编码。前面也提到了，Workflow 中也有一个名为 `URL Encode` 的动作是专门用来编码 URL 的。

那么，啥时候用我们手动编码呢？答案是：你把 URL 直接放到浏览器的地址栏的时候。

URL Schemes 都可以直接放到 Safari 的地址框里触发，因为 URL 就是地址/链接，而地址栏就是放链接的地方嘛。所以地址栏的 URL 就要严格遵守 URL 的规则，它看不懂了就不跟你玩了。除此之外，有一部分效率 App 也不会自动编码，如果你发现哪个动作在 Launch Center Pro 里跑的特别顺畅，到其它 App 就卡壳儿的话，你就先把输入内容编下码，应该就能解决问题了。

## 如何查找以上各类 URL

前面介绍了基本、复杂、变形、x-callback-URL 这几种形式的 URL Schemes，几乎在每一部分都留下了一个问题——「去哪找这些 URL Schemes」？

其中，基本 URL Schemes 是可以由你自己手动查询的，**所有支持基本 URL Schemes 的 App 都可以用以下方法查到其基本 URL Schemes**。而其它几种 URL Schemes 因为是写进代码中的，需要查询各 App 的文档，来参照例子根据自己的需求制作 URL。

### 查找基本 URL Schemes

_越狱和不越狱本质上用的是同一种办法，只是越狱以后可以直接从 iOS 查看 URL。_

基本 URL Schemes 的查找方法可以通过 App 中的 `info.plist` 来查询，分为越狱和不越狱的方法，二者原理一样：

**未越狱方法**

不越狱的话，就无法查看 App 包内的内容，所以需要借助电脑。

首先，在 iTunes 找到你想用 URL 打开的 App，右键选择在文件夹中显示：

![](https://cdn.sspai.com/attachment/origin/2015/10/10/286115.jpg?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

然后把这个文件复制到桌面上解压（或者其它地方，总之不要直接在原文件夹解压）：

![](https://cdn.sspai.com/attachment/origin/2015/10/10/286116.jpg?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

解压完毕后，在解压出的文件夹中，找到 `.app` 文件：

![](https://cdn.sspai.com/attachment/origin/2015/10/10/286117.png?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

然后选择显示包内容：

![](https://cdn.sspai.com/attachment/origin/2015/10/10/286118.jpg?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

找到 `info.plist` 这个文件，用你电脑里能打开它的 App 打开它（Mac 上用 [TextWrangler](https://itunes.apple.com/cn/app/textwrangler/id404010395?mt=12) 就好）。

![](https://cdn.sspai.com/attachment/origin/2015/10/10/286119.jpg?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

然后查找 `URLSchemes`：

![](https://cdn.sspai.com/attachment/origin/2015/10/10/286120.jpg?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

在 `CFBundleURLSchemes` 下的那两行就是该 App 的基本 URL Schemes 了。

**需越狱方法**

如果越狱后，可以用 iFile 或 Filza File Manager 这样的文件管理软件，进入路径：

```
/var/containers/Bundle/Application
```

找到你想要用 URL Schemes 打开的 App，进入下一级文件夹，搜索 `info.plist`：

![](https://cdn.sspai.com/attachment/origin/2015/10/10/286121.jpg?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

最后用文本编辑器打开 `info.plist`，在其中搜索 `URLSchemes` 即可：

![](https://cdn.sspai.com/attachment/origin/2015/10/10/286122.jpg?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

本质上，如前文所说，两者是一种方法，区别仅是越狱后查询的灵活度变高，你随时可以看看自己新装的 App 的 URL Schemes 是啥。如果你像我一样基本使用 Launch Center Pro 代替主屏的话，这种灵活性还是需要的。

### 复杂 / 变形 / x-callback-URL

_若想全知全能，唯有查询文档。_

复杂 / 变形 / x-callback-URL 这三种类型的 URL Schemes 是写入代码中的，无法通过查询 .plist 文件来获取。但支持这三种 URL Schemes 的 App 的开发者将这些功能加入到自己 App 中一般是希望用户使用的，所以针对那些希望用户使用的功能都会专门写文档来告诉读者如何使用它们。

如果你想搜索任何一个 App 的复杂 / 变形 / x-callback-URL，你只要搜 `App 名 URL Schemes`，一般就能找到该 App 的 URL Schemes 文档页面。同时，直接去这些 App 的官网查找相关网页也可以。

网上会推荐一些库，看起来很方便，你可以一搜就能找到某个 App 支持的 URL Schemes。但实际上，它们没那么好用，因为你想，这些库，跟网上那些列表一样，都是个人自发做的，所以覆盖面未必够，时效性也肯定不如开发者的文档高，毕竟做库和列表的这些人也得看了开发者的文档才能添加到自己的库或列表里。

但是，如果你用 Launch Center Pro 的话，我倒是推荐你在想找一个 App 的 URL Schemes 的时候先看下 Launch Center Pro。Launch Center Pro 会匹配你的 App，然后直接显示出该 App 可使用的 URL。而且在动作生成的最后一步，你只需要考虑你这个动作要输入的是普通文本还是纯数字（比如填日期时间等就只需要纯数字），根据你的内容选择普通键盘或数字键盘。也就是说，通过 Launch Center Pro 生成的动作是几乎不用考虑语法的。仅凭 Launch Center Pro 可以解决大部分的 URL Schemes 制作问题，反过来，你也可以根据 Launch Center Pro 生成的动作去理解 URL Schemes。

不过因为 Launch Center Pro 的库也是人做的，它也不是全能的，也有覆盖不全和时效性的问题。所以想完全打造符合你自己使用情境的一套 URL Schemes，还是要手动查文档。

但仅靠扒别人的动作是无法根据自己的情境为自己量身定做一套自动化的动作的，要学会靠自己，查文档。

## URL Schemes 的衰败

_苹果的各项改进一点点蚕蚀了 URL Schemes 的领域，但目前宣告 URL Schemes 死刑还为时尚早。_

6s 之后的设备大概都会支持 3D Touch，它的特征之一就是从 Homescreen 的 App 图标上直接进入该 App 的具体某个功能了。这个功能也让很多人兴奋了一把，虽说会用 URL Schemes 的人早就做到类似的事了。不过，既然官方已经有了这样的功能，为什么还要用 URL Schemes？

同样，在 iOS 9 中，我们还可以用 Siri 建立关于 App 的提醒事项，来做到以前只有用 Launch Center Pro 和 Due 这样的 App 才能做到的定时打开 App。而且 iPhone 6s 还可以做到不在充电状态下使用 _Hi, Siri_ 这样我们要建立一个提醒事项或者闹铃也无比简单，只要说一声「Hi, Siri. 半小时以后叫我。」就能定一个计时器。在这种比较之下 [Due](https://sspai.com/post/tag/Due) 这样的 App 的作用显然是被大大地削弱了。除此之外还有通知中心部件，Sharesheet 的出现都在一定程度上代替了 URL Schemes 的作用，削弱了其价值。 但按照目前的状态，充其量只能说 URL Schemes 在衰败，还远不能宣判其死刑。

3D Touch 和 URL Schemes 重复的地方只有一部分复杂 URL Schemes 的功能：一些复杂 URL Schemes 的功能 3D Touch 没有涵盖，反过来 3D Touch 也有一些可以做到的事通过复杂 URL Schemes 做不到。但在复杂 URL Schemes 之上的变形 URL Schemes 跟 x-callback-URL 都是 3D Touch 无法做到的。

Siri 确实非常好用，我每天都用它很多次。所以我知道，如果不戴耳机，它是通过扬声器跟你交流的，这种时候它听错了你说错了，都得来回矫情半天，周围有人的话场面会变得很尴尬。所以很多场合，通过 Due 的 URL Schemes，直接从 Dock 中的 Launch Center Pro 里找到一个 Timer 或添加一个提醒其实更舒服。

我承认 URL Schemes 如今已无往日辉煌，但它在 iOS 上的效率方面的作用能不能被完全替代，目前也未可知。

## 结语

_用原生 iOS 的人分两种，懂 URL Schemes 的和不懂的。前者是魔法师，后者是麻瓜。_

URL Schemes 目前仍是使用 iOS 设备提高效率的必要工具。效率有两件核心：减少时间浪费和在工作的时间集中注意力。通过 URL Schemes 完成的自动化动作同时做到了这两点：它减少操作步骤，从而减少时间浪费；避免在桌面和 App 内的层层寻找，直达功能，从而减少了干扰。

我最后想以一个故事结尾：

我有个朋友，他有节课，老师讲的快，板书来不及记，他就拍下来，下课抄下来整理。我有一次见他誊板书，发现他隔一会儿就碰一下屏幕。我问他你这是做什么，他回答说因为屏幕一会就会黑下来然后锁屏，碰屏幕一下就能再亮一会。我当场吐血，在设置里教他把自动锁屏的时间设为了「永不」。

他好像有点可笑，为什么，因为自带的这么简单的功能他竟然不知道！非要用手一下一下地碰来让设备保持解锁状态。那么，反过来想想自己。有的 App，你几乎每次用都是用它的那个功能那个界面，但你每次都是从主屏幕找到它，再点进去，再在一层一层的功能里选中它。这样的你，是不是在哪里跟我那位朋友有点儿像？

---

### 鸣谢

为了保证这样的文章的正确性和可读性，我在个别部分的写作过程中咨询了他人的意见，并在文章基本结束后请了各层次的人来阅读，下面是对这些人的感谢：

感谢 [@gviridis](http://weibo.com/n/gviridis) 对沙盒机制部分的意见；感谢 [墨客](https://sspai.com/post/tag/%E5%A2%A8%E5%AE%A2) 作者 [@an00na](http://weibo.com/an00na) 对我在 -xcallback-URL 的查找方面的问题的解答；感谢 [@三块五毛](http://weibo.com/steyuanxing) 和 [@文刀漢三](http://weibo.com/wendaohansan) 抽出时间阅读如此长的文章并提出合适的建议。

---

1.  最实用的功能是可以设定一个手势，通过该手势呼出一个界面，这个界面上有许多的系统开关，比如 Wi-Fi、VPN 等。  [↩](https://sspai.com/post/31500#fnref:1 "return to article")
    
2.  花括号在 Drafts 中的另一作用为编码。  [↩](https://sspai.com/post/31500#fnref:2 "return to article")
    
3.  喜欢术语解释的可以看 [Wikipedia](https://zh.m.wikipedia.org/zh/%E7%99%BE%E5%88%86%E5%8F%B7%E7%BC%96%E7%A0%81)。  [↩](https://sspai.com/post/31500#fnref:3 "return to article")