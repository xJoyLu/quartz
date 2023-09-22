author:: JamesHopbourn
source:: [妙用重定向，优化 iOS 的搜索体验 - 少数派](https://sspai.com/post/68026)
clipped:: [[2022-11-08]]
published:: 

编注：本文涉及 URL Rewrite 和正则表达式。如果你对于正则表达式不太熟悉，可以阅读 [这篇文章](https://sspai.com/post/60650) 快速入门。如果不了解 URL Rewrite 的基本知识，以及相关的增减重定向规则，可以阅读 [这篇文章](https://surge.mitsea.com/http-processing/url-rewrite)。

本文所设计的重定向规则，均可在 [Apple Automation](https://github.com/JamesHopbourn/Apple-Automation) 项目的 [URL rewrite.conf](https://github.com/JamesHopbourn/Apple-Automation/blob/master/URL%20Rewrite.conf) 文件中找到，无需在文章中逐条复制。

---

在 macOS 上使用 Alfred，其带来的效率提升，是一用过就很难回去的体验。在普通模式下，直接输入文字回车就能进行搜索。如果是输入了特定关键词，再加上搜索文字，即可打开对应的 URL 或者 workflow。但是否有一种办法，可以将这样的功能带到 iOS 上呢？

本文将结合 302 重定向技术，在 iOS 上实现类似于 Alfred 的功能。通过关键词重定向，可以**快速搜索某个网页上相关的内容**。在写好重定向规则后，只需要从 iOS 的主屏幕下拉呼出 Spotlight，输入搜索关键词和内容，即可**跳转到指定的网页或应用并展示搜索结果**。

## 在指定网站内搜索

使用 302 重定向技术，可以帮我们直接跳转到我们想要搜索的网站中去。

### 谷歌

自从 2010 年，谷歌退出中国大陆市场后，使用进行谷歌搜索的结果如下所示。

![](https://cdn.sspai.com/2021/07/30/article/6ba309de741108e845b75aa302631925?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

这个页面会将地址重定向到 Google HK。复制跳转的地址，可以得到如下的原始链接。

```
https://www.google.cn/search?q=sspai&ie=UTF-8&oe=UTF-8&hl=zh-hans-cn&client=safari
```

为了解决这层不必要的跳转，便可以使用 302 重定向技术，可以直接将 Google CN 重定向到 Google，语法如下：

```
^https?://www.google.cn https://www.google.com 302
```

该规则由三个部分组成，`^https?://www.google.cn`是要匹配的 URL 地址，`https://www.google.com`是重定向之后的地址，最后的 302 则是地址重写的模式。加入重写规则之后，再次搜索以 sspai 为关键词搜索，就可以直接显示搜索结果，而跳转之后的地址如下：

```
http://www.google.com/search?q=sspai&ie=UTF-8&oe=UTF-8&hl=zh-hans-cn&client=safari
```

可以看出，此时 URL 的地址已经重定向到了 google.com。无需手动点击，在回车之后可以直接显示搜索结果。

这便是 302 重定向最基本的应用之一。有了这样的基本概念之后，不妨把思路拓宽一点，不要限制于谷歌搜索上，把它应用到更广的范围。

### 哔哩哔哩

使用网页版的哔哩哔哩搜索需要几步？大约六步。

而借助重定向技术，可以快速直达搜索结果页面。接下来来看看如何写出一条规则，访问哔哩哔哩，并输入关键词进行搜索，得到如下的搜索地址：

```
https://search.bilibili.com/all?keyword=少数派
```

删掉「少数派」关键词，重定向地址到 bilibili.com 的搜索地址，实现了 302 跳转到其他网站的功能，效果如下所示。 YouTube 也可以使用类似的方法进行重定向。

```
^https?://www.google.cn/search\?q=blbl\+ https://search.bilibili.com/all?keyword= 302

^https?://www.google.cn/search\?q=ytb\+ https://www.youtube.com/results?search_query= 302
```

![](https://cdn.sspai.com/2021/07/30/article/fdf4a0c7218ebcaba067796be66a3681?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

### GitHub

GitHub 是程序员们最喜欢的网站之一，也是最大的软件源代码托管服务平台，可谓是一个软件的大宝库。少数派上曾发过许多介绍 GitHub 软件文章，如下所示：

-   [《程序员常逛的 Github，原来是个隐藏的学习网站》](https://sspai.com/post/58120)
-   [《免费好用的软件哪里找？GitHub 上的这些资源不能错过》](https://sspai.com/post/53901)

所以，GitHub 作为这样的一个软件宝库，也值得为它写一条重定向规则。

访问 GitHub，分别以 ssh 为关键词搜索项目，JamesHopbourn 为关键词搜索用户，得到如下的 URL 地址：

```
https://github.com/search?q=ssh&type=repositories

https://github.com/search?q=JamesHopbourn&type=users
```

![](https://cdn.sspai.com/2021/07/30/article/54cf41d2aa2c2ec43f35c502859aee2a?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

通过这两条 URL 可以看出，GitHub 为了区分搜索类型，在 URL 地址里加入了 type 这一参数。但是构造的重定向地址有一个要求：**最后一个参数必须是关键词参数**。所以只要稍微调整一下参数顺序即可，调整参数位置后的 URL 地址如下：

```
https://github.com/search?type=repositories&q=ssh

https://github.com/search?type=users&q=JamesHopbourn
```

为了区分项目搜索和用户搜索，分别给它们命名缩写：gh 和 ghu，所以重定向规则和效果图如下：

```
^https?://www.google.cn/search\?q=gh\+ https://github.com/search?type=repositories&q= 302

^https?://www.google.cn/search\?q=ghu\+ https://github.com/search?type=users&q= 302
```

![](https://cdn.sspai.com/2021/07/30/article/ee1dc191fad91aee063953475a8af55a?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

根据这个原理，其他类似的单参数网页也可以如法炮制。读者可以根据自己的需要，给需要的网站编写规则。此处给出基本模版如下：

```
^https?://www.google.cn/search\?q=自定义网站缩写\+ 网站的搜索地址 302
```

## 在指定应用中搜索

实现了上面的谷歌搜索结果优化和其他网站跳转，不妨再次把思路拓宽一点。URL Scheme 也是一种 URL，只是它的 Scheme 不是属于 http 或者 https 罢了。所以也可以考虑给 URL Scheme 加一个 302 跳转功能。

以知乎为例，通过 zh 关键词和 302 跳转，将输入内容传递给知乎的 URL Scheme，并跳转知乎进行查询。

```
^https?://www.google.cn/search\?q=zh\+ zhihu://search?q= 302
```

但是在实际使用过程中，在每次跳转到知乎之前，需要经过 Safari 跳转。但是出于安全策略，每次都需要询问是否在知乎中打开，这会直接导致使用体验大打折扣。

![](https://cdn.sspai.com/2021/07/30/article/373dcadc5b85e62f36d3deaf9b2bca7a?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

这是苹果基于用户安全考虑而设计的，但是也在无形当中影响了使用体验。所以为了解决这个问题，有两种方式可以解决：

1.  使用其他浏览器，像是 Google Chrome 浏览器。在将它设置为默认浏览器之后，它只需要第一次确认之后，以后就不会再次询问。但是很明显这个解决方法，只适用于非 Safari 用户，对于 Safari 用户这会带来些许不便。
2.  如果其他浏览器这条路行不通，有没有其他方法？作者回想起了一个细节，每次在安装捷径动作的时候，Safari 就从不会询问是否在捷径中打开，这说明苹果对于自家的应用，开了一个白名单，如果是苹果官方应用，就无须确认即可直接跳转。

所以不难想出，只要构建一个捷径，让它代为传递参数即可实现直接跳转，无需二次确认。但是爱因斯坦曾说过：「凡事尽可能简洁，但不能太过简单。」有没有什么办法，可以不运行捷径，却同样可以实现跳转？

此处联想到在 Hum 的 [《URL Schemes 使用详解》](https://sspai.com/post/31500)这篇文章中，提到的 `x-success` 和 `x-error` 两个参数，它们的作用是在 URL Scheme 主体执行成功或者失败之后，跟着执行的其他 URL Scheme，它需要软件支持 x-callbakck-url 技术。

通过阅读[《配合“快捷指令”使用 X-Callback-URL》](https://support.apple.com/zh-cn/guide/shortcuts/apdcd7f20a6f/ios)这篇文章，可以知道捷径是支持 `x-error` 和 `x-success` 的，那么是否可以打开一个根本不存在的捷径，然后捷径就认为这条 URL Scheme 执行出现错误，从而去执行 x-error 所对应的真实 URL Scheme 呢？构造以下两种的 URL Scheme， 代表着 `x-success` 和 `x-error` 两种情况。

```
shortcuts://x-callback-url/run-shortcut?name=test&x-success=zhihu://search?q=

shortcuts://x-callback-url/run-shortcut?name=unnamed&x-error=zhihu://search?q=
```

![](https://cdn.sspai.com/2021/07/30/article/04382b62b53bb190dc9d2d2e8cf79055?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

经过尝试，`x-success` 会导致捷径闪退，`x-error` 会报错导致终止运行。所以，这两种解决方案只能以失败告终，只能设计捷径解决该需求。但是这同时也可以是对捷径未来的一个展望。是否可以去除这个捷径存在验证步骤，或者设计出一个名为 url 的参数，提供给捷径的 打开 URL Scheme 的功能呢？如下所示，只要传入 URL 参数，就可以通过捷径这个中转站，免二次确认直接打开某个 URL Scheme。

```
shortcuts://open-url?url=
```

接下来只好改弦更张，开始设计捷径解决需求。通过查询 Apple 官方文档 [使用 URL 方案运行快捷指令](https://support.apple.com/zh-cn/guide/shortcuts/apd624386f42/ios)，想要通过 URL Scheme 给捷径传入参数，可以使用下面这个 URL Scheme 实现：

```
shortcuts://run-shortcut?name=捷径名称&input=text&text=传入参数
```

为了使用捷径进行直接跳转，对重定向规则进行修改，将原来的 zhihu URL Scheme 替换为包含参数的捷径 URL Scheme。可以看到在传入参数的 text 处，预先置留了一个 `zh,` 的关键词字符，这是给捷径识别的关键词，用于区分不同的跳转软件。

```
^https?://www.google.cn/search\?q=zh\+ shortcuts://x-callback-url/run-shortcut?name=URL%20Rewrite&input=text&text=zh, 302
```

接下来开始设计捷径，首先要明确一点，这个捷径应该是可以处理多个 URL Scheme 的，而不是单单只为了知乎设计。所以这也就是预留关键词 `zh,` 的用途。

根据这一设计思路，就可以大概想出这个捷径的模块了，它由以下三个模块组成：

1.  传入文本处理：用于将预留关键词和搜索关键词分开；
2.  URL Scheme 字典：用于存储不同软件的 URL Scheme；
3.  打开 URL：构建 URL Scheme 之后，通过捷径直接打开。

### 传入文本处理

在上面重定向地址中，为了跳转不同的软件，放置不同的预留关键词。此时，它作为参数传入，接下来就需要传入文本进行处理。以知乎为例，预留关键词为 `zh,` 所以为了分割两个不同的关键词。此处可以使用自定义文本分割，以半角逗号为分割符，分开两个元素。并从拆分文本中取出第一项，并设置成名为 `app` 的变量。如法炮制，再从拆分文本中取出最后一项，设置成名为 `keyword` 的变量，它代表着实际要查询的文本。

![](https://cdn.sspai.com/2021/07/30/article/bf5d37498e02568941108d37a72e8805?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

### URL Scheme 字典

为了实现多个应用程序的跳转，此处可以考虑使用字典来保存 URL Scheme，然后通过字典的键(key)查找对应的值(value)。以知乎、淘宝和京东为例，创建一个字典，键值对如下：

```
zh zhihu://search?q=%@

tb taobao://s.taobao.com?q=%@

jd openjd://virtual?params={"des":"productList","keyWord":"%@","from":"search","category":"jump"}
```

在构建好了字典之后，便是顺理成章地从找出映射关系。使用脚本在词典中获取 `app` 变量的值，例如刚才传入的 `app` 变量值为 zh，就查找到了 `zhihu://search?q=%@`这条 URL Scheme。

这时在 value 中可以看出，搜索的关键词参数后加上了 `%@` 这样的字符，这是从 Pin 那边借鉴来的思路。使用文本替换模块，将 `%@` 替换为刚才设置好的 `keyword` 参数。为什么要设计 `%@` 这样的代替符，是考虑到部分 URL Scheme 参数位置的原因，以上面京东的 URL Scheme 为例，它的参数值并不是放在最后，而是作为 JSON 的键值对参数传递，所以使用 `%@` 的代替符是最优解。

到此，URL Scheme 构建完毕。

![](https://cdn.sspai.com/2021/07/30/article/26607dbc17adcbd3cde2257927cad4cd?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

### 打开 URL

如上面右图所示，该步骤较为简单，只需要两个模块即可实现，将 URL 设置为更新后的文本，并打开该 URL Scheme。需要注意的是，虽然该模块显示的是在 Safari 浏览器打开，但是实际上是会直接跳转到对应的软件，无需二次确认。

整个捷径只使用了 11 个模块，就可以完美地实现功能需求，且如果以后还有其他 URL Scheme 加入，只需要在字典处增加键值对即可，可扩展性和维护性较好。

![](https://cdn.sspai.com/2021/07/30/4d4cac955644e222622c05b7bed5c5a4.gif)

## 小结

本段介绍了重定向的更高级玩法，使用重定向、URL Scheme 和捷径实现，只需要从主屏幕下拉，输入软件缩写 + 关键词，即可直接跳转到相应软件进行搜索。实现了类似 macOS 上 Alfred 的使用体验，虽然中间免不了使用捷径的跳转，但是动画较为流畅，实际使用起来体验还是很好的。

它的核心思路再梳理：

1.  为每个软件创建重定向规则
2.  在捷径的字典里增加 URL Scheme 键值对

两个步骤即可配置完成，而且重定向规则也有通用模版，只要稍加研究，就能理解这个玩法。重定向规则模版如下，只要将模版中两处的 `%@` 替换，修改为你所设定的关键词，规则就创建好了，再手动写入配置文件即可。但是要注意的是，捷径名称必须是：「URL rewrite」，如果要使用其他名字，需要将模版中的 name 参数值同样修改。

```
^https?://www.google.cn/search\?q=%@\+ shortcuts://x-callback-url/run-shortcut?name=URL%20Rewrite&input=text&text=%@, 302
```

在本文中，使用了 302 重定向技术，通过关键词重定向了 Spotlight 的搜索结果。URL 和 URL Scheme 本质上是同一类东西，只是它们使用的协议不同。一个是 http 和 https，另一个则是各软件厂商自己定义的协议。整体的框架是一致的，所以才可以扩展出这么多玩法。

借助 302 重定向，实现了从谷歌跳转到其他网站，跳转到应用里。读者可以根据自己的需求，结合上面给出的重定向规则模版，写出适合自己使用的规则。

## 参考文章

-   [302 Found - HTTP | MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/302)
-   [HTTP 302 - 维基百科，自由的百科全书](https://zh.wikipedia.org/zh-hans/HTTP_302)
-   [Google Advanced Search - Google.de](http://www.google.cn/advanced_search)
-   [The Ultimate Guide to the Google Search Parameters](https://moz.com/blog/the-ultimate-guide-to-the-google-search-parameters)