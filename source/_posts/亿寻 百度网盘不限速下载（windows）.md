---
title: 亿寻 百度网盘不限速下载（windows）
tags: 
- windows
- 百度云
date: 2020-03-01 17:50:00
comments: true
---
作者：kud  
地址：https://www.52pojie.cn/thread-1065014-1-1.html

* 使用右键 下载/使用 saldl 下载

在使用右键 下载/使用 saldl 下载 请先设置以下参数值 BDUSS、version、devuid、rand 
及 time 。否则右键 下载/使用 saldl 下载 将不可选。


获取 BDUSS、version、devuid、rand 及 time 的值

##### 我的
```
NNNmRafjZwSHZnZWo4SFdUSEItMjlzY0JzeDhES0tXUXRmQ1lQWlhKLWxzYlplSVFBQUFBJCQAAAAAAAAAAAEAAAAdP986z6bR9M~CX1~Tx8nLAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAKUkj16lJI9eSE
```

所需工具: 数据包捕获工具。这里仅以 Fiddler 为例进行说明。


Fiddler
https://www.telerik.com/fiddler

下载（可能需要代理）
https://telerik-fiddler.s3.amazonaws.com/fiddler/FiddlerSetup.exe

安装
双击 FiddlerSetup.exe，单击 I Agree 按钮，单击 Install 进行安装。

设置
在开始屏幕或开始菜单中，单击 Fiddler 以打开 Fiddler 。单击菜单 
Tools/Options/HTTPS，选中 Decrypt HTTPS traffic，在打开的对话框中单击 Yes，在打
开的 安全警告 对话框中单击 是（Y），在打开的对话框中单击 是（Y），在打开的 
TrustCert uccess 对话框中单击 确定，最后单击 Option 对话框中的 OK 按钮。




打开 百度网盘客户端，并登录，单击 设置 图标，单击 设置/传输，将 代理设置 改为 
使用IE代理，最后单击 确定。

单击 百度网盘客户端 的刷新按钮，当 Fiddler 左侧出现黑色线程时，单击 Fiddler 菜单 
Edit/Find，在打开的 Find Sessions 对话框中的 Find 输入栏中，键入 &rand= ，单击 
Find Sessions 按钮。右键单击 Fiddler 左侧任意一个高亮的线程，选择 
Copy/Headers Only。将复制的结果粘贴到记事本，并查找 version、devuid、rand、time 
及 BDUSS 的值。

比如 version 的值为
version= 之后，且 & 之前的所有字符。
devuid、rand 和 time 的值以此类推。

BDUSS 的值为
BDUSS= 之后，且 ; (如果有) 之前所有字符。

将 百度网盘客户端 的 代理设置 恢复为默认值，即 不使用代理，并关闭 Fiddler。

打开 亿寻，单击 登录 按钮，在打开的 登录 对话框中单击 Cookie 按钮，将上面获取的 
BDUSS 值粘贴到 请输入 Cookie 输入栏，最后点击 登录 按钮进行登录。

登录成功后，单击菜单栏 工具/下载参数，将上面获取到的 version、devuid、rand 及 
time 值分别复制到对应的编辑栏中，单击 确定。

注意：下次登录时，请使用 切换账号 按钮进行登录，以避免重新设置。
注意：在更新到新版本时，可将 config 文件夹里的 SAM 和 Download.ini 文件复制到新
版本的 config 文件夹里，可避免重新设置以上参数。
注意：当使用 aria2 无法下载时，请尝试使用 saldl 下载。
注意：当下载目录有与将要下载的文件同名的文件时，saldl 不会继续下载。
注意: 当此方式下载速度非常慢或提示 速度受限 时，应立即停止使用此方式下载。当提示
速度受限 时，一般 24 小时后可以恢复正常。

下载时，如果出现验证码，尽管输便是，每个文件都对应一个验证码，这正常。
下一版解决验证码

深更半夜建议使用快捷下载，其他时段使用分享下载。

* 连接 raw.githubusercontent.com 出错

如果出现无法连接 raw.githubusercontent.com 错误时，检查更新将失败。

可定期手动进行检查。目前版本无视这个错误，作者下个版本将会修复。

使用前请仔细阅读 README 文件。











