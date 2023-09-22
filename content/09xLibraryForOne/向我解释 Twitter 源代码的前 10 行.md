#优化 #twitter #源代码
在过去的几周里，我一直在我的租赁家具公司[Pabio招聘一名高级](https://pabio.com/en-de/)[全栈](https://css-tricks.com/what-does-it-mean-to-be-full-stack/)JavaScript 工程师。由于我们是一个远程团队，我们在 Zoom 上进行面试，我观察到一些开发人员不擅长实时编码或白板面试，即使他们擅长这项工作。因此，相反，我们进行了长达一小时的技术讨论，在其中我向他们询问有关网络生命力、可访问性、浏览器大战和其他类似网络主题的问题。我总是喜欢问的一个问题是：**“向我解释一下 Twitter 源代码的前十行左右。”**[](https://pabio.com/en-de/)

我认为这是一个简单的测试，可以告诉我很多关于他们所拥有的基础前端知识的深度，本文列出了最佳答案。

对于上下文，我共享我的屏幕，打开 Twitter.com 并单击**查看源代码**。然后我请他们逐行帮助我理解 HTML，他们可以说多少就说多少。我还放大以使文本更清晰，因此您看不到整行，但您会有所了解。这是它的样子：

![来自 Twitter 的源代码截图。](https://i0.wp.com/css-tricks.com/wp-content/uploads/2022/02/s_1B56F376C1F0FF4107271F0A0DA0CCE65FEA59C4FFF17FD5500C71C0B3B69841_1642491088212_screenshot-twitter-source-scaled.jpg?resize=2560%2C1600&ssl=1)

请注意，由于我们的技术讨论是对话。我不希望任何人给出完美的答案。如果我听到一些正确的关键词，我就知道候选人知道这个概念，我会尝试将它们推向正确的方向。

### [](https://css-tricks.com/explain-the-first-10-lines-of-twitter-source-code/#aa-line-1-doctype-html)第 1 行：`<!DOCTYPE html>`

每个文档源代码的第一行都非常适合这次面试，因为候选人对`DOCTYPE`声明的了解程度与他们拥有多少年的经验非常相似。我仍然记得我在 Dreamweaver 中使用长长的 XHTML DOCTYPE 行，就像 Chris 在 2009 年的文章[“常见的 DOCTYPES”](https://css-tricks.com/snippets/html/the-common-doctypes/)中列出的那样。

**完美答案：**这是我们一直放在 HTML 文件第一行的文档类型（doc-type）声明。你可能认为这个信息是多余的，因为浏览器已经知道响应的 MIME 类型是`text/html`; 但[在 Netscape/Internet Explorer 时代](https://css-tricks.com/chapter-8-css/)，浏览器有一项艰巨的任务是确定使用哪种 HTML 标准来呈现来自多个竞争版本的页面。

这尤其令人讨厌，因为每个标准都会生成不同的布局，因此采用此标签是为了便于浏览器使用。以前，`DOCTYPE`标签很长，甚至包括规范链接（有点像今天的 SVG），但幸运的是，简单`<!doctype html>`的标签在 HTML5 中被标准化并且仍然存在。

**也接受：**`DOCTYPE`这是让浏览器知道这是一个 HTML5 页面并且应该这样呈现的标签。

### [](https://css-tricks.com/explain-the-first-10-lines-of-twitter-source-code/#aa-line-2-html-dirltr-langen)第 2 行：`<html dir="ltr" lang="en">`

源代码中的这一行告诉我候选人是否知道可访问性和本地化。令人惊讶的是，在我的采访中只有少数人知道该`dir`属性，但这是讨论屏幕阅读器的一个很好的话题。几乎每个人都能弄清楚这个`lang="en"`属性，即使他们之前没有使用过它。

**完美答案：**这是 HTML 文档的根元素，所有其他元素都在这个元素中。在这里，它有两个属性，方向和语言。方向属性的值从左到右告诉用户代理内容在哪个方向；对于阿拉伯语等语言，其他值是从右到左的，或者只是`auto`留给浏览器来确定。

language 属性告诉我们这个标签内的所有内容都是英文的；您可以将此值设置为任何语言标签，甚至可以区分`en-us`和`en-gb`，例如。这对于屏幕阅读器了解要以哪种语言宣布也很有用。

### [](https://css-tricks.com/explain-the-first-10-lines-of-twitter-source-code/#aa-line-3-meta-charsetutf-8)第 3 行：`<meta charset="utf-8">`

**完美答案：**源代码中的元标记用于提供有关此文档的元数据。字符集（char-set）属性告诉浏览器使用哪种字符编码，而 Twitter 使用标准的 UTF-8 编码。UTF-8 很棒，因为它有很多字符点，因此您可以在源代码中使用各种符号和表情符号。将此标记放在代码开头附近很重要，这样浏览器在遇到此行时还没有开始解析太多文本；我认为规则是把它放在文档的第一个千字节中，但我想说最好的做法是把它放在`<head>`.

附带说明一下，看起来 Twitter`<head>`出于性能原因（要加载的代码更少）省略了该标签，但我仍然希望将其明确化，因为它是所有元数据、样式等的明确归宿。

### [](https://css-tricks.com/explain-the-first-10-lines-of-twitter-source-code/#aa-line-4-meta-nameviewport-contentwidthdevice)第 4 行：`<meta name="viewport" content="width=device-...`

**完美答案：**源代码中的这个元标记用于在智能手机等小屏幕上正确调整网页大小。如果你还记得最初的 iPhone 主题演讲，史蒂夫乔布斯在那个 4.5 英寸的小屏幕上展示了整个《纽约时报》网站；那时，这是一个了不起的功能，您必须捏住才能真正阅读。

现在网站在设计上是响应式的，`width=device-width`告诉浏览器使用 100% 的设备宽度作为视口，因此没有水平滚动，但您甚至可以为宽度指定特定的像素值。标准的最佳实践是将初始比例设置为`1`和宽度设置为，`device-width`以便人们仍然可以根据需要进行缩放。

源代码的屏幕截图没有显示这些值，但很高兴知道：Twitter 也适用`user-scalable=0`，顾名思义，它禁用缩放功能。这不利于可访问性，但会使网页更像原生应用程序。它也`maximum-scale=1`出于同样的原因设置（您可以使用最小和最大比例来限制这些值之间的缩放能力）。一般来说，设置全宽和初始比例就足够了。

### [](https://css-tricks.com/explain-the-first-10-lines-of-twitter-source-code/#aa-line-5-meta-propertyogsite_name-contenttwitt)第 5 行：`<meta property="og:site_name" content="Twitt...`

大约 50% 的候选人知道 Open Graph 标签，这个问题的一个好的答案表明他们知道 SEO。

**完美答案：**此标签是网站名称 Twitter 的开放图 (OG) 元标签。[Facebook 制定了Open Graph 协议](https://ogp.me/)，以便更轻松地展开链接并[以漂亮的卡片布局显示它们的预览](https://css-tricks.com/microbrowsers-are-everywhere/)；开发人员可以添加各种作者详细信息和封面图片以进行精美分享。事实上，如今使用 Puppeteer 之类的工具自动生成开放图形图像甚至很常见。（[CSS-Tricks 使用了一个 WordPress 插件](https://css-tricks.com/automatic-social-share-images/)。）

另一个有趣的旁注是元标记通常具有`name`属性，但 OG 使用非标准`property`属性。我想这只是 Facebook 是 Facebook 吗？标题、URL 和描述 Open Graph 标签有点多余，因为我们已经有这些的常规元标签，但人们添加它们只是为了安全。如今，大多数网站都结合使用 Open Graph 和其他元标记以及页面上的内容来生成丰富的预览。

### [](https://css-tricks.com/explain-the-first-10-lines-of-twitter-source-code/#aa-line-6-meta-nameapple-mobile-web-app-title-cont)第 6 行：`<meta name="apple-mobile-web-app-title" cont...`

大多数候选人不知道这一点，但有经验的开发人员可以讨论如何针对 Apple 设备优化网站，例如`apple-touch-icon`s 和 Safari 固定标签 SVG。

**完美答案：**您可以将网站固定在 iPhone 的主屏幕上，让它感觉像是一个原生应用程序。Safari 不支持渐进式 Web 应用程序，而且您无法在 iOS 上真正使用其他浏览器引擎，因此如果您想要 Twitter 喜欢的原生体验，您实际上没有其他选择。所以他们添加这个来告诉 Safari 这个应用的标题是 Twitter。下一行类似，控制应用程序启动时状态栏的外观。

### [](https://css-tricks.com/explain-the-first-10-lines-of-twitter-source-code/#aa-line-8-meta-nametheme-color-contentffffff)第 8 行：`<meta name="theme-color" content="#ffffff"...`

**完美答案：**这是 Apple 状态栏颜色元标记的适当 Web 标准式等效物。[它告诉浏览器为周围的 UI 设置主题](https://css-tricks.com/meta-theme-color-and-trickery/)[。](https://css-tricks.com/meta-theme-color-and-trickery/)Android 上的 Chrome 和桌面上的 Brave 在这方面都做得很好。您可以在内容中放置任何 CSS 颜色，甚至可以使用该`media`属性仅针对特定媒体查询显示此颜色，例如支持深色主题。您还可以在 Web 应用清单中定义此属性和其他属性。

### [](https://css-tricks.com/explain-the-first-10-lines-of-twitter-source-code/#aa-line-9-meta-http-equivorigin-trial-content)第 9 行：`<meta http-equiv="origin-trial" content="...`

我采访过的人都不知道这个。我假设只有当您对标准轨道上发生的所有新事物有深入的了解时，您才会知道这一点。

**完美答案：** Origin 试用版让我们可以在我们的网站上使用新的和实验性的功能，并且用户代理会跟踪反馈并报告给 Web 标准社区，而无需用户选择加入功能标志。例如，Edge 对双屏和可折叠设备原语进行了原始试验，这非常酷，因为您可以根据可折叠手机是打开还是关闭来制作有趣的布局。

**也接受：**我不知道这个。

### [](https://css-tricks.com/explain-the-first-10-lines-of-twitter-source-code/#aa-line-10-html-ms-text-size-adjust100-webkit-text)第 10 行：`html{-ms-text-size-adjust:100%;-webkit-text...`

几乎没有人知道这个。只有您了解 CSS 边缘情况和优化，您才能弄清楚这条线。

**完美答案：**假设您没有移动响应站点，并且您在小屏幕上打开它，因此浏览器可能会调整文本大小以使其更大以便更易于阅读。CSS[`text-size-adjust`](https://developer.mozilla.org/en-US/docs/Web/CSS/text-size-adjust)属性可以使用值 none 禁用此功能，也可以指定允许浏览器放大文本的百分比。

在这种情况下，Twitter 表示最大值为`100%`，因此文本不应大于实际大小；他们这样做是因为他们的网站已经响应，并且他们不想冒险让浏览器破坏具有更大字体的布局。这适用于根 HTML 标记，因此它适用于其中的所有内容。由于这是一个实验性 CSS 属性，因此需要供应商前缀。此外，在这个 CSS 之前有一个缺失`<style>`，但我猜这在上一行中被缩小了，我们看不到它。

**也接受：**我不具体了解此属性，但`-ms`和`-webkit-`是 Internet Explorer 和基于 WebKit 的浏览器分别用于非标准属性的供应商前缀。当 CSS3 出现时，我们曾经要求使用这些前缀，但随着属性从实验到稳定或被采用到标准轨道，这些前缀消失了，取而代之的是标准化属性。

### [](https://css-tricks.com/explain-the-first-10-lines-of-twitter-source-code/#aa-bonus-line-11-bodymargin0)奖金——第 11 行：`body{margin:0;}`

Twitter 源代码中的这一行特别有趣，因为您可以跟进有关重置和规范化网页之间的区别的问题。几乎每个人都知道正确答案的一个版本。

**完美答案：**因为不同的浏览器具有不同的默认样式（用户代理样式表），您希望通过重置属性来覆盖它们，以便您的网站在不同设备上看起来相同。在这种情况下，Twitter 告诉浏览器删除 body 标签的默认边距。这只是为了减少浏览器的不一致性，但我更喜欢规范化样式而不是重置它们，即跨浏览器应用相同的默认值而不是完全删除它们。人们甚至过去使用`* { margin: 0 }`它完全是矫枉过正并且对性能不利，但是现在导入类似`normalize.css`or `reset.css`（甚至[更新的东西](https://css-tricks.com/an-interview-with-elad-shechter-on-the-new-css-reset/)）并从那里开始是很常见的。

### [](https://css-tricks.com/explain-the-first-10-lines-of-twitter-source-code/#aa-more-lines)更多线路！

我总是喜欢玩浏览器检查器工具来查看网站是如何制作的，这就是我想出这个想法的原因。尽管我认为自己是语义 HTML 方面的专家，但每次做这个练习时我都会学到一些新东西。

由于 Twitter 主要是一个客户端 React 应用程序，因此源代码中只有几十行。即使这样，还有很多东西要学！Twitter 源代码中还有一些有趣的行，我留给读者作为练习。你能在采访中解释其中的几个？

```html
<link rel="search" type="application/opensearchdescription+xml" href="/opensearch.xml" title="Twitter">
```

…告诉浏览器用户可以将 Twitter 添加为搜索引擎。

```html
<link rel="preload" as="script" crossorigin="anonymous" href="https://abs.twimg.com/responsive-web/client-web/polyfills.cad508b5.js" nonce="MGUyZTIyN2ItMDM1ZC00MzE5LWE2YmMtYTU5NTg2MDU0OTM1" />
```

…有许多可以讨论的有趣属性，尤其是`nonce`.

```html
<link rel="alternate" hreflang="x-default" href="https://twitter.com/" />
```

…用于国际登陆页面。

```css
:focus:not([data-focusvisible-polyfill]){outline: none;}
```

…用于在不使用键盘导航时移除焦点轮廓（CSS`:focus-visible`选择器在此处填充）。