# 用浮出控件做预览效果

在前面学习控件的时候，我们已经见过了 MessageDialog 了，关于 Button 还有一个浮出控件 Flyout 哦。具体是怎样用呢？接下来就一起看看。

我们还是延续前面的那个示例好了，那么，代码来了。

```
        <Button x:Name="btnWhat" Content="这是什么？">
            <Button.Flyout>
                <Flyout>
                    <StackPanel>
                        <TextBlock Width="430" Style="{StaticResource BaseTextBlockStyle}"
                                   Text="噢！你刚刚又踩到地雷了，要撤销吗？" Foreground="Red" FontSize="25"/>
                        <Button Click="btnUndo_Click" Margin="12" Content="撤销"/>
                    </StackPanel>
                </Flyout>
            </Button.Flyout>
        </Button>
```

当我们点击了撤销按钮后，当然需要 btnWhat 按钮的 Flyout 消失掉，这个嘛，也只要 1 行代码啦。另外这个踩雷的逻辑这里就不展开啦.

```
private void btnUndo_Click(object sender, RoutedEventArgs e)
{
     btnWhat.Flyout.Hide();
}
```

更为重要的是在于这些在 WP8 上也是通用的，这才是核心所在。既然这一篇教程主要是浮出控件，如果可以借助浮出产生预览图像的效果会不会很棒呢？先来看张运行截图吧。

![](images/30.png)

以下都是代码啦，什么 Binding 呀之类的都不用管啦。需要注意的地方也就是那些 Height 和 Width 可能需要拿来调整一下。

```
   <Page.Resources>
        <Flyout x:Key="ResourceFlyoutImage" Placement="Right">                            
            <Image Source="{Binding Path=Source}" MaxHeight="800" MaxWidth="1400" Stretch="Uniform"/>
            <Flyout.FlyoutPresenterStyle>
                <Style TargetType="FlyoutPresenter">
                    <Setter Property="MinHeight" Value="900"/>
                    <Setter Property="MinWidth"  Value="1600"/>
                    <Setter Property="BorderThickness" Value="3"/>
                    <Setter Property="Background" Value="Wheat"/>
                    <Setter Property="BorderBrush" Value="Green"/>
                    <Setter Property="ScrollViewer.ZoomMode" Value="Enabled"/>        
                </Style>
            </Flyout.FlyoutPresenterStyle>
        </Flyout>
    </Page.Resources>    
    <Grid>
        <StackPanel HorizontalAlignment="Left" Orientation="Vertical">
            <Image Source="Assets/14152.jpg" Width="100" Height="100" Margin="12" Tapped="img_Tapped"  
                   FlyoutBase.AttachedFlyout="{StaticResource ResourceFlyoutImage}"                        
                   DataContext="{Binding RelativeSource={RelativeSource Mode=Self}}"/>

            <Image Source="Assets/14158.jpg" Width="100" Height="100" Margin="12" Tapped="img_Tapped"  
                   FlyoutBase.AttachedFlyout="{StaticResource ResourceFlyoutImage}"                                                 
                   DataContext="{Binding RelativeSource={RelativeSource Mode=Self}}"/>

            <Image Source="Assets/14160.jpg" Width="100" Height="100" Margin="12" Tapped="img_Tapped"    
                   FlyoutBase.AttachedFlyout="{StaticResource ResourceFlyoutImage}"                           
                   DataContext="{Binding RelativeSource={RelativeSource Mode=Self}}"/>

            <Image Source="Assets/14164.jpg" Width="100" Height="100" Margin="12" Tapped="img_Tapped"      
                   FlyoutBase.AttachedFlyout="{StaticResource ResourceFlyoutImage}"                                                  
                   DataContext="{Binding RelativeSource={RelativeSource Mode=Self}}"/>
        </StackPanel>
    </Grid>
```

```
private void img_Tapped(object sender, TappedRoutedEventArgs e)
{
    FlyoutBase.ShowAttachedFlyout((FrameworkElement)sender);
}             
```

同样的，在 WP 上也是可以得哦，一下是做了些修改后的 XAML 代码啦。正如大家所见，我把图片都缩小了， Placement 也设置成了 Top，StactPanel 的属性也做了修改。

```
    <Page.Resources>
        <Flyout x:Key="ResourceFlyoutImage" Placement="Top">
            <Image Source="{Binding Path=Source}" MaxHeight="600" MaxWidth="400" Stretch="Uniform"/>
            <Flyout.FlyoutPresenterStyle>
                <Style TargetType="FlyoutPresenter">
                    <Setter Property="MinHeight" Value="600"/>
                    <Setter Property="MinWidth"  Value="400"/>
                    <Setter Property="BorderThickness" Value="3"/>
                    <Setter Property="Background" Value="Wheat"/>
                    <Setter Property="BorderBrush" Value="Green"/>
                    <Setter Property="ScrollViewer.ZoomMode" Value="Enabled"/>
                </Style>
            </Flyout.FlyoutPresenterStyle>
        </Flyout>
    </Page.Resources>
    <Grid>
        <StackPanel VerticalAlignment="Bottom" Orientation="Horizontal">
            <Image Source="Assets/14152.jpg" Width="72" Height="60" Margin="12" Tapped="img_Tapped"  
                   FlyoutBase.AttachedFlyout="{StaticResource ResourceFlyoutImage}"                        
                   DataContext="{Binding RelativeSource={RelativeSource Mode=Self}}"/>

            <Image Source="Assets/14158.jpg" Width="72" Height="60" Margin="12" Tapped="img_Tapped"  
                   FlyoutBase.AttachedFlyout="{StaticResource ResourceFlyoutImage}"                                                 
                   DataContext="{Binding RelativeSource={RelativeSource Mode=Self}}"/>

            <Image Source="Assets/14160.jpg" Width="72" Height="60" Margin="12" Tapped="img_Tapped"    
                   FlyoutBase.AttachedFlyout="{StaticResource ResourceFlyoutImage}"                           
                   DataContext="{Binding RelativeSource={RelativeSource Mode=Self}}"/>

            <Image Source="Assets/14164.jpg" Width="72" Height="60" Margin="12" Tapped="img_Tapped"      
                   FlyoutBase.AttachedFlyout="{StaticResource ResourceFlyoutImage}"                                                  
                   DataContext="{Binding RelativeSource={RelativeSource Mode=Self}}"/>
        </StackPanel>
    </Grid>
```

看样子效果还不错嘛。

![](images/31.png)