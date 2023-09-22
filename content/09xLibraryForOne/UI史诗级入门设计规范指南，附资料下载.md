![动图封面](https://pic3.zhimg.com/v2-43936ef7ef5b846c063538fe266ddc4e_b.jpg)

来源：蜗牛和笔

很多UI小白在一开始学习的时候，不懂的这个控件叫什么，那个字体用多大，适配是什么切图有时什么等等一系列令人头疼的问题摆在面前，犹如来路虎，今天给大家推出入门级设计规范，帮助大家快速入门学习，因此比较基础，而做为一个专业UI设计师的我们，在前行的脚步中也应该温故知新，就让我跟大家一起来对iOS、Android的设计规范、适配问题做一次全面的梳理和复习吧。

  

## iOS设计规范

![](https://pic4.zhimg.com/80/v2-c9a36a15e774fe083245da17820d5a6f_1440w.webp)

苹果自07年1月9日正式发布iPhone到目前为止的iPhone11Pro Max，已经历了十三代产品。19年9月11日推出的11、11Pro、11Pro Max并没有新增尺寸，所以对设计师而言也就没有额外新增工作量了，还是按照以前的做法：750*1334px（@2x）或（375*667pt，@1x）做设计稿，再提供@2x、@3x切图。  

以下为苹果手机历代产品明细（话说你拥有过那几代产品，欢迎留言交流）  

一代：iPhone

二代：iPhone3G

三代：iPhone3GS

四代：iPhone 4

五代：iPhone 4s

六代：iPhone 5

七代：iPhone 5s、iPhone 5c

八代：iPhone6、iPhone6 Plus

九代：iPhone 6s、iPhone 6s Plus

十代：iPhone7、iPhone7 Plus

十一代：iPhone8、iPhone8 Plus、iPhone X

十二代：iPhone XS、iPhone XS Max、iPhone XR

十三代：iPhone11、iPhone11Pro、iPhone11Pro Max

  

如何有效记住iOS设计规范，这里我总结了一个方法“iOS五点两图记忆法”，也就是**五个点+两张图**。

  

1、设计尺寸：375x667pt @1x（750x1334px @2x）为基准设计。

2、设计工具：Sketch、Adobe XD、Photoshop

3、预览效果：Sketch Mirror、Adobe XD或Ps Play

4、切图输出：@2x @3x两套

5、标注工具：蓝湖，摹客

![](https://pic2.zhimg.com/80/v2-38c1345bdd44dbc9a09d92e82340e6b5_1440w.webp)

![](https://pic3.zhimg.com/80/v2-4bbbde202f241f353b982cc614d9594e_1440w.webp)

**考考你：**

1、iPhone8尺寸的设计稿如何快速变成iPhoneX的设计稿？

2、@2倍图被当作@3倍进行开发，会导致什么样的后果？

3、为什么要用375x667pt @1倍图进行设计？（后文也有详细答案哦）

4、iPhone8显示为34px的文字在iPhone11 pro Max里面是不是也是34px？

  

在解释上面问题时，这里我们首先重点理解下**PX**和**PT**这两个单位， 弄清楚为什么建议使用一倍图进行UI设计，才能在设计中以不变应万变。（说明：该部分内容优化自静电老师的总结）

PX大家可能比较熟悉，就是像素，英文pixel的简称。最通俗的理解就是找一个放大镜（不是电脑中的放大镜，是真实的放大镜），然后对准自己面前的显示器或者手机屏幕观看，大部分显示器会在放大镜下出现一个个点。这就是我们平时所说的像素概念。在一台物理分辨率为1080x1920px的显示器中，横向分布1920个点，纵向则有1080个点。这些点通过显示器的光学特性，为我们组成不同的图像。

  

![](https://pic2.zhimg.com/80/v2-645ee3ce4849cc250783e6342f3821fd_1440w.webp)

  

请注意， 在不同尺寸的显示器上，这些点的单位面积并不是一样的。比如一台22英寸的1080p液晶显示器与一台27英寸的1080p液晶显示器，可以发现这两台显示器的像素分布就是27英寸的显示效果明显逊于22英寸显示器的效果，一个重要的原因就是两台液晶面板中的“像素”颗粒大小不一。

  

由此可见，像素这个单位是一个相对单位，不能用厘米、毫米等这些绝对度量单位来衡量他的长度或者宽度，因为1像素只代表一个单位的“点”。

  

另一个重要单位是PT，英文point的简称，这个单位也是iOS开发过程中使用的单位，与px这样的相对单位不同，PT（Point）是一个绝对单位，中文名字是“磅因（或者磅）”（1PT=1/72英寸）。

  

同样用简单直观的例子来演示，拿两台不同型号的iPhone，比如一台ip11和一台ip11pro Max，打开同样一款应用（如QQ音乐），准备好一把尺子，使用尺子分别测量最上方title“音乐馆”文字尺寸。经测量，可以发现不同型号的“音乐馆”文字的尺寸都一样。也可以请iOS开发人员分别写两个针对不同尺寸机型适配的同一个文件，并在两部手机安装，确保这个文件中的字体使用一个字号（30PT）。在两个手机中运行并用尺子测量，我们发现他们的物理尺寸完全一样。

  

![](https://pic1.zhimg.com/80/v2-1de9b1d14bceecc588da860337fd2cbc_1440w.webp)

  

请大家记住一点，**px是相对单位，pt为绝对单位**（类似单位为厘米，毫米等等）。在不确定屏幕密度的情况下，px与pt没有任何可比性。

  

在开发工程师眼中，你如果使用750px的分辨率作图，那么按原大小标注设计稿中的尺寸的话，他们同样在开发环境中是要换算为一倍尺寸的，比如你标注了字号为40px，那么最终开发工程师写在代码里的就是20pt，是除以2的关系。但是呢，如果使用一倍基准分辨率作图，那么就不用除以2啦，所有尺寸开发工程师直接拿过去随取随用。

  

![](https://pic2.zhimg.com/80/v2-301031cee37ba37fe8f8782447526dd9_1440w.webp)

  

现今Sketch、XD、Figma作为纯矢量的移动端ui设计软件，不管是设计还是后期与开发工程师的配合，都严格遵从开发原理，这种设计方法可以最大限度保证设计稿的复现，同时也可以减小文件体积和系统资源消耗，不管是从哪个方面看，都是设计师制作ui界面的明智之选。

  

最后总结一下原因，设计师使用一倍基准尺寸作图，主要是单位转换方便，输出切图方便，理解简单。对于工程师，他们不用再进行复杂的换算，有助于完美复现设计稿。

  

## **一、引导页**

引导页是一张完整图，不能适配，因此需要单独出设计图，**iOS共需提供6套尺寸**，当然也支持视频形式。（目前5以下的适配基本淘汰）

![](https://pic4.zhimg.com/80/v2-4ac201135245e59583a991dd7e498f8b_1440w.webp)

  

## **二、图标**

APP应用图标设计以1024x1024px尺寸进行图标创作即可。再通过现成尺寸模版资源，一键生成整套尺寸导出即可。（模版链接：[https://developer.apple.com/design/resources/Template-AppIcons-iOS](https://link.zhihu.com/?target=https%3A//developer.apple.com/design/resources/Template-AppIcons-iOS)）  

注意：最终提交给到程序员的切图是直角，非圆角图标，他就像相框一样往进套无需切圆角！

![](https://pic4.zhimg.com/80/v2-aa153a673745f59ad18fa95a304041f3_1440w.webp)

![](https://pic2.zhimg.com/80/v2-826af0a1ccb46fba0ff6fd989de83e75_1440w.webp)

  

设备名称

应用图标

App Store图标

Spotlight图标

设置图标

iPhone11P, 11P Max, X, Xs, 8P , 7P , 6s P , 6P

180 x 180 px

1024 x 1024 px

120 x 120 px

87 x 87 px

iPhone11, XR, 8, 7, 6s, 6, SE，5s, 5c, 5,4s, 4

120 x 120 px

1024 x 1024 px

80 x 80 px

58 x 58 px

iPhone 1, 3G, 3GS

57 x 57 px

1024 x 1024 px

29 x 29 px

29 x 29 px

iPad Pro 12.9, 10.5

167 x 167 px

1024 x 1024 px

80 x 80 px

58 x 58 px

iPad Air 1 & 2, Mini 2 & 4,3 & 4

152 x 152 px

1024 x 1024 px

80 x 80 px

58 x 58 px

iPad 1, 2, Mini 1

76 x 76 px px

1024 x 1024 px

40 x 40 px

29 x 29 px

其他设备图标尺寸

  

  

**三、状态栏和导航栏**

**状态栏：**显示时间、运营商信息、电池电量等信息区域。(齐刘海区域)

![](https://pic3.zhimg.com/80/v2-5d3d7427dc82c7ccf04aa96ba0f8423e_1440w.webp)

  

  

**导航栏：**状态栏下面的区域，含页面标题、功能图标等信息区域。

![](https://pic4.zhimg.com/80/v2-a7d5643293b0f036604a926594c77f43_1440w.webp)

  

状态栏跟导航栏一般会进行一体化设计。现在流行大标题导航栏设计，也就是加大导航栏的高度，融入页面内容的标题，当内容上滑时，大标题再回归到常规导航高度。

![](https://pic4.zhimg.com/80/v2-c2947139aa84c0564c954dccf89078d3_1440w.webp)

  

（大标题导航栏的高度一般为116pt（232px），这里包括了20pt（40px）状态栏的高度，同时也能放得下34pt（68px）的大标题和辅助信息（如返回等图标）。  

![](https://pic2.zhimg.com/80/v2-deef649eb140a5d511f1fd4315ec6a05_1440w.webp)

![](https://pic1.zhimg.com/80/v2-b1cbe0c074f5459ccec0ef613235eac0_1440w.webp)

  

导航栏中的元素必须遵守如下几个对齐原则:

1、返回按钮必须在左边对齐。

2、当前界面的标题必须在导航栏正中。（现在也有左对齐）

3、其他控制按钮必须在右边对齐。

  

## **四、标签栏**

**标签栏：**即Tab栏，为底部快速入口，iOS规范中Tab栏一般有**五个、四个、三个**图标的形式，一般不超过五个。分为“**纯图标标签**”和“**图标加文字标签**”及“**文字标签**”三种形式，高度98px(二倍图)最小文字20px,图标大小60px。

![](https://pic1.zhimg.com/80/v2-384e9538bb62de3285b32d8a70c1e19c_1440w.webp)

![](https://pic4.zhimg.com/80/v2-f68ac12cf4a0860fa8cb29b5cd95934b_1440w.webp)

  

  

**五、iTunes 上传页面**

在程序上传App Store时我们需要提供多张App截图，供用户了解APP的功能。这里我们需要提供**1242 x 2688px**和**1125 x 2436px**两套截图，同时也支持视频形式。（微信目前采用的是五张静态页面形式）

![](https://pic4.zhimg.com/80/v2-d696c191d4372bc7abecf5795998a29f_1440w.webp)

微信iTunes上传用截图

  

  

**六、 字体**

中文字体：PingFang SC，英文字体：SF UI Text 、SF UI Display，其中SF UI Text适用与小于19pt的文字，SF UI Display适用于大于20pt的文字。一些只有安卓端的需要用到思源黑体进行设计哦，其他字体大小和字重可参考iOS。

苹方字体链接：[http://navo.top/yEFNBb](https://link.zhihu.com/?target=http%3A//navo.top/yEFNBb)

提取码：uvlp

  

注意：以下字号pt单位是适用@1x倍图，10pt（20px）是手机上显示的最小字体，最大的应该是目前的大标题字体了，达到了34pt（68px）。

元素

字重

字号(pt)

行距

字间距

大标题

Regular

34pt

41pt

11pt

标题1

Regular

28pt

34pt

13pt

标题2

Regular

22pt

28pt

16pt

标题3

Regular

20pt

24pt

19pt

头条

Semi-Bold

17pt

22pt

-24pt

正文

Regular

17pt

22pt

-24pt

标注

Regular

16pt

21pt

-20pt

副标题

Regular

15pt

20pt

-16pt

注释

Regular

13pt

18pt

-6pt

注释1

Regular

12pt

16pt

0pt

注释2

Regular

11pt

13pt

6pt

  

  

**七、色彩**

在iPhone上显示的色域要比我们作图时的RGB色域要广。所以在iPhone上设计怎样的颜色都可以，只要符合产品气质并且在色彩心理学理论范围内。官方建议的系统色彩如下：

![](https://pic4.zhimg.com/80/v2-dfeb63ac27a2172b5b1829f02200923f_1440w.webp)

iPhone的系统色

  

  

**八、控件**

控件包括：**输入框、按钮、滑杆、页卡、开关**等，在设计模板中已经全部列出。

下载地址：[http://navo.top/YrYfQb](https://link.zhihu.com/?target=http%3A//navo.top/YrYfQb)

![](https://pic2.zhimg.com/80/v2-627b4c96094d2c0b212231b3b15561b1_1440w.webp)

  

为了让设计更符合整体产品品牌调性，这些控件可以做二次设计。

  

但得注意两件事：第一，点击区域基本符合44pt（88px）原则，也就是在手机上大小大概是7mm-9mm，适合手指点击。第二，要设计操作的不同状态，不要只设计一种状态。

  

**控件中无处不在的44pt（88px）**

之前我们介绍过，人手指点击区域为7mm - 9mm，在@2x中就是44pt（88px）。苹果的导航条、列表、工具栏都充满了44pt（88px）这个神秘数字。我们在设计时一定也要考虑到手指的点击区域。  

![](https://pic3.zhimg.com/80/v2-6a14a7128587626c589b33116590193a_1440w.webp)

无处不见的44pt（88px）

  

  

**九、界面设计原则**

  

**1.边距和间距（@2x）**

在移动端页面的设计中，页面中元素的边距和间距的设计规范是非常重要的，一个页面是否美观、简洁、通透和边距、间距的设计规范紧密相连。

  

**全局边距（iOS13，@2x）**  

全局边距是指页面内容到屏幕边缘的距离，整个应用的界面都应该以此来进行规范，以达到页面整体视觉效果的统一。在实际应用中应该根据不同的产品气质采用不同的边距，让边距成为界面的一种设计语言，全局边距的设置可以更好的引导用户竖向向下阅读。还有一种是不留边距，通常被应用在卡片式布局中图片通栏显示，这种图片通栏显示的设置方式，更容易让用户将注意力集中到每个图文的内容本身。

![](https://pic1.zhimg.com/80/v2-38c049e6c0282d6f01d94608fc050a20_1440w.webp)

![](https://pic3.zhimg.com/80/v2-bc80bd43363ad16d5a63ba991fd37e1a_1440w.webp)

  

iOS原生态页面“设置”和“通用”页面的边距都是40px。（@2x）

  

![](https://pic4.zhimg.com/80/v2-63aae62b8a263eb12a9db5035c9f5703_1440w.webp)

![](https://pic3.zhimg.com/80/v2-23796a4554686c41f37297efd1ba5d96_1440w.webp)

微信和支付宝的边距都是32px。（@2x）

  

  

**卡片间距**

在移动端页面设计中卡片式布局是非常常见的布局方式，至于卡片和卡片之间的距离的设置需要根据界面的风格以及卡片承载信息的多少来界定，通常最小不低于16px，过小的间距会造成用户紧张情绪，使用最多的间距是20px、24px、30px、40px，当然间距也不宜过大，过大的间距会使界面变得松散，间距的颜色设置可以与分割线一致，也可以更浅一些。

  

![](https://pic2.zhimg.com/80/v2-29bf24993ae29c9b478e2fe758ed49e1_1440w.webp)

  

以iOS（750*1334px）为例，设置页面卡片间距为70px，而通知中心承载了大量的信息，因此采用了较小的16px作为卡片的间距。

  

![](https://pic3.zhimg.com/80/v2-2dfa2862a216785d33228a6ecf463652_1440w.webp)

  

![](https://pic2.zhimg.com/80/v2-1f586d40859bd4fa2ba2574452eefe89_1440w.webp)

卡片间距的设置是灵活多变的，一定要根据产品的气质和实际需求去设置，平时也可以多截图测量一下各类APP的卡片间距都是怎么设置的，看的多了并融会贯通，卡片间距设置自然会更加合理，更加得心应手。

  

**内容间距**

一款APP除了各种栏（状态栏、导航栏、标签栏、工具栏）和控件icon，就是内容了，内容的布局形式多种多样，这里不去探讨内容具体应该如何去布局，我们来说一说内容的间距设置问题。

![](https://pic3.zhimg.com/80/v2-a44712b59f0fd354306aab33dcf4837a_1440w.webp)

  

**格式塔邻近性原则：**

单个元素之间的相对距离会影响我们的感知，互相靠近的元素看起来属于一组，而那些距离较远的则自动划分组外。来看下图，左图中的圆在水平方向比垂直距离近，那么，我们看到了4排圆点，而右图则看成4列。

![](https://pic1.zhimg.com/80/v2-343672b3278971611adf2f809b60b9b8_1440w.webp)

  

在UI设计中内容布局时，一定要重视邻近性原则的运用

  

**2.内容布局**

在APP的设计中内容的布局形式多种多样，这里介绍最常用的两种布局形式，列表式布局和卡片式布局。

  

**列表式布局**

列表式布局方式非常普遍，随便打开一个APP，基本都存在这种布局方式。特点在于能够在较小的屏幕中显示多条信息，用户通过上下滑动的手势能获得大量的信息反馈。这也是一种非常容易理解的展示形式。

![](https://pic3.zhimg.com/80/v2-19deef6fa6fad9477b9bf7e187b6f22e_1440w.webp)

  

## **卡片式布局**

这种布局形式相对灵活。其特点在于每张卡片的内容和形式相互独立，互不干扰，所以可以在同一个页面中出现不同的卡片承载不同的内容。卡片式布局相对时尚、前卫，很多to C产品经常用到。另外，双栏卡片的布局形式，也常见于以图片信息为主导的App，例如一些商城的商品陈列页面。这种形式能在一屏里显示更多的内容（至少4张），同时，由于分开左右两栏的显示，用户可以更加方便地对比左右两栏卡片的内容。

![](https://pic4.zhimg.com/80/v2-04df65a9e096056b27effd19ea5226b7_1440w.webp)

  

  

## **3.界面图片设计比例**

在UI设计中，对于图片的尺寸和比例没有严格的规范，设计师往往凭借经验和感觉设置一个看起来不错的尺寸，但事实上我们是有章可循的。运用科学的手段设置图片的尺寸，可以获得最优的方案，常见的图片尺寸有16:9、4:3、3:2、1:1和1:0.618（黄金比例）等。

![](https://pic1.zhimg.com/80/v2-2cb14f9533fb520031fdc122caf4d6a0_1440w.webp)

  

## **4.APP版式设计规范**

版式设计又叫做版面编辑，即在有限的版面空间里，将版面的构成要素（文字、图片、控件）根据特定的内容进行组合排列。一个优秀的排版要考虑到用户的阅读习惯和设计美感，在UI设计中版面设计的基础原则有哪些呢？

  

## **对齐**

对齐是贯穿版式设计最基础，最重要的原则之一，它能建立起一种整齐规矩的外观，带给用户有序一致的浏览体验。

![](https://pic4.zhimg.com/80/v2-ed86952eae40028349a9ad80d4ddefbb_1440w.webp)

  

  

## **对称**

对称是对立统一规律的本质属性，呈现出一种和谐自然的美，在应用界面的设计中，引导页设计、注册登录输入框和按钮等无一不是对称的设计。

![动图](https://pic4.zhimg.com/v2-b2ba1efff90c99d8a9a3d3f5da088247_b.webp)

  

## **分组**

物以类聚，人以群分。分组是将同类别的信息组合在一起，直观的呈现在用户面前，这样的设计能够减少用户的认知负担，在移动端界面的设计中最常见的分组方式就是卡片，为用户选择提供专注而又明确的浏览体验。

![动图封面](https://pic3.zhimg.com/v2-13c18c494503d51098bee308ff23c1b2_b.jpg)

  

  

## **十、切图命名规范**

  

切图最后需要命名成规范格式，方便程序员查找。切图命名的格式建议全英文，如果大家英文不好需要想办法提升一点简单的词汇量。借由上述工具切图后，需要整理切图命名，或在切图之前对图层命名亦可。以下是切图元素的中英文对照：

![](https://pic1.zhimg.com/80/v2-83a3a24269d67d622496a52514faa5dc_1440w.webp)

切图命名对照表

  

然后我们要按照”功能_类型_名称_状态@倍数”来命名每个切图，比如我们导航条上有一个搜索图标，那么它的名称就是：

navi_icon_search_default@2x.png

(导航_图标_搜索_正常@2x.png)

  

  

## **Android设计规范**

接下来，再一起来看看Android设计规范，这里只是把安卓规范中一些关键信息做了汇总，更详细的不过多赘述，网上已经有很多大佬产出过此类文章，大家可自行搜索。

  

### **一、安卓开发单位是DP、SP**

  

DP：安卓专用长度单位。

以160 DPI屏幕为标注，则1DP=1PX

计算公式：dp x dpi/160=px

例：以720x1280px （320dpi）为例， 1dp x 320 dpi/160=2px

  

SP：安卓专用字体单位。

以160 DPI屏幕为标注，则1SP=1PX

计算公式：sp x dpi/160=px

例：以720x1280px （320dpi）为例， 1sp x 320 dpi/160=2px

  

  

## **二、安卓设计尺寸：**

以1080x1920px作为设计稿标准尺寸

  

1.从中间尺寸向上、下适配，界面调整幅度最小，最方便适配。

2.大屏幕时代依然以小尺寸作为设计尺寸，会限制设计师的设计视角。

3.用主流尺寸来做设计稿尺寸，极大的提高了视觉还原和其他机型适配。

![](https://pic4.zhimg.com/80/v2-4d8f55673275b0179d3a7e236e028c6b_1440w.webp)

  

  

## **三、安卓图标尺寸**

![](https://pic2.zhimg.com/80/v2-86feecdb567213c76ce00e9455936a61_1440w.webp)

  

  

## **四、安卓字体**  

中文：思源黑体 / Noto Sans Han

英文：Roboto

大小：主题文字 36-34px 正文 28-26px 提示文字 24-22px

思源黑体

链接：[http://navo.top/6BZBvm](https://link.zhihu.com/?target=http%3A//navo.top/6BZBvm)

密码：jd31

![](https://pic3.zhimg.com/80/v2-1844df08e0510c0dae8a3793b421cfd6_1440w.webp)

  

  

  

## **五、切图规范**

  

1.切图尺寸必须为**双数**

2.单像素的图会出现边缘模糊的情况

一般情况下，我们只需要提供3套切图资源就可以满足安卓工程师的适配，分别是HDPI、XHDPI、 XXHDPI 3套切图资源。现在都很方便使用figma、sketch、xd直接解放双手，无需手动切图！

  

![](https://pic1.zhimg.com/80/v2-3999324a087a2b3c08a15fa14c0a6e7c_1440w.webp)

  

## **如何用iOS的设计稿适配安卓**

现在绝大多数公司限于人力物力的限制，不能把iOS和安卓的设计稿全部执行出来，因此就存在一稿两用的情况；设计师以iOS版本的设计稿来适配安卓，下面我们来看一组有趣的数学换算题：

1080/1.5=720，720/1.5=480，1242*2208/1.15=1080*1920，也就是说，1242*2208（iOS@3倍尺寸）与1080*1920（安卓尺寸）是可以等比缩放的，所以，iOS与Android的尺寸是可共用1242*2208px。因此，以iOS设计尺寸进行设计是可以适配Android的。（前提是必须和安卓工程师沟通清楚）

  

另一种方式，就是把750×1334px等比例调整尺寸到安卓1080×1920px，对各个控件进行微调，重新提供标注（用dp标注）。也就是需要提供两套标注，一套给iOS，一套给Android。

  

## **iOS开发语言**

  

![](https://pic1.zhimg.com/80/v2-e9a2646e5c3230a59d748436d70593bc_1440w.webp)

  

作为iOS开发工程师，最重要的三个工具是：Obiective-C、Swift、UIKit框架。Obiective-C是目前最有效率的语言；而Swift开发非常高效。一般iOS工程师会在这两个语言中选择一种作为开发工具。UIKit是苹果系统自带的一套框架，这个框架里有设置按钮、滑竿、状态栏、电池电量、键盘等接口可供调用。所以我们看到很多第三方APP的界面中，有许多控件和苹果自带程序是一致的，这就是UIKit的功劳。  

  

## **iOS开发里单位是pt**

750×1334尺寸的换算关系 1pt=2px，也就是说程序员拿到我们的px单位的标注稿，自己除以2就是pt了。（这也是为什么建议设计师用@1倍图做设计稿的原因）

![](https://pic4.zhimg.com/80/v2-f56da14fafbc565d5cd68b8c9ddd721f_1440w.webp)

  

  

## **参考资料及资源下载**

  

苹果开发者中心网址：

[https://developer.apple.com/](https://link.zhihu.com/?target=https%3A//developer.apple.com/)

  

苹果人机交互规范：

[https://developer.apple.com/design/human-interface-guidelines/](https://link.zhihu.com/?target=https%3A//developer.apple.com/design/human-interface-guidelines/)

  

iOS设计资源下载：

[https://developer.apple.com/design/resources/](https://link.zhihu.com/?target=https%3A//developer.apple.com/design/resources/)

  

iOS控件下载地址：

[https://developer.apple.com/design/resources/](https://link.zhihu.com/?target=https%3A//developer.apple.com/design/resources/)

  

屏幕尺寸规范资源：

[http://www.woshipm.com/screen/watch.html](https://link.zhihu.com/?target=http%3A//www.woshipm.com/screen/watch.html)

  

PS蓝湖插件下载：

[https://lanhuapp.com/ps](https://link.zhihu.com/?target=https%3A//lanhuapp.com/ps)

  

SKetch插件下载：

[https://lanhuapp.com/mac](https://link.zhihu.com/?target=https%3A//lanhuapp.com/mac)

  

蓝湖手机预览APP下载：

[https://lanhuapp.com/app](https://link.zhihu.com/?target=https%3A//lanhuapp.com/app)

  

蓝湖自动同步网盘团队协作：

[https://lanhuapp.com/sync](https://link.zhihu.com/?target=https%3A//lanhuapp.com/sync)

  

![动图封面](https://pic2.zhimg.com/v2-e417f538e56d398f50f1d3698e9bce41_b.jpg)

[全网顶尖UI全栈设计教程强势来袭！​mp.weixin.qq.com/s?__biz=MzI2Mzc0Nzk2OQ==&mid=2247523461&idx=1&sn=88470c4b106e40f4b84821e562324b08&chksm=eab5fc6bddc2757d412b6acb88714fef36fbc75ad171f7bf11d766cc7369a639097cec091b8d&scene=21#wechat_redirect![](https://pic3.zhimg.com/v2-454b7d4263ada2477a9d8543fe2d6c86_180x120.jpg)](https://link.zhihu.com/?target=http%3A//mp.weixin.qq.com/s%3F__biz%3DMzI2Mzc0Nzk2OQ%3D%3D%26mid%3D2247523461%26idx%3D1%26sn%3D88470c4b106e40f4b84821e562324b08%26chksm%3Deab5fc6bddc2757d412b6acb88714fef36fbc75ad171f7bf11d766cc7369a639097cec091b8d%26scene%3D21%23wechat_redirect)

[UI设计进阶干货 - 动效](https://link.zhihu.com/?target=http%3A//mp.weixin.qq.com/s%3F__biz%3DMzI2Mzc0Nzk2OQ%3D%3D%26mid%3D2247488542%26idx%3D1%26sn%3Defb224bc29c84e9846fb22269e18eaff%26chksm%3Deab674f0ddc1fde64d9850a1df12638c170145cf1e663e874280f094e9b54fed14a98264c77c%26scene%3D21%23wechat_redirect)

[UI设计进阶干货-闪屏](https://link.zhihu.com/?target=http%3A//mp.weixin.qq.com/s%3F__biz%3DMzI2Mzc0Nzk2OQ%3D%3D%26mid%3D2247487657%26idx%3D1%26sn%3Df85fa5aa92c08119964292b384bc3632%26chksm%3Deab67047ddc1f951d55c09a27712337812ecec463c2f61e92723fbb2f7cb6077bf7eae2ec722%26scene%3D21%23wechat_redirect)

[UI设计进阶干货-引导页](https://link.zhihu.com/?target=http%3A//mp.weixin.qq.com/s%3F__biz%3DMzI2Mzc0Nzk2OQ%3D%3D%26mid%3D2247487694%26idx%3D1%26sn%3D8e31c5e88126b91c4feee892a6ddfa04%26chksm%3Deab67020ddc1f936bbf3c5d693402a8b5125083347beacf87a226ecb9c61efe30f46f917c85c%26scene%3D21%23wechat_redirect)

[UI设计进阶干货-注册登录](https://link.zhihu.com/?target=http%3A//mp.weixin.qq.com/s%3F__biz%3DMzI2Mzc0Nzk2OQ%3D%3D%26mid%3D2247487699%26idx%3D1%26sn%3D72757cd87180ca3e95c5af9292e44f36%26chksm%3Deab6703dddc1f92bccf7ceb4551f2a66f0f1b1cb6dd40fa1efedb7e33ba45797eccd69797c14%26scene%3D21%23wechat_redirect)

[UI设计进阶干货 - 首页](https://link.zhihu.com/?target=http%3A//mp.weixin.qq.com/s%3F__biz%3DMzI2Mzc0Nzk2OQ%3D%3D%26mid%3D2247487808%26idx%3D1%26sn%3D4249c5f855c6950c506e567f46d998a3%26chksm%3Deab671aeddc1f8b862a1b62b24afbdccb60db3b050d6003a39f48962feb69a8873b9871c2c94%26scene%3D21%23wechat_redirect)

[UI设计进阶干货 - Banner](https://link.zhihu.com/?target=http%3A//mp.weixin.qq.com/s%3F__biz%3DMzI2Mzc0Nzk2OQ%3D%3D%26mid%3D2247488423%26idx%3D1%26sn%3D846a610207020ed6d90e1a6d4fa806c8%26chksm%3Deab67349ddc1fa5f786a710117b1e0984c2c0a794e06e0186a1c150b00b71804c8e94936e199%26scene%3D21%23wechat_redirect)

[UI设计进阶干货-列表页](https://link.zhihu.com/?target=http%3A//mp.weixin.qq.com/s%3F__biz%3DMzI2Mzc0Nzk2OQ%3D%3D%26mid%3D2247487843%26idx%3D1%26sn%3Db7bd0dcaf0e56837070d4c3480c02e36%26chksm%3Deab6718dddc1f89bc36ed78b002050deb810adaa25b3869cfb3f7ac36484d1363b1771c63626%26scene%3D21%23wechat_redirect)

[UI设计进阶干货 - 适配&标注](https://link.zhihu.com/?target=http%3A//mp.weixin.qq.com/s%3F__biz%3DMzI2Mzc0Nzk2OQ%3D%3D%26mid%3D2247488280%26idx%3D1%26sn%3Dc2557397152520a923d4de3e1de2612d%26chksm%3Deab673f6ddc1fae0f4b4a5b4e23d3d47dc729b889bc5677fc61505f76afb931129e2efc94b2b%26scene%3D21%23wechat_redirect)

[UI设计进阶干货 - 切图&命名](https://link.zhihu.com/?target=http%3A//mp.weixin.qq.com/s%3F__biz%3DMzI2Mzc0Nzk2OQ%3D%3D%26mid%3D2247488272%26idx%3D1%26sn%3Dbe14f5ec4b390c5301373b6395cf6a5e%26chksm%3Deab673feddc1fae82561065ea172737b5629cb3dc187b0b49d56f364fd02d3b7dac1783b8b23%26scene%3D21%23wechat_redirect)

[UI进阶干货—金刚区](https://link.zhihu.com/?target=http%3A//mp.weixin.qq.com/s%3F__biz%3DMzI2Mzc0Nzk2OQ%3D%3D%26mid%3D2247491251%26idx%3D1%26sn%3D660ab3295892196cd4f91141012c820c%26chksm%3Deab67e5dddc1f74b0d8c689a96c39fe80a496280e5080b3fab5a07e649db301e95b09e050517%26scene%3D21%23wechat_redirect)

[UI进阶干货—阴影](https://link.zhihu.com/?target=http%3A//mp.weixin.qq.com/s%3F__biz%3DMzI2Mzc0Nzk2OQ%3D%3D%26mid%3D2247489501%26idx%3D1%26sn%3D2650156801e46f45d542ee7ff5b621a6%26chksm%3Deab67733ddc1fe251ca5cbc1b727c339bd77e691ebd798af36b2505d4f2f850bd497c6a25053%26scene%3D21%23wechat_redirect)

[UI进阶干货 - 竞品分析](https://link.zhihu.com/?target=http%3A//mp.weixin.qq.com/s%3F__biz%3DMzI2Mzc0Nzk2OQ%3D%3D%26mid%3D2247493136%26idx%3D1%26sn%3Dfb3ad810b1ad61eaabd24c2517efe310%26chksm%3Deab586feddc20fe8cd20e21996afcb3e6e1cc1951c132f3ef6ad04becd66406b3adc0c1f6f70%26scene%3D21%23wechat_redirect)

[UI进阶干货-详解B端产品&C端产品](https://link.zhihu.com/?target=http%3A//mp.weixin.qq.com/s%3F__biz%3DMzI2Mzc0Nzk2OQ%3D%3D%26mid%3D2247493145%26idx%3D1%26sn%3D079abad6417e637ceae4d87bdb16150a%26chksm%3Deab586f7ddc20fe14ee6f3b3eeb4210e872265396cea88d3119647f617537b2552460cc2e588%26scene%3D21%23wechat_redirect)

[UI进阶干货-尼尔森十大交互原则](https://link.zhihu.com/?target=http%3A//mp.weixin.qq.com/s%3F__biz%3DMzI2Mzc0Nzk2OQ%3D%3D%26mid%3D2247493172%26idx%3D1%26sn%3D1ba0b7cf9163633eb16bf0d34c943cdb%26chksm%3Deab586daddc20fccba48a906592af237818c208ace08efb10712ab72ba5850a93a25b6ee067a%26scene%3D21%23wechat_redirect)

[UI进阶干货 - PRD撰写技巧](https://link.zhihu.com/?target=http%3A//mp.weixin.qq.com/s%3F__biz%3DMzI2Mzc0Nzk2OQ%3D%3D%26mid%3D2247493318%26idx%3D1%26sn%3De5ee80dddd267cc7682173d1c195536f%26chksm%3Deab58628ddc20f3e3b681ffc222d3844432cc9475997e319f63456315785adefa9dab1cecc4c%26scene%3D21%23wechat_redirect)

[UI进阶干货 - 加载动画](https://link.zhihu.com/?target=http%3A//mp.weixin.qq.com/s%3F__biz%3DMzI2Mzc0Nzk2OQ%3D%3D%26mid%3D2247493352%26idx%3D1%26sn%3D0ac7c134c55bb05522a9cb1f3cdeffca%26chksm%3Deab58606ddc20f102618771dd4ec67ea5d0e4595022a3f3383283813bb9be24c7baf12d96249%26scene%3D21%23wechat_redirect)

[UI进阶干货 - 表单](https://link.zhihu.com/?target=http%3A//mp.weixin.qq.com/s%3F__biz%3DMzI2Mzc0Nzk2OQ%3D%3D%26mid%3D2247493714%26idx%3D1%26sn%3D930598b7051417afe2652078eec1b04b%26chksm%3Deab588bcddc201aa554c820a521968066cee705db369f8616f1325decc7a500e9dfd8bd12c0d%26scene%3D21%23wechat_redirect)

[UI进阶干货 - 轻量化设计](https://link.zhihu.com/?target=http%3A//mp.weixin.qq.com/s%3F__biz%3DMzI2Mzc0Nzk2OQ%3D%3D%26mid%3D2247493827%26idx%3D1%26sn%3Dc95d27c59135077d3988713c9ea48ebd%26chksm%3Deab5882dddc2013bc5b23e223903432e4c606aa4c49e5abfe2fa0be0dbe83bfe7a072c5cdcca%26scene%3D21%23wechat_redirect)