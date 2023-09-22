author:: xww2652008969
source:: [某违法视频app解密 - 『移动安全区』 - 吾爱破解 - LCG](https://www.52pojie.cn/thread-1647519-1-1.html)
clipped:: [[2022-06-11]]
published:: 

#稍后阅读

`jadx`

`Fiddler.exe`

## 1，播放视频

播放app里视频(因为视频类容属于非法内容，所以打了很多码，请谅解)，发现提示需要开通vip。开始抓包

![CAEKg.jpg](https://s1.328888.xyz/2022/06/10/CAEKg.jpg)

## 2，抓包(因为数据是https，设备经过处理)

![ChUYe.png](https://s1.328888.xyz/2022/06/10/ChUYe.png)

发现图中url 像是视频地址，获取返回数据

![ChyXq.png](https://s1.328888.xyz/2022/06/10/ChyXq.png)

这个应该是加密，只能逆向app

![ChJyA.png](https://s1.328888.xyz/2022/06/10/ChJyA.png)

通过搜索关键字发现上面代码，encData是先用`AES/CBC/PKCS&Padding`加密然后再使用`` `base64``加密，需要寻找token。

因为`token`联想到验证发现请求头`Authorization`然后通过通过关键字查询发现一下代码

![image-20220610014836758](https://www.52pojie.cn/C%3A/Users/w/AppData/Roaming/Typora/typora-user-images/image-20220610014836758.png)

通过关键字查阅代码

![ChfPi.png](https://s1.328888.xyz/2022/06/10/ChfPi.png)

怀疑`token`是Authorization，尝试解密，编写代码(token是隐私所以不写出来)运行

 *复制代码* *隐藏代码* `String encData = "ua6b7wMaDJkIQyVYFEVhykFKqcoCSrnAQrbnBQUJmS6GuAJwr8Qp6HGLiIE9q9qooxgVb/bVMkiVRIqOicXsUdJz9ftYhL0W86T/MIkJ2OODQG1yM1N7uXpIa7Zm6C3aGfTsqyqGwkoJzY6gpGSfLgY3g3NTSygZQcGjo3UqSlAYEbGtUufXG6rLVSBUbLWUFuaiwnifDcDpr47kzIjP6A4zOnxyJYj3iXky+zkbGJwNzsxW04gwr+mu05yFMzIbboQQztaLHTds7O9ZOwBG0FwwtR+OI16SvruzZNQI46VN/0lpNOnRIdXWJ22JwP0v24ULGBz4RSqcBtk4F9efuB2C8xjzrbgm3NGMOWgKdXDa8U02jDfmmMjrQO6weM2MQ8SfDTKZTg9O7auUOIgRij/qOoiUkfKN5prGkFWVpZJxhdSjSRZjLc7pjQnm0C4IZsecZYYgJ14pXrHc5nVuSSdkxQDwzTkNltuIDixy/OxWL4Yct92wpgY3MUSc5UZW/O1g53LSkQsSabt0WMHPJb7qbWSLb19TNUnLBszuxpGLCjQ5Bl4KNrjrWgRDGQT0eI83NxDsuBs2P+sgWL7gQPwoXEtHGnGtt7tWhxPanEhF827erO1OxNLvozQIew701w4dTGqeUjWL3+BGG3ZGXeDQKwBREUPWq723rmDiu5Mj9HNF27UA48ub5A4ScgTzomz81Z8q/ZcBi+QNAbgrcKW88u2sX6yafmjSYY/OApVyGFj9cgTSxmhYyKEGo+xcaJ7q5RMwPyRp11RqLMYV9vKXY0Q5eZ/tWE7Y8bJkCI2IREsQ3/eUAHVdoNQyeOzuZyFi7eI7AkhZAvCkceJSatWzke4UIMMcVDB/A6vWpC3X6E954IIeHbOb00cQNoUUMBw5q+nl+CY5qjiANE/p36wPNeIxBV92U1BduviZvx8N3SckF/73l7uE6JGNaJJpul1jUkolMxtsnRvffnV8EwFKNEzujvzRWNrwWKsg41a2Y12h+kL/BeRtRdCKub/BdMojn8Wd6o5xPDduGXlpLg==";
        String token = "这是token";
        try {
            String substring = token.substring(2, 18);
            SecretKeySpec secretKeySpec = new SecretKeySpec(substring.getBytes("UTF-8"), "AES");
            Cipher cipher = Cipher.getInstance("AES/CBC/PKCS5Padding ");
            cipher.init(2, secretKeySpec, new IvParameterSpec(substring.getBytes()));
            String str = new String(cipher.doFinal(Base64.getDecoder().decode(encData)));
            System.out.println(str);
        } catch (Exception e) {
            
            System.out.println(e);
        }`

![ChCMT.png](https://s1.328888.xyz/2022/06/10/ChCMT.png)

生成字符串观察为json，优化一下并且发现m3u8地址，这个是视频地址，访问地址获取m3u8文件，`previewurl`为展示视频地址，`videourl`为完整视频地址,

`domain/enc.key`为假的key，文件AES加密,需要寻找key

![ChRGX.png](https://s1.328888.xyz/2022/06/10/ChRGX.png)

查阅代码寻找关键字发现key是在本地

![ChYlZ.png](https://s1.328888.xyz/2022/06/10/ChYlZ.png)

![ChTOC.png](https://s1.328888.xyz/2022/06/10/ChTOC.png)

发现上面二个文件 查看一下

![Chcxg.png](https://s1.328888.xyz/2022/06/10/Chcxg.png)

kb文件就是key

使用开源工具`N_m3u8DL-CLI`尝试解密,解密完成

![Chwh1.png](https://s1.328888.xyz/2022/06/10/Chwh1.png)

## 3分析请求头

解密视频后需要分析往上层分析

![ChfPi.png](https://s1.328888.xyz/2022/06/10/ChfPi.png)

因为抓包时发现请求头`t`和`s`参数会变化都不一样，通过分析`t`为时间戳

![ChrAv.png](https://s1.328888.xyz/2022/06/10/ChrAv.png)

`s`为`t`的某段数据数据的`md5`加密

上层更简单简单抓包就可以发现api，不做叙述。  
PS;因为样本是内容是非法的，所以不提供样本