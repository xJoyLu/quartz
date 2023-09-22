author:: null
source:: [Notion的进度条样式和代码收集贴](https://www.douban.com/group/topic/247171966/?_i=82029272inecFS)
clipped:: [[2022-07-19]]
published:: 

感觉网上的都好混乱，而且因为是百分数，经常弄出两个数值，复制改代码的时候改起来很累，所以自己收集和整理了一下，把所有A/B的形式都弄成了“数值”，用这个进度条的时候只需要知道数值这个部分写百分数就好啦

> 下面的预览图都是windows的

看不懂这些代码、不知道怎么用的，可以看帖子第二部分 ios的符号显示得不一样，如果需要自行修改的话可以看帖子最后部分，有说明怎么自定义进度条

另外如果有人对小组件有兴趣的话，这里还有一个小组件的收集贴⬇️

## PART 1 代码

![](https://img3.doubanio.com/view/group_topic/l/public/p492761560.webp)

if(prop("数值") >= 1, "−−−−−−−−−−♦︎ 100%", slice("−−−−−−−−−−", 0, floor(prop("数值") \* 10)) + "♦︎" + slice("−−−−−−−−−−", 0, ceil(10 - prop("数值") \* 10)) + " " + format(round(prop("数值") \* 100)) + "%")

![](https://img9.doubanio.com/view/group_topic/l/public/p492466246.webp)

if(prop("数值") >= 1, "✦✦✦✦✦✦✦✦✦✦ 100%", slice("✦✦✦✦✦✦✦✦✦✦", 0, floor(prop("数值") \* 10)) + slice("✧✧✧✧✧✧✧✧✧✧", 0, ceil(10 - prop("数值") \* 10)) + " " + format(round(prop("数值") \* 100)) + "%")

![](https://img2.doubanio.com/view/group_topic/l/public/p492466401.webp)

if(prop("数值") >= 1, "▓▓▓▓▓▓▓▓▓▓ 100%", slice("▓▓▓▓▓▓▓▓▓▓", 0, floor(prop("数值") \* 10)) + slice("░░░░░░░░░░", 0, ceil(10 - prop("数值") \* 10)) + " " + format(round(prop("数值") \* 100)) + "%")

![](https://img1.doubanio.com/view/group_topic/l/public/p492466649.webp)

if(prop("数值") >= 1, "⭐️⭐️⭐️⭐️⭐️⭐️⭐️⭐️⭐️⭐️ 100%", if(empty(prop("数值")), "0%", replaceAll(slice("xxxxxxxxxx", 0, floor(prop("数值") \* 10)), "x", "⭐️") + " " + format(round(prop("数值") \* 100)) + "%"))

![](https://img2.doubanio.com/view/group_topic/l/public/p492466751.webp)

if(prop("数值") >= 1, "🟦🟦🟦🟦🟦🟦🟦🟦🟦🟦 100%", replaceAll(slice("xxxxxxxxxx", 0, floor(prop("数值") \* 10)), "x", "🟦") + replaceAll(slice("xxxxxxxxxx", 0, ceil(10 - prop("数值") \* 10)), "x", "⬜️") + " " + format(round(prop("数值") \* 100)) + "%")

![](https://img9.doubanio.com/view/group_topic/l/public/p492466855.webp)

if(prop("数值") >= 1, "✅", if(empty(prop("数值")), "0%", slice("■■■■■■■■■■", 0, floor(prop("数值") \* 10)) + " " + format(round(prop("数值") \* 100)) + "%"))

![](https://img2.doubanio.com/view/group_topic/l/public/p492466972.webp)

if(prop("数值") >= 1, "∣∣∣∣∣∣∣∣∣∣ 100%", slice("∣∣∣∣∣∣∣∣∣∣", 0, floor(prop("数值") \* 10)) + slice("", 0, ceil(10 - prop("数值") \* 10)) + " " + format(round(prop("数值") \* 100)) + "%")

![](https://img2.doubanio.com/view/group_topic/l/public/p492472012.webp)

if(prop("数值") >= 1, "++++++++++", slice("++++++++++", 0, floor(prop("数值") \* 10)) + slice("−−−−−−−−−−", 0, ceil(10 - prop("数值") \* 10)))

![](https://img2.doubanio.com/view/group_topic/l/public/p492472082.webp)

if(prop("数值") >= 1, "·········· 100%", slice("··········", 0, floor(prop("数值") \* 10)) + slice("", 0, ceil(10 - prop("数值") \* 10)) + " " + format(round(prop("数值") \* 100)) + "%")

![](https://img1.doubanio.com/view/group_topic/l/public/p492472147.webp)

if(prop("数值") >= 1, "⚈⚈⚈⚈⚈⚈⚈⚈⚈⚈", slice("⚈⚈⚈⚈⚈⚈⚈⚈⚈⚈", 0, floor(prop("数值") \* 10)) + slice("⚆⚆⚆⚆⚆⚆⚆⚆⚆⚆", 0, ceil(10 - prop("数值") \* 10)))

![](https://img9.doubanio.com/view/group_topic/l/public/p492472216.webp)

if(prop("数值") >= 1, "✅", replaceAll(slice("xxxxxxxxxx", 0, floor(prop("数值") \* 10)), "x", "🌳") + replaceAll(slice("xxxxxxxxxx", 0, ceil(10 - prop("数值") \* 10)), "x", "🌱") + " " + format(round(prop("数值") \* 100)) + "%")

![](https://img9.doubanio.com/view/group_topic/l/public/p492472286.webp)

if(prop("数值") >= 1, "🌝🌝🌝🌝🌝🌝🌝🌝🌝🌝 100%", replaceAll(slice("xxxxxxxxxx", 0, floor(prop("数值") \* 10)), "x", "🌝") + replaceAll(slice("xxxxxxxxxx", 0, ceil(10 - prop("数值") \* 10)), "x", "🌚") + " " + format(round(prop("数值") \* 100)) + "%")

![](https://img1.doubanio.com/view/group_topic/l/public/p492477328.webp)

if(prop("数值") >= 1, "❤❤❤❤❤❤❤❤❤❤", replaceAll(slice("xxxxxxxxxx", 0, floor(prop("数值") \* 10)), "x", "❤") + replaceAll(slice("xxxxxxxxxx", 0, ceil(10 - prop("数值") \* 10)), "x", "🤍"))

![](https://img1.doubanio.com/view/group_topic/l/public/p492497958.webp)

是楼下姐妹分享的月亮进度条，我自己调整了一下

if(prop("数值") < 1, slice("🌕🌕🌕🌕🌕🌕🌕🌕🌕🌕", 0, floor(prop("数值") \* 10) \* 2) + if(prop("数值") \* 10 - floor(prop("数值") \* 10) <= 0, "", if(prop("数值") \* 10 - floor(prop("数值") \* 10) <= 0.3, "🌘", if(prop("数值") \* 10 - floor(prop("数值") \* 10) >= 0.7, "🌖", "🌗"))) + slice("🌑🌑🌑🌑🌑🌑🌑🌑🌑🌑", 0, floor(10 - prop("数值") \* 10) \* 2), "🌕🌕🌕🌕🌕🌕🌕🌕🌕🌕") + " " + format(prop("数值") \* 100) + "%"

如果你的数值是A/B形式的，可以用她帖子里的代码：

## PART 2 代码入门

如果只是想用进度条，没必要上面那一大串代码都认识。只需要知道什么是属性（property）就够了。简单来说，我们在notion里面新建表格，可以添加的列，都是属性

![](https://img1.doubanio.com/view/group_topic/l/public/p494981998.webp)

这些属性在代码里面表达的通用格式是

prop("属性名字")

（我上面那串代码之所以打了数值，是因为我的属性名字就叫数值，不是说那里来填数字。这个地方取什么名字都可以，看你新建的属性名字是什么）

属性有很多种类型，比如文本、数字等等，要用进度条，会公式（Formula）这个够了

![](https://img1.doubanio.com/view/group_topic/l/public/p494983567.webp)

公式就是自动运算，不需要你一个一个数字敲出来去算出百分比。算百分比的公式大家都知道，就是简单的除法。拿阅读进度来举例，在算出百分值之前，你需要有两个量：已阅读量和总页数。新建完这两个量之后（它们的属性类型必须是数字即Number），在属性类型是Formula的属性（叫什么名字都可以，这里我随便取个名字叫百分数）下输入：

prop("已阅读量")/prop("总页数")

表格会自动算出来了

然后你再新建一个属性，属性类型也是Formula，名字也是任意（这里我把它叫进度条）。然后把你想要的进度条代码复制粘贴进去，把所有prop("数值")中的数值二字，统统换成百分数。进度条就出来了

> 注意：双引号不能去！括号不能去！只能改中文

## PART 3 自定义进度条

1\. 没有百分比、想要加上去的，在倒数第一个括号前加上：

\+ " " + format(round(prop("数值") \* 100)) + "%"

![](https://img1.doubanio.com/view/group_topic/l/public/p492474269.webp)

![](https://img2.doubanio.com/view/group_topic/l/public/p492474322.webp)

![](https://img9.doubanio.com/view/group_topic/l/public/p492474426.webp)

记得最前面还要改一下100%时的样式，是【空格】+100%

如果不想要百分比，就把这部分删掉

2\. 想要单独改100%时的样式，只需要把>=1后面的冒号内修改成你想要的样式就好了

![](https://img1.doubanio.com/view/group_topic/l/public/p492475428.webp)

![](https://img2.doubanio.com/view/group_topic/l/public/p492475593.webp)

只需要复制10棵树，再加上【空格】+100%就好了

3\. 想要把表情替换成另外的样式

首先随便复制上面的有表情包的代码（必须要有表情包，不是普通符号）

![](https://img2.doubanio.com/view/group_topic/l/public/p492476733.webp)