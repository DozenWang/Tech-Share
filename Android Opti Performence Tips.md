###[Building a better Instagram app for Android](http://instagram-engineering.tumblr.com/post/97740520316/betterandroid)

这篇文章主要从两个方面来优化Instagram的性能：**产品设计** 和 **启动时间**。

####经验：
#####极简设计
 尽量使用纯色的设计取代渐变的图片资源。在屏幕上绘制纯色要比从磁盘上加载渐变的图片更节约内存资源，从而获得更快的性能。

#####改善启动时间
**Keypoint**:
- TraceView 发现耗时运行的代码
- Lazy-loading 延迟加载不需要启动时所需的资源
- 重写解析Json 的耗时代码
- Newsview，显示所有的喜好和评论，最初作为webview编写。它需要在启动时加载，以便尽可能快的显示用户数据。
问题是webview有自己的缓存系统，无法控制。
转换到Native实现，本地转换后的冷启动时间减少了30%。
