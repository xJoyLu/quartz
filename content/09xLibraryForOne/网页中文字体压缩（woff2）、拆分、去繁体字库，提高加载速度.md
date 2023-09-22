author:: null
source:: [网页中文字体压缩（woff2）、拆分、去繁体字库，提高加载速度](https://www.imaegoo.com/2020/chinese-font-compress/)
clipped:: [[2022-10-14]]
published:: 

从客户得到的网页字体足足有 10MB 大小，会严重拖慢网页加载，如何处理？

阅读下面的解决方法前，建议先阅读[网页字体优化](https://developers.google.cn/web/fundamentals/performance/optimizing-content-efficiency/webfont-optimization?hl=zh-cn)，了解一些基本知识，以及，为什么。

### [](#字体去繁体 "字体去繁体")字体去繁体

GBK 结尾的字体偏大的原因是包含庞大的繁体字库，大多数网页并不需要，可以使用 [fontTools](https://github.com/fonttools/fonttools) 得到字体的简体中文子集。

安装 Python 3.7 和 pip，再运行 `pip install fonttools` 来安装 fontTools。

运行 `pyftsubset --help` 查看命令帮助，得知需要 Unicode 列表来提取字体子集。

我们看一下 Unicode 表：

字符集

字数

Unicode 编码

基本汉字

20902字

4E00-9FA5

基本汉字补充

74字

9FA6-9FEF

扩展A

6582字

3400-4DB5

扩展B

42711字

20000-2A6D6

扩展C

4149字

2A700-2B734

扩展D

222字

2B740-2B81D

扩展E

5762字

2B820-2CEA1

扩展F

7473字

2CEB0-2EBE0

扩展G

4939字

30000-3134A

康熙部首

214字

2F00-2FD5

部首扩展

115字

2E80-2EF3

兼容汉字

477字

F900-FAD9

兼容扩展

542字

2F800-2FA1D

PUA(GBK)部件

81字

E815-E86F

部件扩展

452字

E400-E5E8

PUA增补

207字

E600-E6CF

汉字笔画

36字

31C0-31E3

汉字结构

12字

2FF0-2FFB

汉语注音

43字

3105-312F

注音扩展

22字

31A0-31BA

〇

1字

3007

\* 转载自[汉字 Unicode 编码范围](https://www.qqxiuzi.cn/zh/hanzi-unicode-bianma.php)

这里会遇到一个问题，基本汉字（4E00-9FA5）区间内，简体字、繁体字是交叉的，没有一个固定的简体区间和繁体区间，所以需要一个[简体字的 Unicode 表](https://www.ansell-uebersetzungen.com/gbuni.html)，经过整理，我得到最终的 unicodes 文件，再加入 latin 的区间（0000-00FF），以及[中文标点符号](https://blog.csdn.net/COCO56/article/details/87618925)，作为参数传入 fontTools 获得字体子集。

你可以直接从 [Gist](https://gist.github.com/imaegoo/d64e5088b723c2e02c40985f55ff12db) 下载我整理好的文件：[sc\_unicode.txt](https://gist.githubusercontent.com/imaegoo/d64e5088b723c2e02c40985f55ff12db/raw/5ebd2ce49418c73459a9dfe050483409306a6c1d/sc_unicode.txt)，并和需要处理的字体放在一起。

1  

pyftsubset fang-zheng-hei-ti-gbk.ttf --unicodes-file=sc\_unicode.txt  

该命令会压缩方正黑体，执行后可在同目录下找到 `fang-zheng-hei-ti-gbk.subset.ttf`，字体大小变为原来的 27.6%

1  
2  

2020/05/13  10:53         2,823,032 fang-zheng-hei-ti-gbk.subset.ttf  
2020/05/12  11:09        10,210,812 fang-zheng-hei-ti-gbk.ttf  

### [](#字体压缩 "字体压缩")字体压缩

编译安装 [Google woff2](https://github.com/google/woff2)（笔者的环境是 Ubuntu 16.04）

1  
2  
3  
4  

sudo apt-get install -y git g++ make  
git clone --recursive https://github.com/google/woff2.git  
cd woff2  
make clean all  

再压缩字体

1  
2  
3  

./woff2\_compress ./fang-zheng-hei-ti-gbk.ttf  
Processing ./fang-zheng-hei-ti-gbk.ttf => ./fang-zheng-hei-ti-gbk.woff2  
Compressed 6760548 to 3704803.  

1  
2  

2020/05/12  11:09        10,210,812 fang-zheng-hei-ti-gbk.ttf  
2020/05/12  17:29         3,704,896 fang-zheng-hei-ti-gbk.woff2  

可见对方正黑体进行压缩后，压缩比 36.3%

如果配合去繁体使用，最终字体大小只有 1.09 MB (1,148,408 bytes)，效果显著。

最终使用时，还需要考虑 [woff2 的浏览器兼容问题](https://www.caniuse.com/#search=woff2)，提供多种格式（woff 和 ttf）保证兼容。

### [](#字体拆分 "字体拆分")字体拆分

请阅读：[Unicode-range 子集内嵌](https://developers.google.cn/web/fundamentals/performance/optimizing-content-efficiency/webfont-optimization?hl=zh-cn#unicode-range_%E5%AD%90%E9%9B%86%E5%86%85%E5%B5%8C)

### [](#参考资料 "参考资料")参考资料

1.  网页字体优化 [https://developers.google.cn/web/fundamentals/performance/optimizing-content-efficiency/webfont-optimization?hl=zh-cn](https://developers.google.cn/web/fundamentals/performance/optimizing-content-efficiency/webfont-optimization?hl=zh-cn)
2.  fontTools Docs [https://fonttools.readthedocs.io/en/latest/](https://fonttools.readthedocs.io/en/latest/)
3.  汉字 Unicode 编码范围 [https://www.qqxiuzi.cn/zh/hanzi-unicode-bianma.php](https://www.qqxiuzi.cn/zh/hanzi-unicode-bianma.php)
4.  Unicode Table for Simplified Chinese Characters [https://www.ansell-uebersetzungen.com/gbuni.html](https://www.ansell-uebersetzungen.com/gbuni.html)

 [Landscape Vectors by Vecteezy](https://www.vecteezy.com/free-vector/landscape)