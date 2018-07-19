### 说明

本文记录对`ApplePS2SmartTouchPad.kext`一些配置项的修改

参考：[5966-details-about-the-smart-touchpad-driver-features](https://osxlatitude.com/forums/topic/5966-details-about-the-smart-touchpad-driver-features/)

#### 去除拖移锁定（延迟）
默认下，双击拖移后会有一个很长的延迟，在这个延迟内可以继续单指拖动窗口，这个设定实在是难以习惯。

`FLiftDragReleaseTimeOut`用来控制拖移释放后的延迟，设置为`0`即可。

#### 底部和右边区域触摸和滑动指针
默认配置下，底部和右边区域被设置为*边缘滚动*区域，允许使用单手指进行滚动操作，从而导致底部区域无法响应触摸和指针定位。

`EdgeScrolling`设置为`false`禁用边缘滚动后就可以直接释放底部和右边区域。

当然也可以单独配置，毕竟边缘滚动有时候还是挺好用的：

`EdgeHScrollArea`用来控制底边缘滚动区域

`EdgeVScrollArea`用来控制右边缘滚动区域

#### 双指滚动优化

```
// 根据力度滚动，体验一般
<key>Auto2FingScroll</key>
<false/>

// 持续滚动
<key>Continuous2FingScroll</key>
<false/>

// 更高的值并不一定会更顺滑
<key>ScrollSmoothSamples</key>
<integer>4</integer>

// 应该跟滚动流畅度有关，原贴没此项信息
<key>InertialScrollDepth</key>
<integer>2</integer>

// 调节滚动速度，增加以提高
<key>ScrollLevelGranularity</key>
<integer>50</integer>

// 滚动停止检测，如果需要短距离快速滑动可以增加该项值
// 问题是会导致轻滑体验极差
<key>ScrollStopDetectSamples</key>
<integer>1</integer>
```

#### 触摸手势
因为手势操作实际上是通过触发按键绑定，所以可以直接在`系统设置-键盘-快捷键`中直接通过手势来设置快捷键（我最近才发现，是不是我太落后了= =）。

尝试着修改手势阈值，但并不能改善三指的误操作= =

不过目前似乎只能识别三指和四指的上下左右手势，有空再研究一哈