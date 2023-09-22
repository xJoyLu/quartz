本节是收集一些阅读友好型的字体  

# 中文字体

-   霞鹜文楷： [https://github.com/lxgw/LxgwWenKai](https://github.com/lxgw/LxgwWenKai) [flying fly flies](https://publish.obsidian.md/chinesehelp/07+%E4%BF%A1%E6%81%AF%E6%BA%90%E4%B8%8E%E8%B4%A1%E7%8C%AE%E8%80%85/flying+fly+flies)推荐
-   竹石体： [https://m.fonts.net.cn/font-35850420097.html](https://m.fonts.net.cn/font-35850420097.html) [无铭](https://publish.obsidian.md/chinesehelp/01+2021%E6%96%B0%E6%95%99%E7%A8%8B/%E6%97%A0%E9%93%AD)推荐
-   萍方
-   思源黑体
-   华康手札

# 英文字体

Bookerly：自行百度，kindle的字体 [flying fly flies](https://publish.obsidian.md/chinesehelp/07+%E4%BF%A1%E6%81%AF%E6%BA%90%E4%B8%8E%E8%B4%A1%E7%8C%AE%E8%80%85/flying+fly+flies)推荐

# 字体

知乎：

```
body {
    font-family: -apple-system,BlinkMacSystemFont,Helvetica Neue,PingFang SC,Microsoft YaHei,Source Han Sans SC,Noto Sans CJK SC,WenQuanYi Micro Hei,sans-serif;
    font-size: 15px;
    color: #121212;
}
```


简书

```
body {
    line-height: 1.42857;
    color: #404040;
    background-color: #fff;
    font-family: -apple-system,BlinkMacSystemFont,"Apple Color Emoji","Segoe UI Emoji","Segoe UI Symbol","Segoe UI","PingFang SC","Hiragino Sans GB","Microsoft YaHei","Helvetica Neue",Helvetica,Arial,sans-serif;
    font-feature-settings: "tnum";
    font-variant: tabular-nums;
}
```


## 英文常见字体

非衬线字体（Sans-serif）

- Helvetica ：被评为设计师最爱的字体，Realist风格，简洁现代的线条，非常受到追捧。在Mac下面被认为是最佳的网页字体，在Windows下由于Hinting的原因显示很糟糕。

- Arial ：Helvetica的「克隆」，和Helvetica非常像，细节上比如R和G有小小差别。如果字号太小，文字太多，看起来会有些累眼。Win和Mac显示都正常

- Lucida Family ：Lucida Grande是Mac OS UI的标准字体，属于humanist风格，稍微活泼一点。Mac下的显示要比Win下好。

- Verdana ：专门为了屏显而设计的字体，humanist风格，在小字号下仍可以清楚显示，但是字体细节缺失严重，最好别做标题。

- Tahoma ：也是humanist风格，字体和Verdana有点像，但是略窄一些，counter略小，曾经是Windows的标准字体，Mac 10.5之后默认也有安装。

- Trebuchet MS: 为微软设计的一个humanist风格字体，个人觉得个性太过突出，用得不好会不搭。


衬线字体（Serif）

- Georgia ：基本上适合正文屏显的衬线字体，非Georgia莫属了。笔画粗重，衬线明线，轮廓较大，小字体显示也很清晰，同时细节还算OK。

- Times ：Times是为了报纸而设计的，特点是可以在有限的空间塞进去更多的文字，笔画较弱，小字号正文屏显看起来累眼。曾经Engadget改版的时候用了Times作为正文，被骂得很惨之后换成了Georgia。



## 中文常见字体

非衬线字体

- 微软雅黑（Microsoft YaHei） ：Vista之后新引入的字体，打开Cleartype之后显示效果不错，不开Cleartype发虚。微软雅黑的美观度和清晰度都较好，可以作为网页的首选字体。它在Mac平台的对应字体是华文细黑（STXihei）。

- 华文细黑 ：Mac下的默认中文。

- Droid Sans和衍生的WenQuanYi Microhei ：Andriod中的中文，也是Linux绝大多数发行版本的默认中文，，当然也有用WenQuanyi Zenhei的，不过比较少了。


衬线字体

- 中易宋体（SimSun） ：Win最常见的字体，小字体点阵，大字体TrueType，但是大字体并不好看，所以最好别做标题。宋体是最常见的中文字体，如果没有指定字体，操作系统往往选择它来渲染。很多人认为，这种字体并不美观。

- 仿宋（FangSong） ：这种字体是衬线体，比宋体的装饰性更强。如果字号太小，会影响清晰度，所以只有在字号大于14px的情况下，才可以考虑这种字体。它在Mac平台的对应字体是"华文仿宋"（STFangsong）。

- 楷体（KaiTi） ：楷体也是衬线体，装饰性与仿宋体接近，但是宽度更大，笔画更清楚一些。这种字体也不应该在小于14px的情况下使用。它在Mac平台的对应字体是"华文楷体"（STKaiti）。


## 设置字体

由于Windows和Mac的中文字体没有交叉，所以应该同时为两个平台指定字体。

常见的做法是，Windows平台指定"微软雅黑"（Microsoft YaHei），Mac平台指定"华文细黑"（STXihei）。



## 笔记
[[网页中文字体压缩（woff2）、拆分、去繁体字库，提高加载速度]]
[[中文字体压缩的那些事]]