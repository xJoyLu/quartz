Obsidian Minimal主题的作者 [@kepano](https://twitter.com/kepano) 分享了一个网页抓取 js 脚本，抓取网页内容的效果非常赞，使用方式也很简单，整理出来分享给大家。

-   随便添加一个书签，例如：Clipper
-   在标签上右键「编辑地址...」
-   输入 js 脚本的代码内容保存
-   使用时，打开网页、或者选中网页中的内容点击这个标签即可

![](https://pepcn.com/GTD/_image/2021-08-10/CleanShot%202021-08-10%20at%2016.39.18@2x.png?c=1)JS 代码的下载可以访问作者的 GitHub [obsidian-web-clipper.js](https://gist.github.com/kepano/90c05f162c37cf730abb8ff027987ca3#file-obsidian-web-clipper-js) 。建议将代码复制到本地，粘贴到编辑器修改其中的 库名称、笔记存储位置以及标签名称。例如我的库名称是 Document、打算将剪藏的网页内容保存到 稍后阅读 文件夹，添加标签 #稍后阅读。![](https://pepcn.com/GTD/_image/2021-08-10/CleanShot%202021-08-10%20at%2016.45.51@2x.png)修改好的代码可以利用 [Bookmarklet Maker](https://caiorss.github.io/bookmarklet-maker/) 网站转换成书签形态。

1.  访问 Bookmarklet Maker 网站，粘贴代码到 Code 区域
2.  点击 Generate Bookmarklet 按钮
3.  复制 Output 中的内容，编辑上面创建的 Clipper 的书签粘贴进去保存即可。

![](https://pepcn.com/GTD/_image/2021-08-10/CleanShot%202021-08-10%20at%2016.49.55@2x.png) 最后来看看抓取效果，有 YAML 的类别记录，网页中的代码抓取和还原不错，不过表格好像还不行。 ![](https://pepcn.com/GTD/_image/2021-08-10/CleanShot%202021-08-10%20at%2016.59.11@2x.png)