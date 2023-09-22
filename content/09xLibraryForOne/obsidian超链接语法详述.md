obsidian超链接语法详述 by [Ryooo](https://publish.obsidian.md/chinesehelp/07+%E4%BF%A1%E6%81%AF%E6%BA%90%E4%B8%8E%E8%B4%A1%E7%8C%AE%E8%80%85/Ryooo)  
ob的插入基于markdown的插入图片和插入链接衍生。

### 图片

`![图片替代文字](图片地址)`语法是可取的，ob支持用这种方式插入网络图片，但是本地图片似乎只支持vault内的图片。  
ob默认以`![[]]`的形式插入图片，并在当前页面中显示。  
ob支持`[[Pasted image 256.png]]`插入vault内的图片，图片不一定需要在附件文件夹中。但是这样是不显示的。、

### 链接

ob支持`[链接文字](链接地址 "Title")`，需要注意的是如果链接文字为空链接是不显示的。ob也支持[自动连接](https://publish.obsidian.md/chinesehelp/01+2021%E6%96%B0%E6%95%99%E7%A8%8B/Markdown#%E8%87%AA%E5%8A%A8%E8%BF%9E%E6%8E%A5) 。

### note

`[[]]`以link的形式插入note。这个可以通过`[[filename#header]]`的方式引用到更细的层级，也可以用`[[filename|代替文本]]`的方式进行文本替换  
`![[]]`会将插入的note显示在当前页，类似图片。这个等价于`![](note名字)`  
`[链接文字](note name)`会以链接方式插入note。这个和`[[]]`不同在于，这种方式不会自动显示note名字，需要在链接文字中填写。

### 文件

`[文字](file:///文件路径)`可以打开本地文件，路径中需要使用`/`，文件名需要全英文，空格需要重编码成%20。目前只支持绝对路径  
[猫](file:///D:/Providing%20NotesForReview.docx)