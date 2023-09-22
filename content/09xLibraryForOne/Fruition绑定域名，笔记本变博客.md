author:: null
source:: [Notion建站 | Fruition绑定域名，笔记本变博客 | TANGLY’s BLOG](https://tangly1024.com/article/fruition-notion)
clipped:: [[2022-06-29]]
published:: 

#稍后阅读

CloudFlare+Fruition绑定Notion域名，将notion笔记变成自己的独立博客站点，并解决xxx.notion.site的域名无法访问的问题。https://fruition.tangly1024.com

## [](#ad3d88c67eca46a48c50b86d8578b948 "前言")前言

你是否也想要搭建一个博客，然后专注于写作。但碍于网站建设的技术门槛、又或者登录CSDN、Wordpress这类博客平台的步骤繁杂，导致你最后没能坚持这个写作的习惯。

这套方案让你像在写日记一样，写作发布自己的博客网站，分享有趣的内容，让更多的人关注到你。搭建的速度相当快，我的网站搭建效果如下：

![Fruition Notion 的博客页面](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F8ff3ab27-d099-4bac-b427-8d774b323dcb%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D8c03b4b634fd5f8307b607f0cafa3b7d0ecb371da42be4016e3ae08161e50b17%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=d7f89daf-8919-4324-8442-6f74b5ece090&cache=v2)

Fruition Notion 的博客页面

### [](#7a21bc94b05a439eb06e9f1ef7093176 "方案特点")方案特点

-   页面排版完全自定义，依托于Notion强大的模板功能，Block嵌套功能，你可以实现多种页面布局方式。

-   Notion在网页端、APP端的编辑效果是实时同步的，你在Notion中编辑你的笔记本时，这个博客网站的内容也会实时同步。

-   省钱：不用自己购买服务器，只需要购买一个域名（当然也可以购买免费的），也可以直接使用Notion自带的访问域名。例如我的notion自带域名，然而有时候这个域名会无法访问。（[https://tanghh.notion.site/tangly1024-tk-fcd673e000e74bb79667918f94eed2d8](https://tanghh.notion.site/tangly1024-tk-fcd673e000e74bb79667918f94eed2d8)）

## [](#90a7c5eb349048149b186f9853e7b014 "自定义域名绑定Notion")自定义域名绑定Notion

这里可以通过 Fruition + CloudFlare Workers的方式，将Notion的分享域名 [xxx.notion.site](http://xxx.notion.site/) 转发到你的自定义域名上。

### [](#8d30c96adc0344e6be2de3eba0509de1 "工具介绍")工具介绍

-   [Notion](https://www.tangly1024.com/article/notion)： 由国外华人团队开发的，（应该是）最强笔记软件，并支持将笔记页面分享到网上。

-   [CloudFlare](https://www.cloudflare.com/zh-cn/) ：提供专业的域名托管、反向代理、CDN加速、免费的SSL证书等网络服务，借助它我们可以快速地将我们的网站发布到全球各地。并支持执行Javascript脚本（Workers机制）,借助这一机制，我们可以在用户访问的URL地址上实时渲染内容。

-   [Fruition](https://fruitionsite.com/771ef38657244c27b9389734a9cbff44): 一段简短开源的JavaScript脚本，借助CloudFlare的Workers机制，在用户访问域名时，将域名内容映射到对应的Notion笔记页面。

## [](#09c520cdbc4747fabc860e34ac326ecd "操作步骤")操作步骤

#### [](#9f6e1ff0692d4941b4a7107a9a5c173a "Step 0: 准备域名")Step 0: 准备域名

1.  在您想要公开访问的页面上启用“公开访问权限”，也就是 Share On the Web，这样别人可以通过你的notion域名访问你的网页。

![将Notion页面分享到网上](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F1c7fd5af-fd41-4579-b78c-3b3640ee1cf0%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D7405ec3ddeb8f8fff9df9ffeaf544f5db17db6138ccd349a9ea768f598307a28%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=023d5fac-5b74-476d-a1a6-d74eb43c4c08&cache=v2)

将Notion页面分享到网上

2.  注册一个域名

可以在阿里云、腾讯云这些域名大厂上购买域名，国内大厂有保障。我是在腾讯云上购买并且备案的域名。

![在腾讯云购买域名价格](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F0e4b4d72-c284-4b7a-8c84-f9e1bde893ad%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3Da69564a68346d5a236bdfbbceee3db6e8b1d49707facd46d6bdb02526c83d707%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=5383c146-2277-4aa1-84ad-58a7835e62ff&cache=v2)

在腾讯云购买域名价格

或者可以用 [https://freenom.com/](https://my.freenom.com/) 注册一个免费的域名；不过免费的域名对网站的运营推广不利，搜索引擎优先会收入优质的域名。

![freenom免费域名](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F2ca5e655-1286-4cb8-955d-1bd9f6933c43%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D53512a8c808c67dc091f3a57f480c840fff7bd85ac03ec770160a292b07adda4%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=d836a784-920c-499b-9963-cc862445b7dd&cache=v2)

freenom免费域名

#### [](#f11d59a6b4ed4afc8efdb7f6d0af21ad "Step 1: 设置 CloudFlare 账号 (5 分钟)")Step 1: 设置 CloudFlare 账号 (5 分钟)

1.  注册账号: [https://dash.cloudflare.com/sign-up](https://dash.cloudflare.com/sign-up)

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F5c7779fb-47cf-4cb7-813a-83b9d8bf9b35%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D0253c34a042970b716755f8064edbe6334d5244080df5c792d2cf3838aa804f3%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=3ff76200-a703-4c7e-8147-ac7216872b72&cache=v2)

2.  填写你的域名，即便你想要使用二级子域名(blog.tangly1024.com), 这里仍然要填写的是一级域名，tangly1024.com

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fed1a3c23-a9ec-4d11-9391-a75cb56c3975%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3De68ba58aec6d19e5f27e2a23aaf90246086a72dd8c8144656b42fe265458150a%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=2a72a6c5-a72e-45ad-84c9-bdd98ba77f50&cache=v2)

3.  选择免费方案

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F7e547892-a740-421d-95d4-121230a3bbd0%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D0657b8046dc268e2595b00ea3aebb5ba93423c08d37adaf2df5f0cf564204593%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=184ed58a-c55a-4172-b43d-b449466ccd04&cache=v2)

4.  如果你的域名还没有任何一条A类解析记录，需要在这里手动添加一条记录，Name是根域名，Content填写 `1.1.1.1` 。然后点击继续，跳转到DNS配置页面。

-   若您用的是子域名，请添加一条记录 Name 是子域名且Content为 `1.1.1.1` 。

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F9e36279b-9c8b-4c9b-bfeb-44b98d91437f%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D75b7f9708c7b20e18f85026186ae2a38b3e9b85a67425dcb2f89eb51933c9ef1%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=3a20ec1b-7d2d-45e7-9d0e-4e1823b0b9e5&cache=v2)

5.  复制以下两个 2 域名名称服务器 `nameservers`, 以 `.ns.cloudflare.com` 结尾的那两个

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fe93d1654-3278-4d62-987c-227022f5454b%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3Ddbd3d44159b83e19a76392b4c5f77ea96d4b7a75fb1fd792f0173c3af9fc3e95%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=48e81e50-57b6-4b33-b89e-ac1f67fc341e&cache=v2)

6.  将名称服务器替换到你的域名服务商的配置中

💡

我这里用的是腾讯的域名后台，其他域名也一样。腾讯的域名主要是认证备案方便一些。

域名右侧菜单→更多→修改DNS ；

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fb5bd3e74-24ec-4e7e-a2f0-1cc4730f8467%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D233512a46ef7d8c9a5c1f0a27febed89a7bd5826279150a0eacf105bfd548287%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=e9a6226a-3c76-448a-a0a3-1893fca91dac&cache=v2)

等待cloudflare完成NS检查并激活后的邮件

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F76d2166c-0dd5-4771-9c09-ff760a384fc7%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D64e0e4bf457539aced7f9260dded341498c4edbe5a2a7f276f4d197734fc8aa9%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=f4b9df85-876a-419b-8ff2-513f9d7fe5dc&cache=v2)

踩坑：腾讯域名的DNSPod中修改NS，导致CloudFlare检测不到NS,需要直接到[https://www.dnspod.cn/](https://www.dnspod.cn/)这个网站修改腾讯云的DNS记录

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Ff7bb503c-19dc-4a9d-bbdc-8993d5a5b2ab%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3Dc04f9ebc517518011854598e5b49aa06bcac239eeca281f8f149284444048a97%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=34978f7a-5b41-47d0-b40c-7d9db353d7af&cache=v2)

更新NS可能需要72小时的全球生效时间

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F444906b0-9943-45a0-a523-cd2cf6018737%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D3c39a735ea9c242f48a790b14c34737f2c9736487d31ea53d74d0cec7a814ccf%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=299ac9f6-6d9a-4f23-b2cf-3144d76425ce&cache=v2)

💡

腾讯云DNS修改说明：由于各地网络运营商存在缓存，修改后一般 1~2 个小时内刷新生效， 最长需要 72 小时，请您耐心等待。

7.  稍等一分钟, 点击Done完成，检查名称服务器配置

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Ff84e767f-1d6e-4503-a68f-a9d67fb1c2ce%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D77980e52f59eb8455e8c962de2ce1aa5e1a8fd324bfa77118a8331bceefc2280%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=ef0a2771-962b-49dd-9e99-fbca7bd8a9f1&cache=v2)

8.  选择灵活的 SSL/TLS 加密模式(Flexible)

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F86fb45ea-88ba-4f12-8ec0-0c294227c586%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D0970bde3b0149890b3d75375e2cb1c3faa8d64356177225e3499a06fffc0c3ad%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=91d6f09e-7e36-4e90-a32e-9ed2f1ad7845&cache=v2)

这里的类型若选择错误，域名会出现“重定向次数过多”而不能访问的问题。(解决方案点击展开)

### [](#26129037804f498f887e4eed8acc86cc "CloudFlare 造成重定向的次数过多的原因")CloudFlare 造成重定向的次数过多的原因

当网站开启了 CloudFlare 服务，用户访问我们的网站时，其实访问的离用户比较近的 Cloudflare 服务器，Cloudflare 再代理用户请求我们的源服务器，以达到加速和保护源服务器的目的。Cloudflare 代理用户请求我们源服务器获取网页资源的过程叫**回源**。

Cloudflare 造成循环重定向的错误就出在了回源的过程中，造成这种错误的原因就是 http 和 https 之间的重定向。

Cloudflare Crypto 的 SSL 中有 4 个选项（如下），其中 Off 就是不启用 SSL，通过 HTTP 协议访问网站。另外 3 种是通过 HTTPS 协议访问网站。

![notion image](https://www.notion.so/image/https%3A%2F%2Fwww.wpzhiku.com%2Fwp-content%2Fuploads%2F2019%2F04%2Fximage.png.pagespeed.ic.1Z1K6xrHsa.png?table=block&id=632867d4-492d-43d8-b0ba-6fe97b85b2d8&cache=v2)

Cloudflare CDN 配置

-   Flexible：当我们的源网站没有配置 HTTPS 支持时，启用这个选项，Cloudflare 会在回源的时候通过 HTTP 协议访问我们的网站。

-   Full：当我们的源网站支持 HTTPS，但是 HTTPS 证书和域名不匹配或者是自签名证书时，Cloudflare 会通过 HTTPS 协议访问源网站，但不会验证证书，也就是说，即使我们的源网站提供的 HTTPS 证书不受浏览器信任，Cloudflare 也会通过 HTTPS 回源网站。

-   Full(strict)：当我们的源网站支持 HTTP ，并且证书有效时（未过期且受信任）。Cloudflare 会通过 HTTPS 协议访问源网站，并在每个请求过程中验证证书。

了解了上面各个设置的功能，我们来看一下 Cloudflare 的循环重定向问题是怎么出现的，在 Cloudflare 中开启了 SSL 后，访问网站时出现循环重定向需满足下面两个条件：

1.  SSL 中设置了 Flexible，CDN 以 HTTP 协议回源网站。

2.  源网站支持 HTTPS，并且设置了通过 HTTP 协议访问时，自动跳转到 HTTPS 协议。

到这里，可能就有朋友发现问题了，我们访问 Cloudflare 的 [CDN](https://www.wpzhiku.com/tag/cdn/) 服务器的时候，是通过 HTTPS 访问的，CDN 访问源网站的时候，是通过 HTTP 访问的，源网站上 HTTP 又自动跳转了 HTTPS，完美的一个循环重定向。重定向的次数多了，浏览器就撂挑子报出了 ERR\_TOO\_MANY\_REDIRECTS 的错误。

### [](#9fab8a7d83604cb1b3289ffa176fe8b0 "CloudFlare 造成重定向的次数过多问题的解决办法")CloudFlare 造成重定向的次数过多问题的解决办法

知道了循环重定向的原因，我们也就知道了怎么解决这个问题，通过测试，下面的两种设置方法都可以解决 Cloudflare 循环重定向的问题。

-   SSL 中选择 Full(strict) 或者 Full(strict)，让 CDN 回源的时候使用 HTTPS 的方式回源，没有 HTTP 什么事了，就不会跳来跳去了

-   源网站不设置 HTTPS 支持或者 不设置 HTTP 跳转 HTTPS，让 Cloudflare 回源的时候使用 HTTP 方式获取资源。

修改了 CloudFlare 设置后，可能需要过几分钟或清理浏览器缓存后才能生效。

除了 Cloudflare，使用其他 CDN 提供商的时候，也可能会出现这个问题，如果设置了 CDN 后，遇到了 Chrome 报重定向次数过多的问题，可以通过上面的思路查找问题。如果你在使用其他 CDN 的时候也遇到了类似的问题，欢迎在评论中提出，让更多的朋友看到。

如果你的服务器有自带的SSL证书，这里可选完全(Full)

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F9d3fb7b9-654f-484d-9a55-87a244fcb1cf%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D03ad6ae3df313bf6ef16f69faecc92c82fc1b795a108549ce265d2386537071e%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=85de5aea-9bc3-44ef-b507-c44dc32972d8&cache=v2)

9.  可选：开启永远使用 HTTPS,自动缩小化以及Brotli加速

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F4ea044ae-69cb-4e20-9870-792ad3e35c6c%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3Df0af99cfdf621c01c1476ff91fcce76eb046e80450d7d05562ba1c2b74373080%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=2314e9a1-935a-4e3a-8848-e2403431938b&cache=v2)

10.  点击完成

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F6f76a854-7098-4ce6-a332-e694b39ab2f2%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3Dc1e3b894c62079f0a05792c72361d9cb6fa9fb37d60d5492087c00f2ba210df8%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=5de50654-28d7-4a11-878b-b5eb8f47b28b&cache=v2)

11.  如果前面的NS解析已经生效，Cloudflare会检测到你的网站，你将会看到如下页面。否则要再检查一下NS的配置，再点击重新检查(每小时只能点一次)。

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F0c85e5ba-3dc3-4871-bee5-c100a58cc3ab%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D556cb7e768fcc9e8b3f7c5d0e5b4e939cadd7fa534e6d9a44c90e6e22568c9b7%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=9466896d-1510-485f-bbd9-1b4b6f21bd40&cache=v2)

可以用`dig`命令 来检测当前生效的NS

dig NS `你的域名`

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F5ec9b425-ce4b-42ea-9585-e04eeef8309a%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3Db4c7a7b780311619848082d968d8adad591e8d3300ee60cec4ac8e508be43b5f%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=e65dbde9-5767-4e7f-ba60-fcff99b9bb9e&cache=v2)

我在执行的时候等的还挺久，Namesevers一直是旧的没有更新过来，不着急

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F518c81df-92b9-462e-956d-721a73dabb8a%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D423478e2b745e1788a6e959c3f254a0d4c92ed551bf6551b6b7bdd12154b6671%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=241ec440-23fd-49c9-97cf-a26e054799ec&cache=v2)

12.  选择`Workers`工作页 (上方蓝盒子按钮中的一个)点击`Manager Workers`

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F065a77fe-072f-4932-9828-070e77fb1bb4%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3Db35a4d1aeff63cb0940dba237e9440f503b1156059a7e745559e829534c7948c%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=64073e35-bd60-4a73-b2b2-a666cd29fdfc&cache=v2)

13.  为你的Worker随便填写一个子域名 (无所谓填啥)

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fe3bcafea-22dd-4e01-9b86-542674bdbe5e%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D84ab6c0dadd7df32a388ec4ebbd1c44366f0b1a47390332249e6d7f000199bf1%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=2deef809-712e-4124-a540-502328dc9828&cache=v2)

14.  点击安装，并确定

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fd81dd492-c47d-4885-b970-bfb46af60e05%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D85efd1909f2e1c9a3eacc655856bda609a20d24d59d59d6f64852a26a6a058b1%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=d93c9c37-fe3c-42ef-a035-05fbe4d88cbe&cache=v2)

15.  选择免费方案

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F5e42872c-c904-4642-ba1e-67ffbea17228%2FScreen_Shot_2020-05-04_at_11.14.24_PM.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D5c7cb94d6ddb3ae6c901884c4f966d6f0e5b1acb9afb66e95ced5e02e104fe10%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=5f8190b2-c109-4c6d-92f7-8639793d1063&cache=v2)

如果你的网站访问者很多，以后可以再换成收费方案。

16.  验证你的个人邮箱，并回到Workers管理页面 (参见 #12)

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F16e82d73-b971-41fe-9fb4-c25c8d1b14ae%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D9cbe621a99a793188491830728247bfb8a31f8e0c13746fc09f2e9a1aa26da86%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=014c6bd9-8281-433d-8455-cadd16c24de3&cache=v2)

17.  点击创建Worker

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fdcdcea91-9270-4a4f-9de5-c7bc1cbb615a%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3Dfdb7ed5de2256e713fc9503a2c18d981f7c670b724f508325e571ee3227f2d81%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=567b3827-3cda-478c-a708-f6c7dabdc6ce&cache=v2)

#### [](#8530706e41bf48c9be3f14b071c4189a "Step 2: 定制生成Fruition脚本(2分钟)")Step 2: 定制生成Fruition脚本(2分钟)

例如：我的配置是

👉

`域名映射：` tangly1024.tk `notion分享URL：` https://www.notion.so/tanghh/Library-4df48560645f4c568aa9c788a38b5e4a

#### [](#c382483dd8094456bdf508464ae94507 "Step 3: 将脚本粘贴到 Cloudflare (1分钟)")Step 3: 将脚本粘贴到 Cloudflare (1分钟)

1.  删除旧的代码，粘贴你的

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fb2aedf89-4fbd-4e60-8858-5598d7329370%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3Da8587d29ed1dcdc3aa3b98596fab26614f58eed879a90eb88e8b488a19f459cb%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=e4125ba2-65e0-4258-89f3-4231d60cd8d9&cache=v2)

2.  点击保存和部署 Save and Deploy

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fbf2a1616-304e-4cbb-9cbe-dfa670e55838%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D78bf6e5e2b61aa974fa102d1dabbab6799dbcea480217177c9148940968a0845%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=e8ece654-b13e-4adf-a32e-8cc12a0ae419&cache=v2)

3.  保存完成后, 点击页面顶部的你的网站名

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fd5a7add2-6b33-4be5-951d-10dc3ff869b7%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D1e928daa8b503a666cc5d9b7fafe24766519dd557736a292b44ea2fb98c5abbd%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=591f6234-f357-416b-94bf-8141c99470f9&cache=v2)

4.  访问Workers 页面点击 Add Route 添加路由

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fb2600ac1-577b-4352-869c-7f8f7b11ced5%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3Dd39d9aaaa6962e9ede950a00a76403e979e8529b423f490515d8ace85454541a%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=9eb32bd4-0837-4bc4-bef1-273f04f3ea74&cache=v2)

5.  输入您的域名 `yourdomain.com/*` (或你的子域名 [`subdomain.yourdomain.com/*`](http://subdomain.yourdomain.com/*) 如果用的子域名) 作为路由并且选择你刚创建的Worker

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F04ef4ebd-0684-4d92-8c3d-6cac01320bff%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D67b35b91c61cb5c0d237376f77bec23e94d227b69ff92a5e9128e2183fe5ba11%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=b268a267-1601-4b36-817e-06f700eca4dd&cache=v2)

6.  点击 **save 保存, 万事大吉**. 🎉

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fc921e63e-a491-42c4-9279-c0c7bbb9f2fd%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3Dd2e31054c11f4767abfecce92aafe2618c3b36e030c084154fd0d00b60c44c24%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=566b9902-eb46-4b87-92f3-7d5b1c53fab3&cache=v2)

7.  [给作者发邮件](mailto:me@stephenou.com) 让我看看你的有趣的网站

8.  欢迎将 [Fruition](https://fruitionsite.com/) 添加到你的网站，让更多人知道他。

## [](#70092ee72243436081490afcf59f4468 "FAQ（常见问题）")FAQ（常见问题）

#### [](#ef49f1606cd8415e993671e7c2bdf350 "1.访问页面时报错Mismatch：")1.访问页面时报错Mismatch：

问题：打开网站时显示：`Mismatch between origin and baseUrl (dev).`

解决：配置中的MY\_DOMAIN与实际域名不符，我的实际打开地址是www.tangly1024.tk，但配置是tangly1024.tk，这样也是错误的。请检查域名地址的正确性。

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F90533f09-4ebf-4cf3-b46d-da9515c4d52c%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D461af39aaea7f0d5ac4c7ee0e872be52ab83d8d07b7a7d1827cebcf4be3df629%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=e7850076-6dcf-4ebd-8a57-c0553f5002b1&cache=v2)

#### [](#2914eebdb5ca4f4f8b12047572ceacea "2.配置CloudFlare显示错误 1004 ")2.配置CloudFlare显示错误 1004

问题：配置解析时显示 `DNS Validation Error (Code: 1004) This record type cannot be proxied`.

解决检查一下配置，当值为1.1.1.1时，必须关闭右边的橙色云，选择仅限DNS代理。

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fc589a2b3-34cd-48e3-9e71-54354943af97%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D33aab994fb8e60f379c3a039b54c3b4363f09f698c75f59fa608816b03c2c256%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=fc9c2a84-c695-4428-84c3-74c7d7123307&cache=v2)

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F766fbea0-1318-4b02-b1c2-86d07dc7ae34%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D3bdd940cdb6fbdfd5d7ae7a25ab7619a7c007d49f9740c352e93ad9e1242da27%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=03e36f81-8795-4ee1-ba45-9ee19f6a6352&cache=v2)

#### [](#07ab76ff8f0d4044b4b6fa92ae64f13b "2.配置CloudFlare显示错误 1034 ")2.配置CloudFlare显示错误 1034

问题：访问网站显示错误 Error 1034，并且提示`Check your DNS records to ensure they are pointed to the IP address(es) you were assigned at registration.`

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fe2a9a148-5895-4138-b274-1a2059b6e3ec%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3Dd36721ef1a077316bb59d455cf6a73db7313b7049f56a4f87b1968aa7a1cba92%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=a1d5a429-393e-4923-ac27-0d3c8e9d53d9&cache=v2)

解决：ip受限导致，参考此文章，配置新的回源ip

## [](#386ff894a3674923bc249ad04dfdc976 "行动建议")行动建议

你的notion博客网站搭建成功了吗，不妨在评论区，留下你的博客地址，让我看看吧~

-   博客排版方式推荐：这个博客加入了文章分类的功能，挺实用的：

![notion image](https://www.notion.so/image/https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F3f9d10fb-3bb5-4c10-b191-d20a3f8e753c%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220629%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220629T112300Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D849f5df0afb7d1d08b9d8fd68cc9e1ee9e322d369a0b5abe675b40733c1ac08e%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject?table=block&id=89c15952-076d-4d60-ab62-2f63c8487207&cache=v2)

## [](#7f0409a5f3be4e9c98a529c77237acfa "参考")参考