[TOC]

#### UI 渲染

* CPU 负责图像数据计算，GPU 负责图像数据渲染，显示器则负责最终图像显示

  1. CPU 把计算好的、需要显示的内容交给 GPU

  2. GPU 完成渲染后放入帧缓冲区

  3. 视频控制器根据垂直同步信号（VSync）以每秒 60 次的速从帧缓冲区读取帧数据交由显示器完成图像显示
  4. Skia 是CPU向 GPU 提供视图数据的帮手

* 测量 》约束 》 布局 》 绘制 （布局边界）》合成渲染

#### Skia

* Skia 是跨平台的，因此它作为 Flutter iOS 渲染引擎被嵌入到 Flutter 的 iOS SDK 中，替代了 iOS 闭源Core Graphics/Core Animation/Core Text,  所以ios的包要大一些