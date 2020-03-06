# AHS-IPA

## 准备工作

- 应用程序 ipa 包
- 下载页面 html
- 两张 icon 图片（可选）
- manifest.plist
- 支持https的文件服务器

应用程序ipa包： 存储在服务器中，下载时需要
下载页面html：  内测用户访问下载应用包的入口
两张icon图片：   57x57和512x512，应用下载时，系统显示（可选）
manifest.plist：  其他命名亦可，是一份应用包的配置清单，其中包含了 ipa 包的下载地址
https的服务器： 主要是应为 manifest.plist 文件需要 https 支持；ipa包以及下载页面和icon图片存储在https或http下都可以

## 实现原理

**关键协议**：

```cpp
itms-services:///?action=download-manifest&url=你的 manifest.plist 文件地址
```

测试用户访问下载页面，当其触发 itms-services 协议，该协议指向了 manifest.plist 配置清单，该清单中包含了 ipa 的下载地址等信息，这样，系统即可触发安装事件。

## manifest.plist文件中名词解释

`software-package`：**应用 (.ipa) 文件的下载URL**

`display-image`：**57 x 57 像素的 PNG 图像，在下载和安装过程中显示。指定图像的完全限定 URL**

`full-size-image`：**512 x 512 像素的 PNG 图像，表示 iTunes 中相应的应用**

`bundle-identifier`：**应用的包标识符，与 Xcode 项目中指定的完全一样**

`bundle-version`：**应用的包版本，在 Xcode 项目中指定**

`title`：**下载和安装过程中显示的应用的名称**

