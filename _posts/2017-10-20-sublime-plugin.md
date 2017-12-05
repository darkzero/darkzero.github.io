---
layout: post
title:  "常用的 Sublime Text 3 插件"
date:   2017-10-20 17:52:00 +0900
---
上次提到了Sublime Text 3，这次就来列一下我常用的Sublime Text 3插件好了。

### 准备

##### 安装 Package Control

为了使用插件先要安装 Package Control

参见：[官网的安装方法][package_control_3]{:target="_blank"}

- 方法一 使用Package Control组件安装: 

    用快捷方式 ``ctrl + (`)`` 或者在菜单里选择 `View > Show Console` 打开命令行窗口。

    然后在命令行里输入以下命令 : 

```
import urllib.request,os,hashlib; h = '6f4c264a24d933ce70df5dedcf1dcaee' + 'ebe013ee18cced0ef93d5f746d80ef60'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
```

- 方法二 直接安装

    参考官网右边的手动安装方法～

    下载安装包解压缩到Packages目录（菜单 > Preferences > Browse Packages）

    一般在下面这个目录

```
用户目录/Library/Application Support/Sublime Text 3/Packages
```

> 重启Sublime Text 3。如果在 Preferences > package settings 中看到 Package Control 这一项，则安装成功。按下Ctrl+Shift+P调出命令面板输入install 调出 Install Package 选项并回车，然后在列表中选中要安装的插件。

* 安装插件

    快捷键 Command+Shift+P 或者在 菜单里选择 Preferences > Package Control 打开 Package Control 窗口。

    选择 Install Package，然后在搜索框里输入你想要的插件名字就能看到插件列表，点击你想要安装的插件即可。

    有一部分插件安装后可能需要重启 Sublime。

### 我常用的插件

* **Sublime Terminal**

    Command + Shift + T 能在当前编辑文件的路径下打开Terminal窗口

* **OmniMarkupPreviewer**

    Markdown 预览用

    用 Command + Shift + O 打开浏览器窗口预览正在编辑的Markdown文件。

[package_control_3]: https://packagecontrol.io/installation#st3
