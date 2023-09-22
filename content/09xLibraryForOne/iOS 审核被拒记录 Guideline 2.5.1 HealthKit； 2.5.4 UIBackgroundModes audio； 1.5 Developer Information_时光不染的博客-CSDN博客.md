author:: null
source:: [iOS 审核被拒记录 Guideline 2.5.1 HealthKit； 2.5.4 UIBackgroundModes audio； 1.5 Developer Information_时光不染的博客-CSDN博客](https://blog.csdn.net/hzhnzmyz/article/details/120024604)
clipped:: [[2022-06-28]]
published:: 

#iOS #审核

![](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[时光不染](https://blog.csdn.net/hzhnzmyz) ![](https://csdnimg.cn/release/blogv2/dist/pc/img/newCurrentTime2.png) 于 2021-09-05 15:03:36 发布 ![](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes2.png) 899 ![](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect2.png) 收藏  6 

版权声明：本文为博主原创文章，遵循 [CC 4.0 BY-SA](http://creativecommons.org/licenses/by-sa/4.0/) 版权协议，转载请附上原文出处链接和本声明。

### iOS 审核被拒记录 2.5.1

Guideline 2.5.1 - Performance - Software Requirements  
Your app uses the HealthKit or CareKit APIs but does not indicate integration with the Health app in your app description and clearly identify the HealthKit and CareKit functionality in your app's user interface.  
Next Steps  
To resolve this issue, please revise your app description to specify that your app integrates with the Health app.

您的应用程序使用HealthKit或CareKit [API](https://so.csdn.net/so/search?q=API&spm=1001.2101.3001.7020)，但未在应用程序说明中指明与健康应用程序的集成，并在应用程序的用户界面中明确标识HealthKit和CareKit功能。  
若要解决此问题，请修改你的应用程序描述，以指定你的应用程序与健康应用程序集成。

以上内容的意思大致是，使用了HealthKit 或CareKit框架，但是在应用中看不到你在哪用了。

#### 解决方案一（当前项目不需要HealthKit框架,将HealthKit相关内容和权限移除）

正如我自己的项目，一开始准备用HealthKit获取玩家运动步数，尝试后发现CoreMotion更方便好用，而且只要在配置表配置权限就可以。  
 

检查是否完全移除HealthKit相关权限的位置  
1.移除Identifiers里相关的权限  
[https://developer.apple.com/account/resources](https://developer.apple.com/account/resources)  
![](https://img-blog.csdnimg.cn/fb25acc2518b479e86ae084f698e637c.png)  
![](https://img-blog.csdnimg.cn/8aaf85c47a87497982a31265ea642fe0.png)

2.info.plist移除相关键值对  
![](https://img-blog.csdnimg.cn/f6d973ce36af49b7923e4efc04791a30.png)

3.移除Signing&Capabilities里的HealthKit

![](https://img-blog.csdnimg.cn/8928e621baa6490ea12658723f80b34d.png)

4.检查是否有文件引用Health.kit  
全局搜索import HealthKit 并移除

5.检查FrameWork文件夹是否有HealthKit.FrameWork留存

![](https://img-blog.csdnimg.cn/63c02946b0c74df484ce94f678fada6e.png)

6.如果是有小组件等子项目，第1 ，2，3条在子项目也查一下

#### 解决方案二（当前项目需要HealthKit框架）

如果框架能正常使用，出现上述问题，说明审核人员找不到你在哪里使用了HealthKit相关内容。下次提审备注并最好提交一份使用位置的录屏，类似下面的2.5.4的做法

### iOS 审核被拒记录 2.5.4

Guideline 2.5.4 - Performance - Software Requirements  
Your app declares support for audio in the UIBackgroundModes key in your Info.plist but did not include features that require persistent audio.  
Next Steps  
The audio key is intended for use by apps that provide audible content to the user while in the background, such as music player or streaming audio apps. Please revise your app to provide audible content to the user while the app is in the background or remove the "audio" setting from the UIBackgroundModes key.

您的应用程序在Info.plist的UIBackgroundModes键中声明支持音频，但不包括需要持久音频的功能。  
音频键用于在后台向用户提供音频内容的应用程序，如音乐播放器或流媒体音频应用程序。请修改应用程序，以便在应用程序处于后台时向用户提供音频内容，或从UIBackgroundModes键中删除“音频”设置。

以上内容的意思大致是，在info.plist 里声明了使用音频的后台播放权限，但是在应用中看不到你在哪用了。

我当前项目使用了画中画做的新手引导，在App切到后台时，引导视频依然能播放，但是审核人员大概没测到，所以需要在下次提审时给备注，或者发邮件提醒

![](https://img-blog.csdnimg.cn/4a499d42bb7341ac90639742481f5e31.png)

### iOS 审核被拒记录 1.5

The support URL specified in your app’s metadata, https://appgame-xxxxxx.html, does not properly navigate to the intended destination.  
Next Steps  
To resolve this issue, please revise your app’s support URL to ensure it directs users to a webpage with support information.

应用程序元数据中指定的支持URL，https://appgame-xxxx.html，无法正确导航到预期目标。  
要解决此问题，请修改应用程序的支持URL，以确保它将用户引导到包含支持信息的网页。

以上内容的意思大致是，你填写的技术支持网站没有能联系到你的方式。  
在技术支持网站填上邮箱和电话就可以了。  
如果没有技术支持网站，可以通过微博、简书、公众号等这些能够发布文章的平台，写一篇文章，把文章链接填上去即可。文章内容，主要是有联系信息，其他的可以写点产品的介绍，产品截图等。