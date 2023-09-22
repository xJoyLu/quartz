author:: null
source:: [iOS Widget小组件大小和位置(透明组件)_时光不染的博客-CSDN博客_ios widget 尺寸](https://blog.csdn.net/hzhnzmyz/article/details/119872090)
clipped:: [[2022-06-28]]
published:: 

#iOS #Swift #Widget

![](https://img-blog.csdnimg.cn/3de8c9c538384e2896eafa7776362235.png) ## size

小组件获取组件大小  
1.在Widget获取比较容易，通过`context.displaySize`获取

```
	context.displaySize
	
	struct SmallProvider: IntentTimelineProvider {
    func getTimeline(for configuration: SmallIntent, in context: Context, completion: @escaping (Timeline<SmallEntry>) -> Void) {
    	print(context.displaySize)

 	func placeholder(in context: Context) -> SmallEntry {
        print(context.displaySize)
    }

    func getSnapshot(for configuration: SmallIntent, in context: Context, completion: @escaping (SmallEntry) -> ()) {
        print(context.displaySize)
    }

```

2.在主程序获取

机型

屏幕尺寸(pt)

小组件(pt)

中组件(pt)

大组件(pt)

5 / 5s /SE

320x568

140x140

291x140

291x310

6 / 6s / 7 / 8 / SE2

375x667

148x148

321x148

321x324

6p / 6sp / 7p / 8p

375x812

155x155

329x155

329x345

x / xs / 11pro / 12mini

390x844

158x158

338x158

338x354

xr / xsmax / 11 / 11promax

414x736

157x157

348x157

348x351

12 / 12pro

414x896

169x169

360x169

369x379

12promax

428x926

170x170

364x170

364x382

## 小号组件坐标

机型

屏幕尺寸(pt)

左上(CGPoint)

右上(CGPoint)

左中(CGPoint)

右中(CGPoint)

左下(CGPoint)

右下(CGPoint)

5 / 5s /SE

320x568

(x:14,y:30)

(x:165,y:30)

(x:14,y:200)

(x:165,y:200)

(x:-,y:-)

(x:-,y:-)

6 / 6s / 7 / 8 / SE2

375x667

(x:27,y:30)

(x:200,y:30)

(x:27,y:206)

(x:200,y:206)

(x:27,y:382)

(x:200,y:382)

6p / 6sp / 7p / 8p

375x812

(x:23,y:71)

(x:197,y:71)

(x:23,y:261)

(x:197,y:261)

(x:23,y:451)

(x:197,y:451)

x / xs / 11pro / 12mini

390x844

(x:26,y:77)

(x:206,y:77)

(x:26,y:273)

(x:206,y:273)

(x:26,y:469)

(x:206,y:469)

xr / xsmax / 11 / 11promax

414x736

(x:33,y:38)

(x:224,y:38)

(x:33,y:232)

(x:224,y:232)

(x:33,y:426)

(x:224,y:426)

12 / 12pro

414x896

(x:27,y:76)

(x:218,y:76)

(x:27,y:286)

(x:218,y:286)

(x:27,y:496)

(x:218,y:496)

12promax

428x926

(x:32,y:82)

(x:226,y:82)

(x:32,y:294)

(x:226,y:294)

(x:32,y:506)

(x:226,y:506)

## 中号组件坐标

机型

屏幕尺寸(pt)

上(CGPoint)

中(CGPoint)

下(CGPoint)

5 / 5s /SE

320x568

(x:14,y:30)

(x:14,y:200)

(x:-,y:-)

6 / 6s / 7 / 8 / SE2

375x667

(x:27,y:30)

(x:27,y:206)

(x:27,y:382)

6p / 6sp / 7p / 8p

375x812

(x:23,y:71)

(x:23,y:261)

(x:23,y:451)

x / xs / 11pro / 12mini

390x844

(x:26,y:77)

(x:26,y:273)

(x:26,y:469)

xr / xsmax / 11 / 11promax

414x736

(x:33,y:38)

(x:33,y:232)

(x:33,y:426)

12 / 12pro

414x896

(x:27,y:76)

(x:27,y:286)

(x:27,y:496)

12promax

428x926

(x:32,y:82)

(x:32,y:294)

(x:32,y:506)

## 大号组件坐标

机型

屏幕尺寸(pt)

上(CGPoint)

下(CGPoint)

5 / 5s /SE

320x568

(x:14,y:30)

(x:-,y:-)

6 / 6s / 7 / 8 / SE2

375x667

(x:27,y:30)

(x:27,y:206)

6p / 6sp / 7p / 8p

375x812

(x:23,y:71)

(x:23,y:261)

x / xs / 11pro / 12mini

390x844

(x:26,y:77)

(x:26,y:273)

xr / xsmax / 11 / 11promax

414x736

(x:33,y:38)

(x:33,y:232)

12 / 12pro

414x896

(x:27,y:76)

(x:27,y:286)

12promax

428x926

(x:32,y:82)

(x:32,y:294)

## 代码

以下是测量的小组件在屏幕上的几个位置坐标，小组件大小和位置都可以通过以下数据换算得到

![](https://img-blog.csdnimg.cn/76245d14662f4195bc101c8cebf130d5.png)

数组结构为`[X1,X2,X3,Y1,Y2,Y3]`

```
let deviceInfos:[String:Array<Int>] = [
    "320x568":[14,165,305,30,200,370], 
    "375x667":[27,200,348,30,206,382], 
    "375x812":[23,197,352,71,261,451], 
    "390x844":[26,206,364,77,273,469], 
    "414x736":[33,224,381,38,232,426], 
    "414x896":[27,218,387,76,286,496], 
    "428x926":[32,226,396,82,294,506], 
]
```

#### 获取组件宽度

小组件尺寸为`X3-X2`的正方形  
中组件宽度为`X3-X1`，高度等同小组件 `X3-X2`  
大组件宽度为`X3-X1`, 高度为`(Y2-Y1) + (X3-X2)`

小组件高度为X3-X2

```
func GetWidgetSize(_ widgetType:WidgetSizeEnum) -> CGSize {
    let wxh:String =  "\(Int(WIDTH))x\(Int(HEIGHT))"
    
    
    if !deviceInfos.keys.contains(wxh) {
        return CGSize(width: -1, height: -1)
    }
    switch widgetType {
    case .small:
        let smallWidth = deviceInfos[wxh]![2] - deviceInfos[wxh]![1]
        return CGSize(width: smallWidth, height: smallWidth)
    case .medium:
        let mediumWidth = deviceInfos[wxh]![2] - deviceInfos[wxh]![0]
        let mediumHeight = deviceInfos[wxh]![2] - deviceInfos[wxh]![1]
        return CGSize(width: mediumWidth, height: mediumHeight)
    case .large:
        let largeWidth = deviceInfos[wxh]![2] - deviceInfos[wxh]![0]
        let largeHeight = deviceInfos[wxh]![4] - deviceInfos[wxh]![3] + deviceInfos[wxh]![2] - deviceInfos[wxh]![1]
        return CGSize(width: largeWidth, height: largeHeight)
    }
}

enum WidgetSizeEnum {
    case small
    case medium
    case large
}
```

#### 获取小组件位置

`320x568`的机型同屏只有4个位置能放小组件，其他尺寸比例的机型为6个

```

enum WidgetSizeEnum {
    case topLeft
    case topRight
    case middleLeft
    case middleRight
    case bottomLeft
    case bottomRight
}

func GetSmallWidgetPos(_ widgetPos:SWidgetPosEnum)->CGPoint{
    let wxh:String =  "\(Int(WIDTH))x\(Int(HEIGHT))"
    
    if !deviceInfos.keys.contains(wxh) {
        return CGPoint(x: -1, y: -1)
    }
    
    if(wxh == "320x568") {
        switch widgetPos {
        case .topLeft:
            return CGPoint(x: deviceInfos[wxh]![0], y: deviceInfos[wxh]![3])
        case .topRight:
            return CGPoint(x: deviceInfos[wxh]![1], y: deviceInfos[wxh]![3])
        case .middleLeft, .bottomLeft:
            return CGPoint(x: deviceInfos[wxh]![0], y: deviceInfos[wxh]![4])
        case .middleRight, .bottomRight:
            return CGPoint(x: deviceInfos[wxh]![1], y: deviceInfos[wxh]![4])
    } else {
        switch widgetPos {
        case .topLeft:
            return CGPoint(x: deviceInfos[wxh]![0], y: deviceInfos[wxh]![3])
        case .topRight:
            return CGPoint(x: deviceInfos[wxh]![1], y: deviceInfos[wxh]![3])
        case .middleLeft:
            return CGPoint(x: deviceInfos[wxh]![0], y: deviceInfos[wxh]![4])
        case .middleRight:
            return CGPoint(x: deviceInfos[wxh]![1], y: deviceInfos[wxh]![4])
        case .bottomLeft:
            return CGPoint(x: deviceInfos[wxh]![0], y: deviceInfos[wxh]![5])
        case .bottomRight:
            return CGPoint(x: deviceInfos[wxh]![1], y: deviceInfos[wxh]![5])
        }
        
    }
}
```

#### 获取中组件位置

`320x568`的机型同屏只有上下2个位置能放中组件，其他尺寸比例的机型为上中下3个

```

enum WidgetSizeEnum {
    case top
    case middle
    case bottom
}

func GetMiddleWidgetPos(_ widgetPos:MWidgetPosEnum)->CGPoint{
    let wxh:String =  "\(Int(WIDTH))x\(Int(HEIGHT))"
    
    if !deviceInfos.keys.contains(wxh) {
        return CGPoint(x: -1, y: -1)
    }
    
    if(wxh == "320x568") {
        switch widgetPos {
        case .top:
            return CGPoint(x: deviceInfos[wxh]![0], y: deviceInfos[wxh]![3])
        case .middle, .bottom:
            return CGPoint(x: deviceInfos[wxh]![0], y: deviceInfos[wxh]![4])
    } else {
        switch widgetPos {
        case .top:
            return CGPoint(x: deviceInfos[wxh]![0], y: deviceInfos[wxh]![3])
        case .middle:
            return CGPoint(x: deviceInfos[wxh]![0], y: deviceInfos[wxh]![4])
        case .bottom:
            return CGPoint(x: deviceInfos[wxh]![0], y: deviceInfos[wxh]![5])
        }
    }
}

```

#### 获取大组件位置

`320x568`的机型同屏只有1个位置能放大组件，其他尺寸比例的机型为上中下2个

```

enum WidgetSizeEnum {
    case top
    case bottom
}

func GetLargeWidgetPos(_ widgetPos:LWidgetPosEnum)->CGPoint{
    let wxh:String =  "\(Int(WIDTH))x\(Int(HEIGHT))"
    
    if !deviceInfos.keys.contains(wxh) {
        return CGPoint(x: -1, y: -1)
    }
    
    if(wxh == "320x568") {
        return CGPoint(x: deviceInfos[wxh]![0], y: deviceInfos[wxh]![3])
    } else {
        switch widgetPos {
        case .top:
            return CGPoint(x: deviceInfos[wxh]![0], y: deviceInfos[wxh]![3])
        case .bottom:
            return CGPoint(x: deviceInfos[wxh]![0], y: deviceInfos[wxh]![4])
        case .unknown,.alpha1:
            return CGPoint(x: 0, y: 0)
        }
    }
}
```