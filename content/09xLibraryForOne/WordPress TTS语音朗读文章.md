以前利用百度语音合成为博客加入朗读文章功能，[给博客添加TTS语音朗读 简单快速版](https://xptt.com/654048.html)，那时候用的人挺多，效果还不错，后来某天再去点，发现已经不行了，意料中的事情！

现在很多TTS合成都开始收费了，最初是微软，科大讯飞，后来是百度语音，腾讯语音，[再后来是Google也有TTS语音合成](http://programmermagazine.github.io/201309/htm/article2.html)，刚开始和百度一样，可以直接通过网址带参数，加个AUDIO标签元件就可以朗读了，后来也都屏蔽不让用了。

再看看华人头条这家国际网站（手机访问，[传送门](http://www.52hrtt.com/mobileview/info?id=D1627287557710&areaId=1&languageId=1&isWei=1)），点击上面的语音听听，有没有被吓到？人家花了钱的语音效果还那么差。

就当我清理以前代码准备放弃的时候，心想又一个3年过去了，WordPress插件开发也应该又多了吧，以前搜过，没找到，这么实用的功能，怎么会没人折腾呢？

于是信心十足的输入TTS关键字一搜，不用看，第一个肯定是大神的插件(SiteSpeaker TTS Plugin)，也一定是最受欢迎或最强的，作者[SiteSpeaker LLC](https://www.sitespeaker.link/)，外国人，很可能没有中文。

抱着试试的心态，没想到看到CN两个字，应该是中文，不过其他都可以点击试听，就中文试听没声音，没事，继续，插件代码一调用，一试，语音效果很满意，而且播放器也很美观，完美！就连前几天发的那篇拔牙4000字文章[那篇拔牙4000字文章](https://xptt.com/656819.html)也毫无压力。

它其实也是Goolge语音合成实现的，突然有点担心你们是否能正常朗读？因为Goolge被墙，可能也是利用翻译朗读的接口，这普通话听起来还不错。

既然是插件，那么使用起来就很简单了，这里简单介绍一下使用方法：

后台插件搜 SiteSpeaker Widget，然后启用。

[![](https://xptt.com/wp-content/uploads/2021/07/ttsreader.png)](https://xptt.com/wp-content/uploads/2021/07/ttsreader.png)

选择CN，然后点击保存，注意我点击试听没声音，不知道你们是不是一样，不用管，忽略。

[![](https://xptt.com/wp-content/uploads/2021/07/tts%E8%AF%AD%E9%9F%B3%E6%9C%97%E8%AF%BB.png)](https://xptt.com/wp-content/uploads/2021/07/tts%E8%AF%AD%E9%9F%B3%E6%9C%97%E8%AF%BB.png)

接着后台主题编辑，直接把代码放入single.php里面，点击保存，大功告成。

PS：如果你想让按钮Listen to this article改成朗读这篇文章，那么你就把SiteSpeaker Widget插件设置里的代码，找到Listen to this article修改成朗读这篇文章。

对了，这插件不是朗读一定流量后收费吧？现在没任何提示，既然也是调用Google的，应该不会收费。

最后，强烈推荐在你的博客加入TTS语音朗读功能，解放读者的眼睛！可以边做事情，边听你的故事！

最近逛了一圈博客，发现更新的人越来越少了，大家且行且珍惜。

PS:经[缙哥哥提醒](https://www.dujin.org/)微软的语音现在确实不那么生硬了，相反听起来好像业内最牛~~ 语音优化得很好！这里不是说微软系统自带的那个（自带的还是很生硬），而是Microsoft Edge浏览器，不过好奇下去下载手机版的Microsoft Edge浏览器，有语音朗读功能，但是不支持中文，换了英文网页，也没法读，对了， 这点Google Chrome浏览器也应该加入google的tts朗读功能啊。