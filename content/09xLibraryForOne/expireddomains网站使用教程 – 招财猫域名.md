#域名

[expireddomains.net](http://expireddomains.net) 注册账户（免费），登录后，在logo下面的Deleted Domains部分，找到 pendingdelete，点击进去，那么此时你会看到各种后缀的过期域名的列表。

列表里面的 LE是域名长度，End Date为删除日期，那么多的域名过期了，如何找到我想要的呢？这个时候就要去筛选，[expireddomains.net](http://expireddomains.net) 提供了非常强大的筛选功能。

**长度搜索**

你点击打开 Show Filter ，比如你要筛选最近有哪些单字符掉了？ 在Domain Name Settings部分的 Length 的 max 里面输入长度 1 然后按下 apply filter，就可以看到最近过期的单字符。

**关键字搜索**

还有比如你要看看最近有没有sex前缀掉了？你同样点开Show Filter 在 start with 那里输入 sex，然后按下 apply filter，这样就可以筛选以sex开头的域名，再在列表里点一下LE这个表头,让他根据长度从小到大排列。

或者你要看到今天或者明天要掉了的sex前缀，点一下 End Date，让他根据删除时间从最近开始排列，你就会看到对应的列表。

**搜索某个后缀**

还有比如你要看看最近有没有dog后缀的域名掉了？你同样点开Show Filter 在Additional部分，ctrl+f 找到dog后缀，然后勾选，按下 apply filter，这样就可以筛选以dog结尾的域名

**二、域名删除的精确时间？**

上面的expireddomains只是知道大部分域名在哪一天删除，但是你不知道更加精确的时间

要知道更加精确的删除时间，比如是具体几点几分几秒掉的，你就要做个短期统计分析，比如你想知道 .sb 后缀的域名一般具体什么时候删除，你可以使用bt面板的定时任务功能，每天定期跑一些监控代码，监控某一批即将过期删除的sb域名(expireddomains可以随便找到这些过期的sb域名)，记录他们每天掉下的时间，然后做个分析总结推算出sb后缀掉下时间，还有一种方法是直接去信sb管理局，让他们告诉你他们具体什么时候删除域名。

国别后缀的具体删除时间比较复杂，需要自己去尝试测试，新后缀的具体删除时间一般比较有规律，当你在expireddomains知道具体某一天删了，然后你找到whois里面的Updated Date时间，把这个时间+5天，然后再转换为中国时间就是实际掉下时间(新后缀里面显示的基本上都是UTC时间)。