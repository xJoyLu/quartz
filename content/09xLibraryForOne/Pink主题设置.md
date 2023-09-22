- 最新版本更新：2022年07月08日

在wp_options
![](https://img.jk.lu/202211211958475.jpg)

### Banner用法示例
banner用法示例：

https://static.kam.space/banner/2205.webp;

https://static.kam.space/banner/2203.webp 80%,https://static.kam.space/banner/2211.webp;

https://static.kam.space/banner/2204.webp,https://static.kam.space/banner/2202.webp;

https://static.kam.space/banner/2207.webp,https://static.kam.space/banner/2209.webp 90%;

完整格式：

白天图片 + 空格 + Y轴定位 + ，逗号 + 夜晚图片 + 空格 + Y轴定位 + ；分号

url 90%,url 70%;




bgm用法示例：

https://static.kam.space/bgm/一个人过冬天.mp3;

https://static.kam.space/bgm/妄想止疼.mp3;

https://static.kam.space/bgm/close-your-eyes.mp3 闭上眼睛


完整格式：

歌曲地址+空格+歌名+分号

换行符 = 分号，歌名填写不填写都可以
### 常见设置
- 备案
	- 这个是备案插件，若需要请安装 zh_cn_l10n_icp_num.php
- 404
	- 需要服务器设置伪静态规则
- 移动端修改配置
	- 在wp_options
	- 数据库添加参数，以控制是否开启移动模式，如果需要手机上也使用pc模式，可以设置为N以关闭，