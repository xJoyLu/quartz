author:: null
source:: [如何让你的 Windows 变得 mac 里 mac 气](https://m.ithome.com/html/557239.htm)
clipped:: [[2022-06-28]]
published:: 

#稍后阅读 #美化

前段时间，极客之选推出了《[让你的笔记本用上「鸿蒙系统」多屏协同](https://www.ithome.com/0/556/476.htm)》的教程，大家试过之后表示非常实用，体验也很不错，而且有些朋友在台式机上也测试成功了，当然前提是支持 WiFi 6 网卡和蓝牙。另外，随着鸿蒙百机升级计划的实施，以后支持「多屏协同」的设备也会更多，如果你手中正好有一部，只是目前还不能升级的话，不妨先收藏下我们的教程，到时候再体验也不迟。

上篇教程中，很多朋友发现我用的 Windows 10 系统有着像 macOS 一样的外观和体验，看着令人赏心悦目，并表示自己也需要这样的主题，所以在今天这篇文章中我们立刻安排，而且不只是简单的外观模仿，还要在使用体验方面吸取 macOS 的优点。

Windows 系统的美化，其实是个老生常谈的话题，多年前我就研究过 XP 系统如何用上 Win7 的毛玻璃主题，那时 Win7 的设计和毛玻璃特效的确非常精致，而同期的 macOS 还远没有现在漂亮。然而，自从 Win10 之后，微软的审美就以肉眼可见的速度在下降，如今，使用预览版 Win10 系统的我，在看到五颜六色的资源管理器图标后，已经对过段时间的 Win10 太阳谷更新不抱什么期待了…… 我们还是先来看看如何用上 macOS 主题吧。

![](https://img.ithome.com/newsuploadfiles/2021/6/bc64420a-0eb8-4dce-ab37-410999893a3d.png)

▲Win 10 预览版新图标风格

**设备要求**

-   屏幕  分辨率最好支持 2K 及以上
    
-   系统  推荐 Win10 20H2 版本
    

**Mac 套件包括**

-   MyDockFinder 启动器、天气插件
    
-   macOS Monterey 以及 BigSur 壁纸
    
-   4 款无衬线字体（鸿蒙字体、OPPO Sans、思源黑体、苹方）
    
-   Quicklook 快速预览
    
-   Wox 搜索
    

PC 上模仿 macOS 的启动器有很多，我之前用过几款，但都不够精致，功能也不齐全，无法完全替代 Windows 桌面使用，直到我发现了 MyDockFinder。MyDockFinder 可能是目前最精致的 macOS 启动器，同时也是功能最强大、完成度最高的一款。它由一位国产开发者打造，目前还在持续更新中，最新版本为 5.9.9.8（2021.06.14 更新），希望不久后的 6.0 版本能带来更好的体验。

过去的一周里，我一直把 MyDockFinder 当作主力桌面使用，绝大多数情况下可以满足我的使用需求，接下来就把它的安装过程和我的配置方法介绍给大家。

百度网盘下载链接：https://pan.baidu.com/s/1HVKE5lpSLazGmIQPe\_CYKA  密码：ucv6

天翼网盘下载链接：https://cloud.189.cn/t/NNNn6j7rEz2u 访问码：ln8g

MyDockFinder 官网：https://www.mydockfinder.com/

## 配置 MyDockFinder 启动器

**Step 1 安装 MyDockFinder**

1\. 直接把「Mac 套件」中的「MyDock」解压即可，注意不要解压到 C 盘下，不然可能会无法运行（也许是我的个例问题）

2\. 解压后，打开目录下的「Dock\_64.exe」，你会发现你的 Windows 桌面上多了一层 macOS 主题。如无法运行，可能是缺少运行库等，可以在官网寻找对应的解决方案。

![](https://img.ithome.com/newsuploadfiles/2021/6/9d0ed81e-e969-48fa-82bd-86a9369c5867.png)

**Step 2 配置 MyDockFinder**

少啰嗦，先看东西！

![](https://img.ithome.com/newsuploadfiles/2021/6/2056f090-e964-404e-9522-8ba0af72b8ca.png)

▲配置前 不伦不类的杂交桌面

![](https://img.ithome.com/newsuploadfiles/2021/6/7b927e7f-532f-417e-b603-51cb4b1f53df.png)

▲粗略配置后 稍显精美的 macOS 风格

![](https://img.ithome.com/newsuploadfiles/2021/6/18039eb9-595c-4a95-a1e8-f1ecccfd2e79.gif)

▲完全配置后 以假乱真（请忽略右下角预览版系统水印）

**风险提示 & 解决方法：**

如在配置过程中，遇到 MyDockFinder 无法启动、Windows 资源管理器也无法打开的情况，通俗点说就是桌面上除了壁纸什么也没有的时候，按下 Ctrl+Shift+Esc 调出任务管理器，选中 Windows 资源管理器重启，或者找到 dock 结束进程即可恢复正常。

![](https://img.ithome.com/newsuploadfiles/2021/6/bc3bdf37-7dbd-4e6c-b32b-c64008d7b446.jpg)

配置 MyDockFinder 非常简单，遵循一个原则即可 —— 隐藏 Windows 的一切痕迹。大家其实也可以自己研究，以下是我粗略的配置方法，仅供参考。

1\. 隐藏桌面图标、换一张 macOS 风格壁纸（「Mac 套件」中即可获取），可以直接起到事半功倍的效果

2\. 在 MyDockFinder 标题栏中，打开「访达 - 偏好设置 - 全局设置」，勾选「启动时自动隐藏任务栏」，这样 Dock 栏和 Windows 的任务栏就不会重叠了。需要注意的是，任务栏被隐藏后，搜索和多窗口切换可能会不方便，但其实我们还可以用快捷键 Win+S 和 Alt+Tab (Win+Tab) 替代。另外，快捷键 Win+E 可以打开我的电脑

3\. 打开「访达 - 偏好设置 - 通用」，对图标大小和间距进行调整，不同显示器的设置不同，大家按照实际观感调整即可（怎么像怎么来）

PS：每次配置需要重启启动器，按照「访达 - 偏好设置 - 关于 - 重启程序」操作即可

**Step 3 选择一个合适的字体**

大家都知道，macOS 的字体效果比 Windows 出色很多。究其原因，除了 macOS 在字体渲染方面的优势外，还与 Mac 设备几乎都是高分屏也有很大关系。在 MyDockFinder 中，高分屏同样也能带来更好的效果。

另外，MyDockFinder 的默认字体不太精致，在这里给大家推荐几款无衬线字体，非常适合显示使用。字体文件在「Mac 套件」中即可获取。PS：以下字体除了苹方外，均可免费商用。

![](https://img.ithome.com/newsuploadfiles/2021/6/9c8d9209-c7bd-4325-b4bf-8056917449cc.png)

在「访达 - 偏好设置 - 全局设置」中即可修改字体

1\. 苹方：macOS 默认字体，还你原汁原味的苹果风

2\. HarmonyOS Sans：华为鸿蒙系统默认字体，效果也很不错

3\. OPPO Sans：OPPO ColorOS 默认字体，很有设计感

4\. 思源黑体：Google 和 Adobe 联合开发的一款经典黑体

**Step 4 一些细节**

1\. 统一图标风格：常用应用可以直接拖入 Dock 栏，在 Dock 栏图标上执行「右键 - 设置此图标 - 使用图标遮罩 - 重置 - 确定」操作，即可把图标统一为圆角矩形风格

![](https://img.ithome.com/newsuploadfiles/2021/6/d0a66046-dbba-41c4-8b69-b056ac79af73.gif)

2\. 亮度音量调节样式：「访达 - 偏好设置 - 声音 - Mac 样式」

![](https://img.ithome.com/newsuploadfiles/2021/6/6614b582-d5f2-4155-a6b3-2bb80cfe2ffe.gif)

3\. 标题栏字体颜色：个人觉得黑色显得更像 Mac，可以在「访达 - 偏好设置 - 通用」中设置

4\. 标题栏网速：网速监控是很实用的功能，可以在「访达 - 偏好设置 - 监控」中开启

5\. 天气插件：1. 将「Mac 套件」中的「weather」文件夹复制到 MyDockFinder 安装目录下 2. 在 Dock 栏空白处「右键 - 添加系统图标 - 天气预报」即可添加天气图标

![](https://img.ithome.com/newsuploadfiles/2021/6/ccdd0df8-df0b-4b42-8a2e-ea993235e3cb.gif)

6\. 你甚至可以把常用软件拖到「启动台」中

![](https://img.ithome.com/newsuploadfiles/2021/6/520c3a99-433a-410f-a889-bd7344dd0e10.gif)

7\. 更多细节等你挖掘……

## 一些 Mac 上的效率软件

Mac 上有很多使用的效率工具，比如按下空格快速预览、还有 Command + Space 打开 SpotLight 搜索。在 Windows 中你可以安装 Quicklook 和 Wox 进行替代，但我实际使用后发现体验并不是特别好，比如 Quicklook 无法预览 Office 文件，Wox 的查找也不是特别精准。

![](https://img.ithome.com/newsuploadfiles/2021/6/76503ee5-78ad-4e86-822c-3593b10e4b6a.gif)

▲Quicklook 预览 PDF 文档

如果大家有兴趣的话可以自己折腾，我们在「Mac 套件」里同样提供了最新版 Quicklook 和 Wox 的安装包。

关于 Windows 和 macOS 的孰优孰劣的讨论从未停止，Windows 的优势在于数不尽的软件和游戏支持、高效率的多窗口操作、开放且强大的文件管理，这也是其自诞生以来的传统优势，是无数用户所说的“生产力”。而 macOS 虽然也有悠久的历史，但如今的它明显更像是新生代操作系统，它的外观界面、交互设计、多平台融合能力远强于 Windows，使用上也更人性化，再加之 iOS 移动生态的神助攻，让它的竞争力越来越强，不知道过段时间的 Win10 太阳谷会如何应对。如果有一天，Windows 也能拿出一套独具特色的全新交互界面，相信大家就不用大费周折搞一套「Mac 皮」了。