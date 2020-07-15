# MulitSlider
wpf范围滑块
```xml
 <UserControl.Resources>
        <SolidColorBrush x:Key="LeftBackground" Color="#FF0096FF"/>
        <SolidColorBrush x:Key="RightBackground" Color="#2202B1E4"/>
        <SolidColorBrush x:Key="SpecialOriange" Color="#E08A09"/>
        <LinearGradientBrush x:Key="SliderBackground" StartPoint="0,0" EndPoint="0,1">
            <GradientStop Offset="0" Color="#FF02B1E4" />
            <GradientStop Offset="0.5" Color="#FF02B1E4" />
            <GradientStop Offset="1" Color="#FF02B1E4" />
        </LinearGradientBrush>
        <LinearGradientBrush x:Key="SliderThumb" StartPoint="0,0" EndPoint="0,1">
            <GradientStop Offset="0" Color="LightGray" />
        </LinearGradientBrush>
        <LinearGradientBrush x:Key="SliderText" StartPoint="0,0" EndPoint="0,1">
            <GradientStop Offset="0" Color="#7cce45" />
            <GradientStop Offset="1" Color="#4ea017" />
        </LinearGradientBrush>

        <!--  Slider模板  -->
        <Style x:Key="Slider_RepeatButton" TargetType="RepeatButton">
            <Setter Property="Focusable" Value="false" />
            <Setter Property="Template">
                <Setter.Value>
                    <ControlTemplate TargetType="RepeatButton">
                        <Grid Height="12">
                            <Border UseLayoutRounding="True"
                            Height="7"
                            Background="{StaticResource LeftBackground}"
                            CornerRadius="3 0 0 3" />
                        </Grid>

                    </ControlTemplate>
                </Setter.Value>
            </Setter>
        </Style>

        <Style x:Key="Slider_RepeatButton1" TargetType="RepeatButton">
            <Setter Property="Focusable" Value="false" />
            <Setter Property="Template">
                <Setter.Value>
                    <ControlTemplate TargetType="RepeatButton">
                        <Grid Height="12">
                            <Border UseLayoutRounding="True"
                                Height="7"
                                Background="{StaticResource RightBackground}"
                                CornerRadius="0 4 4 0"
                                />
                        </Grid>

                    </ControlTemplate>
                </Setter.Value>
            </Setter>
        </Style>

        <Style x:Key="Slider_Thumb" TargetType="Thumb">
            <Setter Property="Focusable" Value="false" />
            <Setter Property="Template">
                <Setter.Value>
                    <ControlTemplate TargetType="Thumb">
                        <Grid UseLayoutRounding="True" RenderTransformOrigin="0.5,1"
                              Width="50"
                              Margin="-25 -20 -25 0"
                              >
                            <Grid.RowDefinitions>
                                <RowDefinition Height="20"/>
                                <RowDefinition Height="*"/>
                            </Grid.RowDefinitions>
                            <Viewbox x:Name="Pin" Width="50" Grid.Row="0" Margin="0 0 0 5" RenderTransformOrigin="0.5,1">
                                <Border Background="Blue">
                                    <TextBlock Style="{x:Null}" Foreground="White" FontWeight="Normal">00:00:00</TextBlock>
                                    <!--Text="{Binding RelativeSource={RelativeSource FindAncestor, AncestorType=Slider}, Path=Value}"-->
                                </Border>
                                <Viewbox.RenderTransform>
                                    <TransformGroup>
                                        <ScaleTransform ScaleX="0" ScaleY="0" />
                                        <TranslateTransform Y="4" />
                                    </TransformGroup>
                                </Viewbox.RenderTransform>
                            </Viewbox>
                            <Grid Grid.Row="1" Width="12">
                                <Rectangle Height="7" Width="6" UseLayoutRounding="True"
                                       HorizontalAlignment="Left" 
                                       Fill="{StaticResource LeftBackground}"></Rectangle>
                                <Rectangle Height="7" Width="6" HorizontalAlignment="Right"
                                       UseLayoutRounding="True"
                                       Fill="{StaticResource RightBackground}"
                                       ></Rectangle>
                                <!--Background="{StaticResource SliderThumb}"-->
                                <Ellipse Height="24" 
                                     Margin="-12"
                                     Opacity="0"
                                     Width="24"
                                     x:Name="ThumbShadow"
                                     Fill="AliceBlue"
                                     >
                                </Ellipse>
                                <Ellipse Height="12"
                                     Width="12"
                                     Fill="AliceBlue">
                                </Ellipse>
                            </Grid>

                            <!--<TextBlock Text="||" HorizontalAlignment="Center" VerticalAlignment="Center"/>-->
                        </Grid>
                        <ControlTemplate.Triggers>
                            <Trigger Property="IsMouseOver" Value="true">
                                <Trigger.EnterActions>
                                    <BeginStoryboard>
                                        <Storyboard>
                                            <DoubleAnimation Storyboard.TargetName="ThumbShadow" Storyboard.TargetProperty="Opacity"
                                                  To="0.4" Duration="00:00:0.2"
                                                  >
                                            </DoubleAnimation>
                                        </Storyboard>
                                    </BeginStoryboard>
                                </Trigger.EnterActions>
                                <Trigger.ExitActions>
                                    <BeginStoryboard>
                                        <Storyboard>
                                            <DoubleAnimation  Storyboard.TargetName="ThumbShadow" Storyboard.TargetProperty="Opacity"
                                                  To="0.0" Duration="00:00:0.2"
                                                  >
                                            </DoubleAnimation>
                                        </Storyboard>
                                    </BeginStoryboard>
                                </Trigger.ExitActions>
                            </Trigger>
                            <Trigger Property="IsDragging" Value="true">
                                <Trigger.EnterActions>
                                    <BeginStoryboard>
                                        <Storyboard>
                                            <DoubleAnimationUsingKeyFrames Storyboard.TargetName="Pin" Storyboard.TargetProperty="(UIElement.RenderTransform).(TransformGroup.Children)[0].(ScaleTransform.ScaleX)">
                                                <EasingDoubleKeyFrame KeyTime="0:0:0" Value="0" />
                                                <EasingDoubleKeyFrame KeyTime="0:0:0.2" Value="1">
                                                    <EasingDoubleKeyFrame.EasingFunction>
                                                        <SineEase EasingMode="EaseInOut" />
                                                    </EasingDoubleKeyFrame.EasingFunction>
                                                </EasingDoubleKeyFrame>
                                            </DoubleAnimationUsingKeyFrames>
                                            <DoubleAnimationUsingKeyFrames Storyboard.TargetName="Pin" Storyboard.TargetProperty="(UIElement.RenderTransform).(TransformGroup.Children)[0].(ScaleTransform.ScaleY)">
                                                <EasingDoubleKeyFrame KeyTime="0:0:0" Value="0" />
                                                <EasingDoubleKeyFrame KeyTime="0:0:0.2" Value="1">
                                                    <EasingDoubleKeyFrame.EasingFunction>
                                                        <SineEase EasingMode="EaseInOut" />
                                                    </EasingDoubleKeyFrame.EasingFunction>
                                                </EasingDoubleKeyFrame>
                                            </DoubleAnimationUsingKeyFrames>
                                            <DoubleAnimationUsingKeyFrames Storyboard.TargetName="Pin" Storyboard.TargetProperty="(UIElement.RenderTransform).(TransformGroup.Children)[1].(TranslateTransform.Y)">
                                                <EasingDoubleKeyFrame KeyTime="0:0:0" Value="4" />
                                                <EasingDoubleKeyFrame KeyTime="0:0:0.2" Value="0">
                                                    <EasingDoubleKeyFrame.EasingFunction>
                                                        <SineEase EasingMode="EaseInOut" />
                                                    </EasingDoubleKeyFrame.EasingFunction>
                                                </EasingDoubleKeyFrame>
                                            </DoubleAnimationUsingKeyFrames>
                                        </Storyboard>
                                    </BeginStoryboard>
                                </Trigger.EnterActions>
                                <Trigger.ExitActions>
                                    <BeginStoryboard>
                                        <Storyboard>
                                            <DoubleAnimationUsingKeyFrames Storyboard.TargetName="Pin" Storyboard.TargetProperty="(UIElement.RenderTransform).(TransformGroup.Children)[0].(ScaleTransform.ScaleX)">
                                                <EasingDoubleKeyFrame KeyTime="0:0:0" Value="1" />
                                                <EasingDoubleKeyFrame KeyTime="0:0:0.2" Value="0">
                                                    <EasingDoubleKeyFrame.EasingFunction>
                                                        <SineEase EasingMode="EaseInOut" />
                                                    </EasingDoubleKeyFrame.EasingFunction>
                                                </EasingDoubleKeyFrame>
                                            </DoubleAnimationUsingKeyFrames>
                                            <DoubleAnimationUsingKeyFrames Storyboard.TargetName="Pin" Storyboard.TargetProperty="(UIElement.RenderTransform).(TransformGroup.Children)[0].(ScaleTransform.ScaleY)">
                                                <EasingDoubleKeyFrame KeyTime="0:0:0" Value="1" />
                                                <EasingDoubleKeyFrame KeyTime="0:0:0.2" Value="0">
                                                    <EasingDoubleKeyFrame.EasingFunction>
                                                        <SineEase EasingMode="EaseInOut" />
                                                    </EasingDoubleKeyFrame.EasingFunction>
                                                </EasingDoubleKeyFrame>
                                            </DoubleAnimationUsingKeyFrames>
                                            <DoubleAnimationUsingKeyFrames Storyboard.TargetName="Pin" Storyboard.TargetProperty="(UIElement.RenderTransform).(TransformGroup.Children)[1].(TranslateTransform.Y)">
                                                <EasingDoubleKeyFrame KeyTime="0:0:0" Value="0" />
                                                <EasingDoubleKeyFrame KeyTime="0:0:0.2" Value="4">
                                                    <EasingDoubleKeyFrame.EasingFunction>
                                                        <SineEase EasingMode="EaseInOut" />
                                                    </EasingDoubleKeyFrame.EasingFunction>
                                                </EasingDoubleKeyFrame>
                                            </DoubleAnimationUsingKeyFrames>
                                        </Storyboard>
                                    </BeginStoryboard>
                                </Trigger.ExitActions>
                            </Trigger>
                        </ControlTemplate.Triggers>
                    </ControlTemplate>
                </Setter.Value>
            </Setter>
        </Style>

        <Style x:Key="SliderLeft_Thumb" TargetType="Thumb">
            <Setter Property="Focusable" Value="false" />
            <Setter Property="Template">
                <Setter.Value>
                    <ControlTemplate TargetType="Thumb">
                        <Grid Background="#02ffffff">
                            <Viewbox
                                Width="5"
                                Height="16"
                                HorizontalAlignment="Left"
                                >
                                <Path
                                    Width="65.558"
                                    Height="200"
                                    Data="M75.000,54.000 L75.000,418.000 L153.000,418.000 L153.000,475.000 L2.000,475.000 L2.000,2.000 L153.000,2.000 L153.000,54.000 L75.000,54.000 Z"
                                    Fill="#E08A09"
                                    Stretch="Fill" />
                            </Viewbox>
                        </Grid>
                    </ControlTemplate>
                </Setter.Value>
            </Setter>
        </Style>

        <Style x:Key="SliderSide_Thumb" TargetType="Thumb">
            <Setter Property="Focusable" Value="false" />
            <Setter Property="Template">
                <Setter.Value>
                    <ControlTemplate TargetType="Thumb">
                        <Grid
                              Margin="-25 0 -25 0"
                              >
                            <Grid.RowDefinitions>
                                <RowDefinition Height="20"/>
                                <RowDefinition Height="auto"/>
                            </Grid.RowDefinitions>
                            <Viewbox Width="50" Margin="0 -20 0 0" x:Name="PinSide" RenderTransformOrigin="0.5,1">
                                <Border Width="50" Background="Blue">
                                    <TextBlock Foreground="White" Text="00:00:00"></TextBlock>
                                </Border>
                                <Viewbox.RenderTransform>
                                    <TransformGroup>
                                        <ScaleTransform ScaleX="0" ScaleY="0" />
                                        <TranslateTransform Y="4"/>
                                    </TransformGroup>
                                </Viewbox.RenderTransform>
                            </Viewbox>
                            <Grid Grid.Row="1">
                                <Viewbox 
                                Width="8"
                                HorizontalAlignment="Center">
                                    <Path RenderTransformOrigin="0.5,0.5"
                                      x:Name="SideThumbPath"
                                      Opacity="0.8"
                                    Data="m358.4,0l307.2,0a102.4,102.4 0 0 1 102.4,102.4l0,540.416a102.4,102.4 0 0 1 -14.592,52.672l-150.528,251.2a102.4,102.4 0 0 1 -174.848,1.408l-156.544,-252.16a102.4,102.4 0 0 1 -15.488,-54.016l0,-539.52a102.4,102.4 0 0 1 102.4,-102.4z"
                                    Fill="{StaticResource SpecialOriange}"
                                    Stretch="Fill">
                                        <Path.RenderTransform>
                                            <RotateTransform Angle="180"/>
                                        </Path.RenderTransform>
                                    </Path>
                                </Viewbox>
                            </Grid>

                        </Grid>
                        <ControlTemplate.Triggers>
                            <Trigger Property="IsMouseOver" Value="true">
                                <Trigger.EnterActions>
                                    <BeginStoryboard>
                                        <Storyboard>
                                            <DoubleAnimation Storyboard.TargetProperty="Opacity" Storyboard.TargetName="SideThumbPath" Duration="00:00:0.2" To="1"/>
                                        </Storyboard>
                                    </BeginStoryboard>
                                </Trigger.EnterActions>
                                <Trigger.ExitActions>
                                    <BeginStoryboard>
                                        <Storyboard>
                                            <DoubleAnimation Storyboard.TargetProperty="Opacity" Storyboard.TargetName="SideThumbPath" Duration="00:00:0.2" To="0.8"/>
                                        </Storyboard>
                                    </BeginStoryboard>
                                </Trigger.ExitActions>
                            </Trigger>
                            <Trigger Property="IsDragging" Value="true">
                                <Trigger.EnterActions>
                                    <BeginStoryboard>
                                        <Storyboard>
                                            <DoubleAnimationUsingKeyFrames Storyboard.TargetName="PinSide" Storyboard.TargetProperty="(UIElement.RenderTransform).(TransformGroup.Children)[0].(ScaleTransform.ScaleX)">
                                                <EasingDoubleKeyFrame KeyTime="0:0:0" Value="0" />
                                                <EasingDoubleKeyFrame KeyTime="0:0:0.2" Value="1">
                                                    <EasingDoubleKeyFrame.EasingFunction>
                                                        <SineEase EasingMode="EaseInOut" />
                                                    </EasingDoubleKeyFrame.EasingFunction>
                                                </EasingDoubleKeyFrame>
                                            </DoubleAnimationUsingKeyFrames>
                                            <DoubleAnimationUsingKeyFrames Storyboard.TargetName="PinSide" Storyboard.TargetProperty="(UIElement.RenderTransform).(TransformGroup.Children)[0].(ScaleTransform.ScaleY)">
                                                <EasingDoubleKeyFrame KeyTime="0:0:0" Value="0" />
                                                <EasingDoubleKeyFrame KeyTime="0:0:0.2" Value="1">
                                                    <EasingDoubleKeyFrame.EasingFunction>
                                                        <SineEase EasingMode="EaseInOut" />
                                                    </EasingDoubleKeyFrame.EasingFunction>
                                                </EasingDoubleKeyFrame>
                                            </DoubleAnimationUsingKeyFrames>
                                            <DoubleAnimationUsingKeyFrames Storyboard.TargetName="PinSide" Storyboard.TargetProperty="(UIElement.RenderTransform).(TransformGroup.Children)[1].(TranslateTransform.Y)">
                                                <EasingDoubleKeyFrame KeyTime="0:0:0" Value="4" />
                                                <EasingDoubleKeyFrame KeyTime="0:0:0.2" Value="0">
                                                    <EasingDoubleKeyFrame.EasingFunction>
                                                        <SineEase EasingMode="EaseInOut" />
                                                    </EasingDoubleKeyFrame.EasingFunction>
                                                </EasingDoubleKeyFrame>
                                            </DoubleAnimationUsingKeyFrames>
                                        </Storyboard>
                                    </BeginStoryboard>
                                </Trigger.EnterActions>
                                <Trigger.ExitActions>
                                    <BeginStoryboard>
                                        <Storyboard>
                                            <DoubleAnimationUsingKeyFrames Storyboard.TargetName="PinSide" Storyboard.TargetProperty="(UIElement.RenderTransform).(TransformGroup.Children)[0].(ScaleTransform.ScaleX)">
                                                <EasingDoubleKeyFrame KeyTime="0:0:0" Value="1" />
                                                <EasingDoubleKeyFrame KeyTime="0:0:0.2" Value="0">
                                                    <EasingDoubleKeyFrame.EasingFunction>
                                                        <SineEase EasingMode="EaseInOut" />
                                                    </EasingDoubleKeyFrame.EasingFunction>
                                                </EasingDoubleKeyFrame>
                                            </DoubleAnimationUsingKeyFrames>
                                            <DoubleAnimationUsingKeyFrames Storyboard.TargetName="PinSide" Storyboard.TargetProperty="(UIElement.RenderTransform).(TransformGroup.Children)[0].(ScaleTransform.ScaleY)">
                                                <EasingDoubleKeyFrame KeyTime="0:0:0" Value="1" />
                                                <EasingDoubleKeyFrame KeyTime="0:0:0.2" Value="0">
                                                    <EasingDoubleKeyFrame.EasingFunction>
                                                        <SineEase EasingMode="EaseInOut" />
                                                    </EasingDoubleKeyFrame.EasingFunction>
                                                </EasingDoubleKeyFrame>
                                            </DoubleAnimationUsingKeyFrames>
                                            <DoubleAnimationUsingKeyFrames Storyboard.TargetName="PinSide" Storyboard.TargetProperty="(UIElement.RenderTransform).(TransformGroup.Children)[1].(TranslateTransform.Y)">
                                                <EasingDoubleKeyFrame KeyTime="0:0:0" Value="0" />
                                                <EasingDoubleKeyFrame KeyTime="0:0:0.2" Value="4">
                                                    <EasingDoubleKeyFrame.EasingFunction>
                                                        <SineEase EasingMode="EaseInOut" />
                                                    </EasingDoubleKeyFrame.EasingFunction>
                                                </EasingDoubleKeyFrame>
                                            </DoubleAnimationUsingKeyFrames>
                                        </Storyboard>
                                    </BeginStoryboard>
                                </Trigger.ExitActions>
                            </Trigger>
                        </ControlTemplate.Triggers>
                    </ControlTemplate>
                </Setter.Value>
            </Setter>
        </Style>

        <Style x:Key="Slider_CustomStyle" TargetType="Slider">
            <Setter Property="Focusable" Value="false" />
            <Setter Property="Template">
                <Setter.Value>
                    <ControlTemplate TargetType="Slider">
                        <Grid VerticalAlignment="Center">
                            <Rectangle x:Name="PART_SelectionRange" Fill="{DynamicResource {x:Static SystemColors.HighlightBrushKey}}" Height="4" Visibility="Hidden"/>
                            <Track Name="PART_Track">
                                <Track.DecreaseRepeatButton>
                                    <RepeatButton Command="Slider.DecreaseLarge" VerticalAlignment="Bottom" Style="{StaticResource Slider_RepeatButton}" />
                                </Track.DecreaseRepeatButton>
                                <Track.IncreaseRepeatButton>
                                    <RepeatButton Command="Slider.IncreaseLarge" VerticalAlignment="Bottom" Style="{StaticResource Slider_RepeatButton1}" />
                                </Track.IncreaseRepeatButton>
                                <Track.Thumb>
                                    <Thumb VerticalAlignment="Bottom" Style="{StaticResource Slider_Thumb}" />
                                </Track.Thumb>
                            </Track>
                        </Grid>
                    </ControlTemplate>
                </Setter.Value>
            </Setter>
        </Style>

        <Style x:Key="SliderSide_CustomStyle" TargetType="Slider">
            <Setter Property="Focusable" Value="false" />
            <Setter Property="Template">
                <Setter.Value>
                    <ControlTemplate TargetType="Slider">
                        <Grid VerticalAlignment="Center">
                            <Rectangle x:Name="PART_SelectionRange" Fill="{DynamicResource {x:Static SystemColors.HighlightBrushKey}}" Height="4" Visibility="Hidden"/>

                            <Track Name="PART_Track">
                                <Track.Thumb>
                                    <Thumb VerticalAlignment="Bottom" Style="{StaticResource SliderSide_Thumb}" />
                                </Track.Thumb>
                            </Track>
                        </Grid>
                    </ControlTemplate>
                </Setter.Value>
            </Setter>
        </Style>
    </UserControl.Resources>
``` 
