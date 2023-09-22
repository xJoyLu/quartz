author:: 雨临Lewis
source:: [docsify快速入门](https://lewky.cn/posts/docsify-0.html/)
clipped:: [[2022-09-27]]
published:: 

# docsify快速入门

[雨临Lewis](https://lewky.cn/ "Author") 收录于 [Blog](https://lewky.cn/categories/blog/)

 2021-03-01  2021-05-18  约 2418 字  预计阅读 5 分钟  678 次阅读   [1 条评论](https://lewky.cn/posts/docsify-0.html/#comments "查看评论")

## [](https://lewky.cn/posts/docsify-0.html/#docsify)docsify

根据官方说法，docsify是一个神奇的文档网站生成工具，也可以把它当做一个简易版的静态站点诸如Hexo、Hugo等。当然，它是专门针对文档的，忽然想到了程序员深恶痛绝的就是写API文档……

docsify特性很多，最吸引我的是全文搜索、主题简洁好看、无需构建的纯静态站点。这意味着可以很简单地把写完的文档直接扔到Pages服务上，比如GitHub Pages、Coding Pages等等。

## [](https://lewky.cn/posts/docsify-0.html/#%E5%BF%AB%E9%80%9F%E5%AE%89%E8%A3%85)快速安装

首先需要先安装npm，这个请自行解决。

然后用npm来全局安装docsify：

```
1
```

```fallback
npm i docsify-cli -g
```

## [](https://lewky.cn/posts/docsify-0.html/#%E7%AE%80%E6%98%93%E6%90%AD%E5%BB%BA)简易搭建

### [](https://lewky.cn/posts/docsify-0.html/#%E5%88%9D%E5%A7%8B%E5%8C%96)初始化

创建一个文档站点目录，比如`note`目录，然后在该目录下执行命令：

```
1
```

```fallback
docsify init ./docs
```

然后docsify会在该目录下新建一个`docs`目录，里面有3个初始文件：

-   `.nojekyll`：告诉GitHub Pages服务该站点不使用`Jekyll`作为构建工具
-   `index.html`：入口文件
-   `README.md`：作为首页渲染

请尽量使用`docs`目录来初始化docsify，原因是后面要用该目录部署到GitHub Pages。

### [](https://lewky.cn/posts/docsify-0.html/#%E6%9C%AC%E5%9C%B0%E9%A2%84%E8%A7%88%E4%B8%8E%E5%AE%9E%E6%97%B6%E6%9B%B4%E6%96%B0)本地预览与实时更新

使用如下命令可以本地预览站点：

```
1
```

```fallback
docsify serve docs
```

然后就可以通过`http://localhost:3000/`来访问你的文档站点。

docsify支持实时更新，可以在启动本地服务时自动重新加载刚刚更新的文件。

## [](https://lewky.cn/posts/docsify-0.html/#%E5%B8%B8%E7%94%A8%E9%85%8D%E7%BD%AE)常用配置

### [](https://lewky.cn/posts/docsify-0.html/#%E7%AB%99%E7%82%B9%E6%A0%87%E9%A2%98%E5%9B%BE%E6%A0%87)站点标题、图标

站点标题需要修改`index.html`里的`title`标签：

```
1
```

```fallback
<title>Java-Note</title>
```

站点图标要在`index.html`添加如下代码：

```
1
```

```fallback
<link rel="icon" href="//cdn.jsdelivr.net/gh/lewky/lewky.github.io@master/images/avatar.jpg">
```

### [](https://lewky.cn/posts/docsify-0.html/#%E4%B8%BB%E9%A2%98%E9%80%89%E6%8B%A9)主题选择

docsify提供了多款主题，通过修改`index.html`里的css地址即可更换主题：

```
1
```

```fallback
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify@4/lib/themes/vue.css">
```

还有以下的主题可以挑选，有遗漏的可以帮忙补充下：

```
1
2
3
4
5
6
7
8
9
```

```fallback
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify@4/lib/themes/vue.css">
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify@4/lib/themes/buble.css">
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify@4/lib/themes/dark.css">
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify@4/lib/themes/pure.css">
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify@4/lib/themes/dolphin.css">

<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/docsify-themeable@0/dist/css/theme-defaults.css">
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/docsify-themeable@0/dist/css/theme-simple.css">
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/docsify-themeable@0/dist/css/theme-simple-dark.css">
```

### [](https://lewky.cn/posts/docsify-0.html/#github-corner)Github Corner

`index.html`里有个脚本代码如下：

```
1
2
3
4
5
6
```

```fallback
  <script>
    window.$docsify = {
      name: '',
      repo: ''
    }
  </script>
```

name会作为标题显示在站点的侧边栏，repo会作为Github Corner显示在站点的右上角，点击可跳转到对应的地址。样例如下：

```
1
2
3
4
5
6
```

```fallback
  <script>
    window.$docsify = {
      name: 'Java-Note',
      repo: 'https://github.com/lewky'
    }
  </script>
```

### [](https://lewky.cn/posts/docsify-0.html/#coverpage%E5%B0%81%E9%9D%A2)coverpage封面

该参数可以给站点添加一个封面，如下：

```
1
2
3
4
5
6
7
```

```fallback
  <script>
    window.$docsify = {
      name: 'Java-Note',
      repo: 'https://github.com/lewky',
      coverpage: true
    }
  </script>
```

封面由`_coverpage.md`来渲染，默认无该文件需自行创建，内容如下：

```
1
2
3
4
5
6
7
8
9
```

```fallback
![logo](https://docsify.js.org/_media/icon.svg)

# Java笔记

> 个人向的Java学习笔记

* 贵在坚持

[开始阅读](/README)
```

### [](https://lewky.cn/posts/docsify-0.html/#loadnavbar%E5%AF%BC%E8%88%AA%E6%A0%8F)loadNavbar导航栏

该参数用于添加导航栏，如下：

```
1
2
3
4
5
6
7
```

```fallback
  <script>
    window.$docsify = {
      name: 'Java-Note',
      repo: 'https://github.com/lewky',
      loadNavbar: true
    }
  </script>
```

同样需要新建文件`_navbar.md`，内容如下：

```
1
2
3
```

```fallback
* [Home](/)
* Links
    * [CS-Notes](http://cyc2018.gitee.io/cs-notes/#/README)
```

### [](https://lewky.cn/posts/docsify-0.html/#loadsidebar%E4%BE%A7%E8%BE%B9%E6%A0%8F)loadSidebar侧边栏

该参数用于添加侧边栏，如下：

```
1
2
3
4
5
6
7
```

```fallback
  <script>
    window.$docsify = {
      name: 'Java-Note',
      repo: 'https://github.com/lewky',
      loadSidebar: true
    }
  </script>
```

同样需要新建文件`_sidebar.md`，内容如下：

```
1
2
3
```

```fallback
* [简介](/)
* 数据结构
  * [数组](data-structure/array/)
```

个人不建议用这个参数，docsify默认会帮你生成侧边栏，并且有目录效果，可以点击跳转。

### [](https://lewky.cn/posts/docsify-0.html/#%E5%85%A8%E6%96%87%E6%90%9C%E7%B4%A2%E6%8F%92%E4%BB%B6)全文搜索插件

docsify提供了一些插件，包括全文搜索等，可以通过该地址查询有哪些插件：https://cdn.jsdelivr.net/npm/docsify@4.12.0/lib/plugins/

对于全文搜索插件，需要在`index.html`里添加search属性以及JavaScript，官方提供的搜索插件好像有点问题，这里用的是其他的搜索插件。如下：

```
 1
 2
 3
 4
 5
 6
 7
 8
 9
10
11
12
13
14
```

```fallback
  <script>
    window.$docsify = {
      name: 'Java-Note',
      repo: 'https://github.com/lewky',
	  search: {
		maxAge: 86400000, // Expiration time, the default one day
		paths: 'auto',
		placeholder: '🔍 Type to search ',
		noData: '😞 No Results! ',
		depth: 6
	  }
    }
  </script>
  <script src="//cdn.bootcss.com/docsify/4.5.9/plugins/search.min.js"></script>
```

目前似乎高于`4.5.9`版本的搜索插件有bug，只能搜索到首页的数据；建议使用该版本的搜索插件。

此外，使用了无序列表或者有序列表的数据是无法生成对应索引的，也就是说搜索插件无法搜索到列表里的数据。建议尽量别使用列表语法，可以改用特殊符号`●`、罗马数字`ⅠⅡⅢⅣⅤⅥⅦⅧⅨ`和换行符`<br>`来代替列表语法。

## [](https://lewky.cn/posts/docsify-0.html/#%E5%9B%9E%E5%88%B0%E9%A1%B6%E9%83%A8%E6%8F%92%E4%BB%B6)回到顶部插件

在`index.html`引入脚本和参数配置：

```
 1
 2
 3
 4
 5
 6
 7
 8
 9
10
11
12
13
14
```

```fallback
  <script>
    window.$docsify = {
      name: 'Java-Note',
      repo: 'https://github.com/lewky',
	  scrollToTop: {
        auto: true,
        text: 'Top',
        right: 15,
        bottom: 15,
        offset: 300
      }
    }
  </script>
  <script src="//unpkg.com/docsify-scroll-to-top/dist/docsify-scroll-to-top.min.js"></script>
```

参数配置有默认值，不配也可以，一共就这几个属性，可以自己随意定制。

## [](https://lewky.cn/posts/docsify-0.html/#%E4%BB%A3%E7%A0%81%E9%AB%98%E4%BA%AE%E6%8F%92%E4%BB%B6)代码高亮插件

在`index.html`引入脚本，可以根据需要引入对应的语言高亮脚本：

```
1
2
3
4
```

```fallback
<script src="//cdn.jsdelivr.net/npm/prismjs@1.22.0/components/prism-java.min.js"></script>
<script src="//cdn.jsdelivr.net/npm/prismjs@1.22.0/components/prism-bash.min.js"></script>
<script src="//cdn.jsdelivr.net/npm/prismjs@1.22.0/components/prism-c.min.js"></script>
<script src="//cdn.jsdelivr.net/npm/prismjs@1.22.0/components/prism-sql.min.js"></script>
```

## [](https://lewky.cn/posts/docsify-0.html/#%E5%A4%8D%E5%88%B6%E4%BB%A3%E7%A0%81%E5%9D%97%E6%8F%92%E4%BB%B6)复制代码块插件

在`index.html`引入脚本和参数配置：

```
 1
 2
 3
 4
 5
 6
 7
 8
 9
10
11
12
```

```fallback
<script>
	window.$docsify = {
	  // docsify-copy-code (defaults)
	  copyCode: {
	    buttonText : 'Copy to clipboard',
	    errorText  : 'Error',
	    successText: 'Copied'
	  }
	}
</script>

<script src="//unpkg.com/docsify-copy-code@2.1.1/dist/docsify-copy-code.min.js"></script>
```

参数配置有默认值，可以不配置直接引入脚本即可使用。

## [](https://lewky.cn/posts/docsify-0.html/#%E5%9B%BE%E7%89%87%E7%BC%A9%E6%94%BE%E6%8F%92%E4%BB%B6)图片缩放插件

在`index.html`引入脚本即可：

```
1
```

```fallback
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/zoom-image.min.js"></script>
```

## [](https://lewky.cn/posts/docsify-0.html/#%E6%B7%BB%E5%8A%A0fontawesome)添加`fontawesome`

可以通过引入`fontawesome`来使用各种免费的矢量图标来丰富页面内容：

```
1
```

```fallback
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fortawesome/fontawesome-free@5.13.0/css/all.min.css">
```

用法很简单，就是使用`<i>`标签来引入，而markdown兼容html代码，如下：

```
1
```

```fallback
<i class="fas fa-fw fa-home"></i>
```

还有其他的动态图用法等，网上教程很多，这里就不赘述了。

## [](https://lewky.cn/posts/docsify-0.html/#plantuml%E6%8F%92%E4%BB%B6)PlantUML插件

在`index.html`引入脚本即可：

```
1
```

```fallback
<script src="//unpkg.com/docsify-plantuml/dist/docsify-plantuml.min.js"></script>
```

默认主题是`default`，也可以配置成`classic`：

```
1
2
3
4
5
6
7
```

```fallback
<script>
window.$docsify = {
  plantuml: {
    skin: 'classic',
  }
}
</script>
```

## [](https://lewky.cn/posts/docsify-0.html/#%E8%BF%9C%E7%A8%8B%E9%83%A8%E7%BD%B2%E5%88%B0pages%E6%9C%8D%E5%8A%A1)远程部署到Pages服务

`GitHub Pages`支持从三个地方读取文件：

-   `docs`目录
-   `main`分支（以前是叫master分支）
-   `gh-pages`分支

master分支一般用于个人站点，gh-pages分支需要另外创建一个新的分支（默认GitHub仓库创建的是master分支），对于文档站点，建议直接使用`docs`目录来部署，这也是前文为什么建议用docs目录进行初始化的原因。

将文档站点推送到GitHub仓库后，在`Settings`里选择使用`main branch`和`/docs`进行部署即可。

## [](https://lewky.cn/posts/docsify-0.html/#%E5%8F%82%E8%80%83%E9%93%BE%E6%8E%A5)参考链接

-   [docsify官方文档](https://docsify.js.org/#/?id=docsify)
-   [docsify 入坑指南与我放弃 Gitbook 的那些理由](https://zhuanlan.zhihu.com/p/70219397)
-   [有了docsify神器，从此爱上看文档](https://www.jianshu.com/p/4883e95aa903)
-   [关于写作那些事之github告诉我构建失败,然后呢?](https://blog.csdn.net/weixin_38171180/article/details/89227515)
-   [docsify-scroll-to-top](https://www.npmjs.com/package/docsify-scroll-to-top)
-   [入坑 docsify，一款神奇的文档生成利器！](https://baijiahao.baidu.com/s?id=1683928475208184783&wfr=spider&for=pc)

警告

本文最后更新于 May 18, 2021，文中内容可能已过时，请谨慎使用。