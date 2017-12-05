---
layout: post
title:  "编译了一个支持SSL的IJKMediaFrameworkWithSSL"
date:   2017-10-19 17:52:00 +0900
---

最近在做一个和视频流播放有关的项目，就想到了用IJKPlayer。

服务器端提供的m3u8文件的链接都是https，而用cocoapod引入的现成ijkplayer不支持SSL。没办法只好自己clone然后重新编译了一个支持SSL的framework。

想来今后也会有不少人遇到同样的问题，干脆就把编译完成的framework放到git上来。这周内大约会抽做成cocoapod库方便别人（自己）使用。

---

在[这里][IJKMediaFrameworkWithSSL_git]{:target="_blank"}
有编译+合并完成的**IJKMediaFrameworkWithSSL.framework**

#### 提醒：导入到自己的项目后需要把build选项里的bitcode设置为NO
---

### 支持SSL的IJKMediaFrameworkWithSSL编译方法

#### ijkplayer官方git

[https://github.com/Bilibili/ijkplayer][ijkplayer_git]{:target="_blank"}

初始步骤和Readme里写的没什么不同，先把整个代码库checkout到本地
```
git clone https://github.com/Bilibili/ijkplayer.git ijkplayer-ios
cd ijkplayer-ios
git checkout -B latest k0.8.4
```

之后的编译过程，因为需要SSL支持，所以在init-ios.sh之前，需要先初始化ssl

##### 1. 按照下面的流程执行shell

```
cd ijkplayer-ios
sh init-ios-openssl.sh
sh init-ios.sh

cd ios
./compile-openssl.sh clean
./compile-ffmpeg.sh clean
./compile-openssl.sh all
./compile-ffmpeg.sh all
```

##### 2. 如果都正常结束（无视那些warning），打开 ```ijkplayer-ios/ios/IJKMediaDemo/IJKMediaDemo.xcodeproj``` 

这项目里有三个target，*IJKMediaFramework*, *IJKMediaFrameworkWithSSL* 和 *IJKMediaDemo*，在需要支持https的情况下，选择**IJKMediaFrameworkWithSSL**进行编译

在Scheme里把编译环境调成release，分别编译出os版本和模拟器版本。

编译成功后，在
```
ijkplayer-ios/ios/IJKMediaDemo/DerivedData/IJKMediaDemo/Build/Products/
```
下会看到Release-iphoneos和Release-iphonesimulator两个文件夹，里面各有一个IJKMediaFrameworkWithSSL.framework文件。

##### 3. 合并framework

如果你不需要用到模拟器版的framework，直接把```Release-iphoneos```下的那个```IJKMediaFrameworkWithSSL.framework```导入到你的项目即可。

但是我们一般会需要在模拟器下调试，所以这里合并两个framework以便使用。

打开命令行工具，在

```
ijkplayer-ios/ios/IJKMediaDemo/DerivedData/IJKMediaDemo/Build/Products/
```

执行如下命令

```
lipo -create "Release-iphoneos/IJKMediaFrameworkWithSSL.framework/IJKMediaFrameworkWithSSL" "Release-iphonesimulator/IJKMediaFrameworkWithSSL.framework/IJKMediaFrameworkWithSSL" -output ./IJKMediaFrameworkWithSSL
```

你会看到在```Products```文件夹下多了一个*IJKMediaFrameworkWithSSL*文件

用这个文件替换掉```Release-iphoneos/IJKMediaFrameworkWithSSL.framework```里的*IJKMediaFrameworkWithSSL*

然后把这个被替换之后的```/IJKMediaFrameworkWithSSL.framework```导入到你的项目中即可

---

我在
[https://github.com/darkzero/IJKMediaFrameworkWithSSL][IJKMediaFrameworkWithSSL_git]
放了我自己编译+合并完成的**IJKMediaFrameworkWithSSL.framework**

懒得自己来的直接下载也行。

#### 提醒：导入到自己的项目后需要把build选项里的bitcode设置为NO

[ijkplayer_git]: https://github.com/Bilibili/ijkplayer
[IJKMediaFrameworkWithSSL_git]: https://github.com/darkzero/IJKMediaFrameworkWithSSL/
