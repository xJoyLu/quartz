本周研究了下notion，因为有个域名所以有了这篇文章。

## 

[](https://www.o-id.cc/001.%E6%90%AD%E5%BB%BA%E4%B8%80%E4%B8%AA%E5%9F%BA%E4%BA%8Enotion%E7%9A%84%E4%B8%AA%E4%BA%BA%E7%BD%91%E7%AB%99#20a83898780e45c8b4abd8c06fa2eb42 "准备阶段")准备阶段

👉

您需要准备Notion账号、Github账号、next.js项目地址、cloudflare账号。

Github项目地址：[https://github.com/chusight/nextjs-notion-starter-kit](https://github.com/chusight/nextjs-notion-starter-kit)

项目原作者：[https://github.com/transitive-bullshit](https://github.com/transitive-bullshit)

### 

[](https://www.o-id.cc/001.%E6%90%AD%E5%BB%BA%E4%B8%80%E4%B8%AA%E5%9F%BA%E4%BA%8Enotion%E7%9A%84%E4%B8%AA%E4%BA%BA%E7%BD%91%E7%AB%99#e311101696a145ccbb617787675b5ce3 "Notion账号")Notion账号

可以用自定义的QQ邮箱注册。

需要找一些notion页面模板，复制到自己的库，然后分享为所有人可查看。

此时左侧列表栏复制你分享页面的地址。

![](data:image/svg+xml,%3csvg%20xmlns=%27http://www.w3.org/2000/svg%27%20version=%271.1%27%20width=%27371%27%20height=%27282%27/%3e)![notion image](https://www.o-id.cc/_next/image?url=https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F1abeed04-0c41-48e5-a3d1-054ae6383bda%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220513%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220513T063535Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D3086b4d9a98e2dba797315b539ff9278dfbd983a5e09f2c5e051e103d7982a3b%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject&w=750&q=75)

格式如下： https://www.notion.so/******************************

这个很重要，会用到项目内的代码里。

### 

[](https://www.o-id.cc/001.%E6%90%AD%E5%BB%BA%E4%B8%80%E4%B8%AA%E5%9F%BA%E4%BA%8Enotion%E7%9A%84%E4%B8%AA%E4%BA%BA%E7%BD%91%E7%AB%99#586fb107abf34d2eb9ed921997284988 "Github账号")Github账号

国内加载慢注册需要工具。

注册后打开上面的next.js项目fork到自己的库。

项目文件需要修改处请参考项目内自述文件，有几个关键点截图放下面：

![](data:image/svg+xml,%3csvg%20xmlns=%27http://www.w3.org/2000/svg%27%20version=%271.1%27%20width=%27665%27%20height=%27869%27/%3e)![notion image](https://www.o-id.cc/_next/image?url=https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fb2919336-3c5c-4953-8a6c-a6d29f037f44%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220513%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220513T063535Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D45a7ee0162a92f4a487a4cdd0a19d6da5ef5ac13f136d225c69d1a7e32d58816%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject&w=1920&q=75)

总共有三处，从上往下

💡

第一处，

![](data:image/svg+xml,%3csvg%20xmlns=%27http://www.w3.org/2000/svg%27%20version=%271.1%27%20width=%27535%27%20height=%2736%27/%3e)![notion image](https://www.o-id.cc/_next/image?url=https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fac3bbef1-c03f-47a3-aa95-2802fe555615%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220513%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220513T063535Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3Dcb3f39a9ad91abe0c419943df6b79970ac36b8aae7336ad3fc66304339ad75e7%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject&w=1080&q=75)

[components](https://github.com/chusight/nextjs-notion-starter-kit/tree/main/components)文件夹内的

[Update GitHubShareButton.tsx](https://github.com/chusight/nextjs-notion-starter-kit/commit/ff8af71b725506b6cf4052f8e4608607219c118f)文件

这个要修改的是主页右上角的Github链接

![](data:image/svg+xml,%3csvg%20xmlns=%27http://www.w3.org/2000/svg%27%20version=%271.1%27%20width=%271928%27%20height=%27375%27/%3e)![notion image](https://www.o-id.cc/_next/image?url=https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F5bb296f2-69bb-414b-8ce5-e01400435cc0%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220513%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220513T063535Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D665d8cb3799b4005fd20151288e98d41ab06f365de36261df5c060ebc97108cd%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject&w=3840&q=75)

代码链接马赛克部分替换为自己的账户名

![](data:image/svg+xml,%3csvg%20xmlns=%27http://www.w3.org/2000/svg%27%20version=%271.1%27%20width=%271206%27%20height=%2784%27/%3e)![notion image](https://www.o-id.cc/_next/image?url=https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fa8a809a5-9f39-4833-ac18-cdec3a970874%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220513%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220513T063535Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3Dda363c2f2f11bd72401d8881d188b1683e02446014a32433952950ed9a44ff6a%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject&w=3840&q=75)

💡

第二处

![](data:image/svg+xml,%3csvg%20xmlns=%27http://www.w3.org/2000/svg%27%20version=%271.1%27%20width=%27738%27%20height=%27523%27/%3e)![notion image](https://www.o-id.cc/_next/image?url=https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Ff5dec74c-03a6-4e64-a0fa-175ce07fc7ac%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220513%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220513T063535Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3Dee9215918b40c139f527e5ad57fee648c43c949afa3cfb8c1c3777d8e2af1f81%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject&w=1920&q=75)

[public](https://github.com/chusight/nextjs-notion-starter-kit/tree/main/public)文件夹内的图标文件，这个主要功能就是在各种设备上的预览图标，可以下载后在ps内一个一个替换掉，ico有很多网站可以在线转换。

修改完chrome的效果：

![](data:image/svg+xml,%3csvg%20xmlns=%27http://www.w3.org/2000/svg%27%20version=%271.1%27%20width=%27238%27%20height=%2730%27/%3e)![notion image](https://www.o-id.cc/_next/image?url=https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F98fb18e3-e509-47d4-ac86-6169a5f1f3ba%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220513%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220513T063535Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3Dd4c449c60b33532446d37f9869c3417f694e1fdf62e6bd01557c72383187dc96%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject&w=640&q=75)

💡

第三处（关键）

第三处最关键成功与否都在这个文件内

![](data:image/svg+xml,%3csvg%20xmlns=%27http://www.w3.org/2000/svg%27%20version=%271.1%27%20width=%271035%27%20height=%27581%27/%3e)![notion image](https://www.o-id.cc/_next/image?url=https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F63474992-05d0-46fb-8715-0c3e30819e82%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220513%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220513T063535Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D137e12e53fc297fbbe415960664a13cc7d49e806c5a39530d6f39e3bd9bcb685%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject&w=3840&q=75)

`rootNotionPageId:`后面跟在notion内共享页面复制到的link地址的后尾

![](data:image/svg+xml,%3csvg%20xmlns=%27http://www.w3.org/2000/svg%27%20version=%271.1%27%20width=%27545%27%20height=%2762%27/%3e)![notion image](https://www.o-id.cc/_next/image?url=https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fc8ea62a2-9176-43aa-84c4-cf9acf15e2bb%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220513%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220513T063535Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D225cabd425002dd09fea8f318cdbe6809d94de8c49703f2c6053b62032359f02%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject&w=1200&q=75)

domain后面填写你共享页面的Link

name与author可以随意写。

这里有个小tips，notion页面的标题切记不要更改，更改后你这个页面的link地址会有变化，这个代码里的修改就没用了。

底下twitter， GitHub ，Linkedin 不用可以不填，填的话只填写用户名就可以了。

三处修改完就可以去vercel部署项目了。

### 

[](https://www.o-id.cc/001.%E6%90%AD%E5%BB%BA%E4%B8%80%E4%B8%AA%E5%9F%BA%E4%BA%8Enotion%E7%9A%84%E4%B8%AA%E4%BA%BA%E7%BD%91%E7%AB%99#257f79bb625949dba918ef08037a7fa0 "Vercel")Vercel

用上面的Github账号登陆vercel可调用库内刚保存的next.js部署新项目。

部署成功后会生成几个结尾是.app的项目链接，打开这些链接就是项目内修改的notion的页面。

以上教程比较简单，不明之处请自己寻找答案。

> 如果你有独立域名可以继续往下看：

### 

[](https://www.o-id.cc/001.%E6%90%AD%E5%BB%BA%E4%B8%80%E4%B8%AA%E5%9F%BA%E4%BA%8Enotion%E7%9A%84%E4%B8%AA%E4%BA%BA%E7%BD%91%E7%AB%99#4148664d98e44081928b6236853a50e8 "Cloudflare")Cloudflare

一个免费的dns解析网站

先注册账号，输入你的独立域名解析，会有两个属于自己的dns地址。

将独立域名服务商（你的域名购买商）处的dns解析地址修改为cloudflare给的两个dns地址。

当收到邮件反馈，表示你的dns已经解析成功了。

### 

[](https://www.o-id.cc/001.%E6%90%AD%E5%BB%BA%E4%B8%80%E4%B8%AA%E5%9F%BA%E4%BA%8Enotion%E7%9A%84%E4%B8%AA%E4%BA%BA%E7%BD%91%E7%AB%99#60e5516bbb3c48db9063256689361b9c "回到vercel")回到vercel

vercel部署页面

![](data:image/svg+xml,%3csvg%20xmlns=%27http://www.w3.org/2000/svg%27%20version=%271.1%27%20width=%271046%27%20height=%27164%27/%3e)![notion image](https://www.o-id.cc/_next/image?url=https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F9f77ddf9-679c-4d7e-b9e8-6da6c5034543%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220513%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220513T063535Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D37eb333ba4157e8943b1bdd685b34560b6029cf3c892f17e71410a93ed92fd27%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject&w=3840&q=75)

在****Domains****内添加你的独立域名，因为dns已经在Cloudflare解析成功，这个页面会显示你需要在Cloudflare网站添加的dns规则

💡

有两条

💡

A @ xx.xx.xx.xx

💡

CNAME www xxxx.xxxx.xxxx.xxxx

Cloudflare网站添加成功后如图

![](data:image/svg+xml,%3csvg%20xmlns=%27http://www.w3.org/2000/svg%27%20version=%271.1%27%20width=%27956%27%20height=%2779%27/%3e)![notion image](https://www.o-id.cc/_next/image?url=https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fcaefcd0e-e44b-44c1-b028-dab609e6cecb%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220513%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220513T063535Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D2229f3755aa6425c63d174db4ebeafebde623056e08a4c10466888ce26ef6bbd%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject&w=1920&q=75)

vercel上会自动验证

如图

![](data:image/svg+xml,%3csvg%20xmlns=%27http://www.w3.org/2000/svg%27%20version=%271.1%27%20width=%27774%27%20height=%27432%27/%3e)![notion image](https://www.o-id.cc/_next/image?url=https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F5b84cd4c-9bc8-4bb3-9ada-7f52d040cb80%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220513%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220513T063535Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D40c828a2c56b75ed89fca108febdaadbd886944165fdeaa40b569d5d03a43fbc%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject&w=1920&q=75)

成功后你的独立域名就可以访问了！

~~但为了访问速度更快，~~

~~我们再次地~~

### 

[](https://www.o-id.cc/001.%E6%90%AD%E5%BB%BA%E4%B8%80%E4%B8%AA%E5%9F%BA%E4%BA%8Enotion%E7%9A%84%E4%B8%AA%E4%BA%BA%E7%BD%91%E7%AB%99#118c3c74285e4790ac112ca1d89993fe "回到Cloudflare")~~回到Cloudflare~~

~~Cloudflare免费版支持三种页面规则，可以添加以下两种~~

以下规则为WordPress建站规则不适用于vercel

~~具体如图：~~

💡

~~1.~~~~www.****.***~~~~/wp-admin*~~

~~前面是你自己的独立域名~~

![](data:image/svg+xml,%3csvg%20xmlns=%27http://www.w3.org/2000/svg%27%20version=%271.1%27%20width=%27787%27%20height=%27474%27/%3e)![notion image](https://www.o-id.cc/_next/image?url=https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F109e2b3e-d825-439c-8ab0-188e57dc212b%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220513%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220513T063535Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D07b1e5716d4a1509e09ae92f9314080ee9d6daf25ed9c01d1fdfbef122babc76%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject&w=1920&q=75)

💡

~~2.~~~~www.****.***~~~~/*preview=true*~~

~~前面是你自己的独立域名~~

![](data:image/svg+xml,%3csvg%20xmlns=%27http://www.w3.org/2000/svg%27%20version=%271.1%27%20width=%27767%27%20height=%27471%27/%3e)![notion image](https://www.o-id.cc/_next/image?url=https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fcef915f5-c0f0-42cb-bc6d-62c07fece8ac%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220513%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220513T063535Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D2e4f1db1b3e6cb08b07a2694c53eb31982803edf9f91380b17f1c4cce7614476%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject&w=1920&q=75)

~~设置完成DNS规则内会自动生成几个规则，直接添加到记录。~~

~~如图~~

![](data:image/svg+xml,%3csvg%20xmlns=%27http://www.w3.org/2000/svg%27%20version=%271.1%27%20width=%27961%27%20height=%27115%27/%3e)![notion image](https://www.o-id.cc/_next/image?url=https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F9b90b29c-18f3-4b63-b3a9-fb69b69bab9b%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220513%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220513T063535Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3Db7fae476324177c61bff6273c99a1f4c8a173eb7c58ce104089eff7786d711e4%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject&w=2048&q=75)

~~这时所有工作都完成了，你在notion上面修改你的共享页面时，它将自动更新。~~

~~此时你的独立域名访问就是你部署的网页。~~

~~enjoy it ！~~

> 感谢：Athena 指正 以上规则为WordPress建站规则。

> Ps.自己摸索，如有疑问可邮件联系我，谢谢！

更新两点：

1.解析可以直接在域名购买平台解析，直接添加DNS规则。（不需要Cloudflare）

2.首页文章列表用notion里的databace做的。

---
## 说在前面

听闻原作者有了更新（作者地址：[https://github.com/transitive-bullshit/nextjs-notion-starter-kit](https://github.com/transitive-bullshit/nextjs-notion-starter-kit)）预览网页：[https://transitivebullsh.it/](https://transitivebullsh.it/)，去看了下github的分叉，用的是一个韩国老哥的库，（地址在这里：[https://github.com/hanmilLee/nextjs-notion-starter-kit](https://github.com/hanmilLee/nextjs-notion-starter-kit)）预览网页：[https://hmdev.vercel.app/](https://hmdev.vercel.app/)

## 

[](https://www.o-id.cc/004.%E6%90%AD%E5%BB%BA%E4%B8%80%E4%B8%AA%E5%9F%BA%E4%BA%8Enotion%E7%9A%84%E4%B8%AA%E4%BA%BA%E7%BD%91%E7%AB%992.0#eef7fd845de14c4dacd0cd158d433d16 "几个变化")几个变化

可以说是重磅效果：

### 

[](https://www.o-id.cc/004.%E6%90%AD%E5%BB%BA%E4%B8%80%E4%B8%AA%E5%9F%BA%E4%BA%8Enotion%E7%9A%84%E4%B8%AA%E4%BA%BA%E7%BD%91%E7%AB%992.0#1df58ce36ef0486d9e8f1983d6c993c3 "终于有了导航栏")终于有了导航栏

PC

![](data:image/svg+xml,%3csvg%20xmlns=%27http://www.w3.org/2000/svg%27%20version=%271.1%27%20width=%271236%27%20height=%27460%27/%3e)![notion image](https://www.o-id.cc/_next/image?url=https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F0d34b9ad-04b1-4c2c-9e1e-6b93d7285e16%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220513%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220513T063552Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3Dd2a3b6ae71eef4599b1fb78316630854b037f5b8d6c83e4a28c3a8d7e76fcee9%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject&w=3840&q=75)

安卓：

![](data:image/svg+xml,%3csvg%20xmlns=%27http://www.w3.org/2000/svg%27%20version=%271.1%27%20width=%271080%27%20height=%27512%27/%3e)![notion image](https://www.o-id.cc/_next/image?url=https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F2ef07a34-d7fc-49a9-9e59-834d24f3d4e8%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220513%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220513T063552Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D0ac442d2a64d3ccbe1a6d39c44fe1a9c392982275f95fb10a8ccb4b14f684b5a%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject&w=3840&q=75)

导航栏此次在****site.config.ts****文件内

这几行

![](data:image/svg+xml,%3csvg%20xmlns=%27http://www.w3.org/2000/svg%27%20version=%271.1%27%20width=%27933%27%20height=%27520%27/%3e)![notion image](https://www.o-id.cc/_next/image?url=https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F291fbf5c-34e3-4f24-8fc0-503598a14f65%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220513%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220513T063552Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D25a05616cbc9191d4391ed1794536fb30df269448dceb7112e284c9f58aa60b5%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject&w=1920&q=75)

注意中间有个逗号相隔

实测手机端体验良好导航栏标题不要超过三个。

### 

[](https://www.o-id.cc/004.%E6%90%AD%E5%BB%BA%E4%B8%80%E4%B8%AA%E5%9F%BA%E4%BA%8Enotion%E7%9A%84%E4%B8%AA%E4%BA%BA%E7%BD%91%E7%AB%992.0#5f8af41c13f74fd38f868b9659b64357 "文章内的留言板")文章内的留言板

留言板复制完库后，登录github要求安装，自动跳转到[https://utteranc.es/?installation_id=25639318&setup_action=install](https://utteranc.es/?installation_id=25639318&setup_action=install) 点击安装就可以了

### 

[](https://www.o-id.cc/004.%E6%90%AD%E5%BB%BA%E4%B8%80%E4%B8%AA%E5%9F%BA%E4%BA%8Enotion%E7%9A%84%E4%B8%AA%E4%BA%BA%E7%BD%91%E7%AB%992.0#05760b070551486ea87d44a3e3850766 "底部左下的点击统计")底部左下的点击统计

点击统计使用的是[https://hits.seeyoufarm.com/](https://hits.seeyoufarm.com/)

具体代码在[**components**](https://github.com/chusight/o-id/tree/main/components)**/Footer.tsx 内**

在hit网页输入你的域名链接，注意要带[https://](https://o/)

将

![](data:image/svg+xml,%3csvg%20xmlns=%27http://www.w3.org/2000/svg%27%20version=%271.1%27%20width=%271174%27%20height=%27288%27/%3e)![notion image](https://www.o-id.cc/_next/image?url=https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fd67380d7-2285-4a56-8c2d-0ff18ad911b2%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220513%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220513T063552Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3Db5d44638bc050ee0e68ec91bab21b2c5f4acfe36ae806b75ff01833f97fdb201%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject&w=3840&q=75)

里面的内容copy到上面文件内的

![](data:image/svg+xml,%3csvg%20xmlns=%27http://www.w3.org/2000/svg%27%20version=%271.1%27%20width=%271761%27%20height=%27954%27/%3e)![notion image](https://www.o-id.cc/_next/image?url=https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F37b8b194-7733-42e5-aa78-b75c94faf6d8%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220513%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220513T063552Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D5b013735dbbfa7c1935ca1ce98e4576d67ccbdc664d6638ebf44d05809fed2dd%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject&w=3840&q=75)

需要注意的是，尾段的=false需要改为ture

如下：

![](data:image/svg+xml,%3csvg%20xmlns=%27http://www.w3.org/2000/svg%27%20version=%271.1%27%20width=%27403%27%20height=%2745%27/%3e)![notion image](https://www.o-id.cc/_next/image?url=https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Ff359d714-48a5-45e1-a1d5-257da467b993%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220513%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220513T063552Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D994cd7c04751a1c87f139ffd613abcbc5c15535ea7b52be3233aa3b5a2947329%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject&w=828&q=75)

## 

[](https://www.o-id.cc/004.%E6%90%AD%E5%BB%BA%E4%B8%80%E4%B8%AA%E5%9F%BA%E4%BA%8Enotion%E7%9A%84%E4%B8%AA%E4%BA%BA%E7%BD%91%E7%AB%992.0#9aee6cd654934d36bcf3b788e21d478f "需修正处")需修正处

在components/PageHead.tsx内

此处暴露了原作者的GA ID

![](data:image/svg+xml,%3csvg%20xmlns=%27http://www.w3.org/2000/svg%27%20version=%271.1%27%20width=%27917%27%20height=%27509%27/%3e)![notion image](https://www.o-id.cc/_next/image?url=https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F20f37d14-7f2d-46a4-b980-86becd129cfa%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220513%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220513T063552Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D945d9db4efef78e4bb5d6628df913d461055c3980379f6adba21995edc37cd9f%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject&w=1920&q=75)

### 

[](https://www.o-id.cc/004.%E6%90%AD%E5%BB%BA%E4%B8%80%E4%B8%AA%E5%9F%BA%E4%BA%8Enotion%E7%9A%84%E4%B8%AA%E4%BA%BA%E7%BD%91%E7%AB%992.0#cf2f3807ad0445859d5b2c307aa8bd39 "我们可以修正为自己的GA ID")我们可以修正为自己的GA ID

（什么是GA ID？Google Analytics 中文名称“谷歌分析”，是谷歌官方发布的一款网站流量统计分析工具，也是同类型SEO工具中功能最强大的那一个，没有之一，具体可以看这篇文章）

有谷歌账号即可

地址：https://analytics.google.com/

注册添加

在数据流添加一个网页数据流

![](data:image/svg+xml,%3csvg%20xmlns=%27http://www.w3.org/2000/svg%27%20version=%271.1%27%20width=%271080%27%20height=%27669%27/%3e)![notion image](https://www.o-id.cc/_next/image?url=https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F9fec6849-6ad1-4d97-81dd-3d177a627e07%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220513%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220513T063552Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3Dcc7e02319bde2bf83f91b26e3cfe1c84781ce6679133595e2741c787095d6d1b%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject&w=3840&q=75)

添加网页地址与名称可以生成如下ID

![](data:image/svg+xml,%3csvg%20xmlns=%27http://www.w3.org/2000/svg%27%20version=%271.1%27%20width=%271080%27%20height=%27315%27/%3e)![notion image](https://www.o-id.cc/_next/image?url=https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Facc11d92-9bc6-43a2-b9f5-fb03ef37edab%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220513%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220513T063552Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D739b6b449488ec96d96e0950366d36c6a7e996c1aded29928e9942888654d13c%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject&w=3840&q=75)

将G-**********的字段与下图位置替换。

![](data:image/svg+xml,%3csvg%20xmlns=%27http://www.w3.org/2000/svg%27%20version=%271.1%27%20width=%27917%27%20height=%27509%27/%3e)![notion image](https://www.o-id.cc/_next/image?url=https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F20f37d14-7f2d-46a4-b980-86becd129cfa%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220513%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220513T063552Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D945d9db4efef78e4bb5d6628df913d461055c3980379f6adba21995edc37cd9f%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject&w=1920&q=75)

### 

[](https://www.o-id.cc/004.%E6%90%AD%E5%BB%BA%E4%B8%80%E4%B8%AA%E5%9F%BA%E4%BA%8Enotion%E7%9A%84%E4%B8%AA%E4%BA%BA%E7%BD%91%E7%AB%992.0#2266326cc784477bb27f47fb738bbd2f "如不需要GA ID")如不需要GA ID

可将G-*******字段用${config.GAId}替换

![](data:image/svg+xml,%3csvg%20xmlns=%27http://www.w3.org/2000/svg%27%20version=%271.1%27%20width=%27525%27%20height=%27311%27/%3e)![notion image](https://www.o-id.cc/_next/image?url=https%3A%2F%2Fs3.us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fc5fbfc8e-7221-481b-a3b3-a866c4332b30%2FUntitled.png%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Content-Sha256%3DUNSIGNED-PAYLOAD%26X-Amz-Credential%3DAKIAT73L2G45EIPT3X45%252F20220513%252Fus-west-2%252Fs3%252Faws4_request%26X-Amz-Date%3D20220513T063552Z%26X-Amz-Expires%3D86400%26X-Amz-Signature%3D25cc3ba815c8591dc961870c57e136e9fae5e2ad8a47f3bc2272f5b8c6b7d3db%26X-Amz-SignedHeaders%3Dhost%26x-id%3DGetObject&w=1080&q=75)