### 说明

本文记录对`ApplePS2SmartTouchPad.kext`一些配置项的修改

参考：[5966-details-about-the-smart-touchpad-driver-features](https://osxlatitude.com/forums/topic/5966-details-about-the-smart-touchpad-driver-features/)

#### 去除拖移锁定（延迟）
默认下，双击拖移后会有一个很长的延迟，在这个延迟内可以继续单指拖动窗口，这个设定实在是难以习惯。

**配置项**

`FLiftDragReleaseTimeOut`用来控制拖移释放后的延迟，设置为`0`即可。

#### 底部和右边区域触摸和滑动指针
默认配置下，底部和右边区域被设置为*边缘滚动*区域，允许使用单手指进行滚动操作，从而导致底部区域无法响应触摸和指针定位。

**配置项**

`EdgeScrolling`设置为`false`禁用边缘滚动后就可以直接释放底部和右边区域。

当然也可以单独配置，毕竟边缘滚动有时候还是挺好用的：

`EdgeHScrollArea`用来控制底边缘滚动区域

`EdgeVScrollArea`用来控制右边缘滚动区域

#### 触摸手势
因为手势操作实际上是通过触发按键绑定，所以可以直接在`系统设置-键盘-快捷键`中直接通过手势来设置快捷键（我最近才发现，是不是我太落后了= =）。

不过目前似乎只能识别三指和四指的上下左右手势，有空再研究一哈