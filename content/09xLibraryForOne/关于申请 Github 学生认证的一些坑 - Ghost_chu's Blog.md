author:: Ghost_chu
source:: [关于申请 Github 学生认证的一些坑 - Ghost_chu's Blog](https://www.ghostchu.com/github-education/)
clipped:: [[2022-08-23]]
published:: 

本文最后更新于 256 天前，其中的信息可能已经有所发展或是发生改变。

继我薅 Github 羊毛成功后，我的同学也想薅一把，但是被多次拒绝翻车（于是老师傅上手帮忙了 x）。

鉴于似乎不少人审核都没过的，所以记录一下申请 Github 学生认证 的一些坑。

不会吧？这种国际平台肯定不能用中文的，别去用中文填 Form 了。不会的话试试 [Google Translate](https://translate.google.cn/)。

**敲！重！点！**

在申请的时候**全程是不可以挂梯子的，包括反代**。

Github 会根据你的 IP 地址地理位置检查你的 IP 距你学校的距离。如果太远，会被拒绝。

```
We would love to have you onboard GitHub Education the soonest. However, I've taken a look at our logs, and it seems that you have applied far from your campus. If you are using a VPN, please disable it when you reapply. If you are not using a VPN, try reapplying when connected to the internet from a different network.
```

实在上不去，可以尝试改 Hosts 解决，但是绝对不可以改变你的 IP 地址。

简而言之，你必须直连 GitHub。

不少人可能都收到诸如此类的邮件：

```
Unfortunately, we weren't able to approve your educational discount request submitted on <DATE> for <USERNAME>. The item you uploaded is insufficient to demonstrate your current academic status. Modifications to your photo proof might have been detected by the system. Please see suggestions.Suggested proof to expedite your approval: School issued photo ID with current enrollment date. Schedule for current enrollment with school name. Signed registration certificate with current enrollment date. Transcripts with current enrollment date.  To reapply, click here. For help, click here.
```

这个提示实际上是由 Github 自动审核发出的（特点在于你上传后刷新一下状态立刻就会变成 “Rejected”）。

GitHub 是有人工审核的，时间通常会随第一封邮件发给你，你可以届时再次检查你的状态。

受到 GitHub 支持的证明材料有：

-   你的学校的录取通知书（大一新生用，比如我）
-   你的学生证（手写也行，但是得有照片和钢印）
-   你的学校教务系统的课表（学习通的也行）
-   你的成绩单（电子版也可）
-   或者其他任何可以证明你是**在读学生**的材料（已经毕业的材料提交无效）

（以上按照 GitHub 的意思是你提交的时候应该**材料和脸同框**无遮挡）

除此之外，我提交的时候还带了个写个我的 GitHub 的 username 的小纸条以及 [学信网的在线验证报告链接和验证码](https://my.chsi.com.cn/archive/bab/xj/show.action)。

*GitHub 改版后似乎 Upload 按钮消失了，但是你可以保存成文件直接拖进页面框里上传。*

在开启工单之前，你需要知道的几点：

-   Github 无权在工单中审核你的材料，你所有的材料必须提交到审核平台
-   如果提交完新的材料立刻被打回，是自动审核程序干的，你可以等等人工来审核
-   工单可以告诉你你哪里没有满足要求，然后你可以对照提交所需的材料，但无法帮你直接修改为 Approved
-   工单似乎有一套固定的话术，回复比较标准，但的确是人。在你特别不理解的时候你可以仔细问问，GitHub 会告诉你的

通常上述材料提交后，由于 GitHub 的自动审核机制，会被立刻 Rejected。

你需要耐心等待直至人工审核完毕，通常不会晚于页面和邮件显示的日期。

如果逾期仍然未通过，你可以开个工单问问，或者像我多试几次，提交尽可能多的材料然后开个工单蹲人工：

![关于申请 Github 学生认证的一些坑插图](https://cdn.ghostchu.com/wp-uploads/2021/12/1638964901-history.png "关于申请 Github 学生认证的一些坑插图")

只要不停下脚步，道路就会不断延伸 ——