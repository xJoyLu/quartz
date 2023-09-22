#API #Unsplash
## Unsplash

如果你想使用免费版权的图片时，无论你是否用于商业用途，[Unsplash](https://unsplash.com/) 是不错的选择。

我自己也经常用它来制作大型背景图片，例如：[https://www.imyangyong.com](https://www.imyangyong.com/) 。

虽然他们为开发人员提供了很棒的 API，但他们也提供了通过 URL 访问随机图片的选项。

## [](https://www.imyangyong.com/blog/2020/06/javascript/%E4%BD%BF%E7%94%A8%20Unsplash%20API%20%E7%94%9F%E6%88%90%E9%9A%8F%E6%9C%BA%E5%9B%BE%E7%89%87/#1-%E9%BB%98%E8%AE%A4%E9%9A%8F%E6%9C%BA "1. 默认随机")1. 默认随机

请看这个例子，从他们巨大的存储中生成随机的图片。

https://source.unsplash.com/random  

## [](https://www.imyangyong.com/blog/2020/06/javascript/%E4%BD%BF%E7%94%A8%20Unsplash%20API%20%E7%94%9F%E6%88%90%E9%9A%8F%E6%9C%BA%E5%9B%BE%E7%89%87/#%E6%8C%87%E5%AE%9A%E7%94%A8%E6%88%B7 "指定用户")指定用户

我们还可以从特定用户账号中生成随机图像。URL 格式是这样的:

https://source.unsplash.com/user/{USERNAME}  

你可以尝试单击下面的链接，从我的账号中随机生成图片：

[https://source.unsplash.com/user/angusyang9/likes](https://source.unsplash.com/user/angusyang9/likes)

## [](https://www.imyangyong.com/blog/2020/06/javascript/%E4%BD%BF%E7%94%A8%20Unsplash%20API%20%E7%94%9F%E6%88%90%E9%9A%8F%E6%9C%BA%E5%9B%BE%E7%89%87/#3-%E6%8C%87%E5%AE%9A%E5%B0%BA%E5%AF%B8 "3. 指定尺寸")3. 指定尺寸

还有一个选项可以设置要生成的图像的大小。像这样:

https://source.unsplash.com/random/{WIDTH}x{HEIGHT}  

让我们生成下 300 x 300 大小的图片：

[https://source.unsplash.com/random/300×300](https://source.unsplash.com/random/300%C3%97300)

## [](https://www.imyangyong.com/blog/2020/06/javascript/%E4%BD%BF%E7%94%A8%20Unsplash%20API%20%E7%94%9F%E6%88%90%E9%9A%8F%E6%9C%BA%E5%9B%BE%E7%89%87/#4-%E4%BE%9D%E6%8D%AE%E5%85%B3%E9%94%AE%E8%AF%8D%E6%90%9C%E7%B4%A2 "4. 依据关键词搜索")4. 依据关键词搜索

这个真的很棒。你可以从搜索词生成图像。让我们搜索下城市和夜晚（非常有创意）：

[https://source.unsplash.com/random/?city,night](https://source.unsplash.com/random/?city,night)

当然，你可以与尺寸配合使用：

[https://source.unsplash.com/random/900×700/?fruit](https://source.unsplash.com/random/900%C3%97700/?fruit)

## [](https://www.imyangyong.com/blog/2020/06/javascript/%E4%BD%BF%E7%94%A8%20Unsplash%20API%20%E7%94%9F%E6%88%90%E9%9A%8F%E6%9C%BA%E5%9B%BE%E7%89%87/#%E4%BB%A3%E7%A0%81%E7%A4%BA%E4%BE%8B "代码示例")代码示例

以下是 react 中的代码片段：

class RandomImg extends React.Component {  
  constructor() {  
    super();  
    this.state = {  
      bgImageUrl: require('./default.jpeg')  
    }  
  }  
    
  componentDidMount() {  
    this.generateImage();  
  }  
    
  generateImage(){  
    fetch(`https://source.unsplash.com/random/?people`).then((response) => {  
      preloadImage(response.url);  
    })  
	}  
    
  preloadImage(url) {  
    let img = new Image();  
    img.src = url;  
    img.onload = () => {  
      this.setState({  
        bgImageUrl: url  
      });  
    }  
	}  
    
  render() {  
    return <img src={bgImageUrl} />  
  }  
}  

## [](https://www.imyangyong.com/blog/2020/06/javascript/%E4%BD%BF%E7%94%A8%20Unsplash%20API%20%E7%94%9F%E6%88%90%E9%9A%8F%E6%9C%BA%E5%9B%BE%E7%89%87/#%E5%8F%82%E8%80%83%E9%93%BE%E6%8E%A5 "参考链接")参考链接

-   [Generate Random Images From Unsplash Without Using The API](https://awik.io/generate-random-images-unsplash-without-using-api/)