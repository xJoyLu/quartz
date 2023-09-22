## 写在前面

Apple 在今年10月28日的时候发布了 [In-App Purchase Promo Codes](https://link.juejin.cn?target=https%3A%2F%2Fdeveloper.apple.com%2Fnews%2F%3Fid%3D10282016a "https://developer.apple.com/news/?id=10282016a") ，也就意味着「免费+ 内购」的 App也可以通过 Promo Codes 去搞促销活动了。

目前总共允许开发者创建 1000个兑换码，每个内购项目是 100个，正好赶在双十一来临，我就尝试了下内购兑换码如何进行营销活动的整个流程，所以在[浪潮官方微博](https://link.juejin.cn?target=http%3A%2F%2Fweibo.com%2F523432897 "http://weibo.com/523432897")里发起了「转发抽奖免费浪」赠送 100个1GB 流量兑换码活动，活动微博[见这里](https://link.juejin.cn?target=http%3A%2F%2Fweibo.com%2F1748232285%2FEh53lb0n2 "http://weibo.com/1748232285/Eh53lb0n2")。

## 创建兑换码

-   登录 iTunes Connect，点击「我的 App」；
-   点开 App进入详情后选择「功能」-「促销代码」；
-   输入内购需要生成代码的个数，点击「生成代码」-「完成」；
-   下载 Promo Codes.text 即可，之后也可以在「历史记录」里查看；

![](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2016/11/29/e887855e5a4979133c2588a185a96f57~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)

## 导入兑换码

发布转发抽奖的微博后，设定的目标是截止双十一晚上11点11分进行抽奖，但是只有 52个转发，所以只需要导入 52个兑换码就可以，这样确保人人有码。新浪微博抽奖程序对于「虚拟奖品-兑换码」的支持还是不错的，只需要导入 text文件，每个兑换码一行就可以，微博会按实际导入数量发放。点击抽奖后就会以一条公开微博和私信的方式发送给用户，确保公正性。

![](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/leancloud-assets/48d6cac3d429039f7524.png~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)

## 用户如何兑换

-   打开 App Store，第一个 Tab精品推荐拉到底，选择「兑换」；
-   手动输入通过私信获得的兑换码；
-   兑换成功后再回到对应的 App 里；
-   需要点击一下 App 里的内购项目去请求苹果服务器，等待一会儿；
-   再刷新界面就是可以看到实际兑换的效果；

![](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/leancloud-assets/a09792b0b93c758ab144.PNG~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)

## 验证是否被使用

其实很多开发者在做促销活动时都会遇到一个问题，就是不知道发放出去的兑换码有没有被真正使用，不然会浪费很多码出去。比如我这次尝试的活动，微博最终转发是 75次，阅读 15658次，我中间抽了两次奖，因为第一次使用微博抽奖程序有点陌生，有用户可能获得了 2个兑换码，最终发放出去 61个兑换码，可惜 iTunes Connect里还没法显示对应的 Promo Codes 有没有被兑换，所以为了验证是否有被浪费，目前剩下的唯一方式就是手动 Check。

-   Mac 里打开 iTunes，先帐户退出登录，关闭 iTunes；
-   重新打开 iTunes，帐户登录，然后选择「帐户」-「兑换」；
-   手动复制粘贴你想验证的兑换码；
-   如果提示「此代码已兑换」那就是已被使用，提示「此代码必须在 iOS 设备上兑换」说明这些 Promo Codes 是还有效的，还可以继续用到下次的促销活动；

![](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/leancloud-assets/691c18606bf96160b79d.png~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)

  
作者：Allen朝辉  
链接：https://juejin.cn/post/6844903453492248589  
来源：稀土掘金  
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。