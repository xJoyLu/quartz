author:: DecayQ
source:: [通过 Twitter 卡片分享博客](https://blog.decay.fun/2019/07/25/share-my-blog-by-twitter-card/)
clipped:: [[2022-08-29]]
published:: 

# 通过 Twitter 卡片分享博客

2019-07-25 18:33 | [杂事](https://blog.decay.fun/categories/%E6%9D%82%E4%BA%8B/)[前端](https://blog.decay.fun/categories/%E5%89%8D%E7%AB%AF/)[产品](https://blog.decay.fun/categories/%E4%BA%A7%E5%93%81/)[博客](https://blog.decay.fun/categories/%E4%BA%A7%E5%93%81/%E5%8D%9A%E5%AE%A2/)[HTML](https://blog.decay.fun/categories/%E5%89%8D%E7%AB%AF/HTML/) |  329 字 |  1 分钟

[0条评论 | 0次浏览](https://blog.decay.fun/2019/07/25/share-my-blog-by-twitter-card/#vcomment)

[![](https://blog.decay.fun/2019/07/25/share-my-blog-by-twitter-card/banner.jpg)](https://blog.decay.fun/2019/07/25/share-my-blog-by-twitter-card/banner.jpg)

心血来潮试了试文章页下面的“分享到 Twitter”的按钮，发现分享出去的是干巴巴的文字，觉得不是很美观。虽然没怎么去用 Twitter 但是还是知道在时间线上有不同的推文样式。抱着试试看的心态去找了找，还真找到了：[Twitter Card](https://developer.twitter.com/en/docs/tweets/optimize-with-cards/guides/getting-started.html)。

看上去并不难，只需要在`<head>`中配置一些`<meta>`标签。但是我的博客是用 hexo 生成的，所以用的是 pug 的语法：

meta(name='twitter:card' content='summary_large_image')  
//- 必填，可选 “summary”, “summary_large_image”, “app”, or “player”  
  
meta(name='twitter:site' content='@DecayQ')\  
//- 非必填，在卡片 footer 显示的站点@username  
  
meta(name='twitter:creator' content='@DecayQ')  
//- 非必填，内容创作者@username  
  
meta(name='twitter:title' content=page.title)  
//- 必填，站点标题  
  
meta(name='twitter:image' content='https://blog.decay.fun/:article/banner.jpg')  
//- 非必填，卡片显示的图片  

但是，页面设置完了点击分享仍然是纯文本的样式。在[Stackoverflow](https://stackoverflow.com/questions/21478891/twitter-card-share-button)找到了答案：需要去 Twitter 的[卡片验证器](https://cards-dev.twitter.com/validator)地址验证网址即可：

![](https://blog.decay.fun/2019/07/25/share-my-blog-by-twitter-card/validator.png)

之后，通过分享地址：`//twitter.com/intent/tweet?text=title&url=url`即可跳转到相对应的页面，点击分享后时间线上出现的就是选择的卡片模式了。

以上。