---
layout: post
title:  "又自己造轮子：DZAnimatedGift"
date:   2018-03-22 19:21:00 +0900
---

之前的一个项目，有个直播中点按钮送心心（都tm是塞尔达翻译的错）的功能。
初版代码到我手上review的时候我也没仔细注意这边的功能，精力都放在了整体的逻辑和API的接口上。等到直播测试的时候才发现，他们那个心形礼物的抛出动画用的是一个Gif图片。如果用户猛点按钮的话，同时就会有好多个Gif图片，每个用一个View叠加在播放器的View上。自然，这个内存占用就突破天际。。。同屏20个左右就卡的不行。

一怒之下，我就自己造了个轮子给他们用。内存占用暴降，同屏上百个心心也不是问题。

这几天我把这个轮子提取出来，改了接口，做成了一个cocoapod库：

Git: [DZAnimatedGift][DZAnimatedGift_git]{:target="_blank"}

具体用法就参考git里的README就好。

[DZAnimatedGift_git]: https://github.com/darkzero/DZAnimatedGift