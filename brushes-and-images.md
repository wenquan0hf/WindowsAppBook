# 画笔和图像

画笔想必大家都不陌生，这里系统的介绍一下好了。先来介绍纯色画笔。

## 纯色画笔

最简单的纯色画笔就是已经定义好名字的啦，比如 Red 和 Green 这种，据说一共有 256 种已命名的，所以基本已经够用啦。XAML 解析器会自动将这些颜色名称链接到 Color 结构。

还有就是传说中的十六进制颜色值，它可以定义精确的 24 位颜色值，其中有 8 位用于 SolidColorBrush。如下代码所示的，alpha="FF"，红色="55"，绿色="00"，蓝色="88"。

```
<Rectangle Width="200" Height="100" Fill="#FF550088" />
```

还有一种称为属性元素语法。具体用法如下，其中 Opacity 就是透明度咯。

```
  <Rectangle Width="200" Height="100">
     <Rectangle.Fill>
        <SolidColorBrush Color="Yellow" Opacity="0.3" />
     </Rectangle.Fill>
  </Rectangle>
```

## 渐变画笔

除了纯色画笔外，还有渐变画笔。小时候学 PhotoShop 的时候最喜欢渐变画笔了。

LinearGradientBrush 会沿着一条称为渐变轴直线来进行渐变以绘制一个区域。我们还是拿 Rectangle 来做示例。

```
   <Rectangle Width="200" Height="100">
            <Rectangle.Fill>
                <LinearGradientBrush StartPoint="0,0" EndPoint="1,1">
                    <GradientStop Color="Green" Offset="0.0" x:Name="GradientStop1"/>
                    <GradientStop Color="Blue" Offset="0.25" x:Name="GradientStop2"/>
                    <GradientStop Color="Wheat"  Offset="0.7" x:Name="GradientStop3"/>
                    <GradientStop Color="Yellow" Offset="0.75" x:Name="GradientStop4"/>
                    <GradientStop Color="Gold" Offset="1.0" x:Name="GradientStop5"/>
                </LinearGradientBrush>
            </Rectangle.Fill>
        </Rectangle>
```

![](images/45.png)

通过改变 StartPoint 和 EndPoint 的属性值可以创建各种渐变哦，比如垂直和水平方向的渐变，还可以颠倒渐变方向，甚至还可以加快渐变速度呢。

## 直接添加图片

除了用着两种画笔外，还可以直接将图片添加进来呢。

```
 <Ellipse Height="100" Width="200">
    <Ellipse.Fill>
        <ImageBrush ImageSource="9327.jpg"/>
    </Ellipse.Fill>
</Ellipse>
```

效果如下咯，主要是有一张合适的图片啦。

![](images/46.png)

既然用到了 ImageBrush，那就来看看 Image 和 ImageBrush 的区别好了。前者主要用来呈现图像，后者则为其他对象绘制为一个图像。

## Stretch 属性

对于 Image，我们可以来拉伸图像，也就是 Stretch 属性：

- None：图像不经过拉伸。如果源图像比所留给 Image 的区域大，那么就会被剪切。
- Uniform：按照纵横比来缩放图像。
- UniformToFill：按照纵横比来填满所有区域，这意味着可能会有一部分不可见。
- Fill。因为不保留纵横比而填满屏幕，所以图像部分全部可见，但会产生画面变形（失真）。

具体效果见下图（来源于网络）。

![](images/47.png)

## Clip 属性

用 Clip 属性可以对图像进行剪裁，Rect 属性在上一篇博客中用过许多次，前 2 个值为起始点的 X 轴和 Y 轴坐标，后 2 个值为终点的 X 轴和 Y 轴坐标。

```
<Image Source="9327.jpg">
    <Image.Clip>
        <RectangleGeometry Rect="10,10,100,100"/>
    </Image.Clip>
</Image>
```

Image 和 ImageBrush 能处理的图像格式有如下几种：

- JPEG XR
- 图标（ICO）
- 位图（BMP）
- 图像交换格式（GIF）
- 联合图像专家组（JPEG）
- 可移植网络图像（PNG）
- 标记图像文件格式（TIEF）