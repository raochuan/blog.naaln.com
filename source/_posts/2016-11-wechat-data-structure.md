---
title: iOS 微信的本地存储结构简析
date: 2016-11-24 09:30:24
categories: 
- 技术
tags: 
- 微信
---
大约四年前，我有了一个暗恋对象，所以想要把微信的聊天记录保存起来。那时在网上只有一种要付费的类似软件，所以我想，写一个开源的工具好了。于是这件事[很快就完成了](https://github.com/tiancaihb/SaWechat-iOS)（对应微信 6.0；那时的代码质量很低我知道）。

后来我没有了暗恋对象，也就不再关心这件事。最近，因为有不少人认为这样的功能仍然很有用，并且据我搜索到的情况，仍然没有能让每个人拿来直接用的工具。因为在几年之间文件结构发生了一些变化，我在这里记录下来，方便其他的开发者（对应现在的版本 6.3.25；虽然我没想到还能有什么用）。

### 怎么得到这些文件

过去，我可以提示用户在越狱之后用软件自行把微信 App 所在文件夹复制出来。然而自从某个版本的 iOS 开始，在不越狱的情况下，我们只能看到 `/User/Media` 这里的文件，而需要的本地数据在 `/User/Containers/Data/Application/` 微信的 UID。强迫用户为了这么一件事前去越狱显然不太友好，而对“聊天记录迁移”抓包也不方便，所以我想到另一种途径。

这就是 iTunes 备份。从经验判断，恢复备份之后微信里的聊天记录都还在，说明肯定这些文件在备份的时候保存到了电脑上。它们在哪里？[苹果官方给了答案](https://support.apple.com/zh-cn/HT204215)。简单地说，Windows 下在`\用户\（用户名）\AppData\Roaming\Apple Computer\MobileSync\Backup\`，然后我不喜欢用 Mac OS。

不过，iTunes 备份的文件夹结构不是很友好，似乎每个手机上的文件名都变成了一串序号，当然打开相关的 plist 然后看出规律也不难。好消息是，已经有很多人做了类似的事情，例如 [iphonebackupbrowser](https://code.google.com/archive/p/iphonebackupbrowser/)，它也是用 C# 写的，用起来比较方便。

因此，我做的第一步是让用户选取做好的 iTunes 备份，从上面那个源码，稍微修改一下就可以找到 com.tencent.xin 的相关文件，从而在程序里直接通过 iOS 上的路径找到对应的文件。

### 主要的数据库：MM.sqlite

从很久以前，iOS 微信的大部分数据就保存在这个 SQLite 3 数据库里。没有安卓上可恶的加密，直接可以打开。这个文件在 Documets/xxxx/DB/MM.sqlite，中间是对应用户名的 MD5，稍后会讲它的具体含义。不过一般只需要遍历所有的。

![](http://pics.naaln.com/blog/2019-01-14-032451.jpg)

我们感兴趣的是 Chat_ 开头的表，分别是和一个人（或群聊、公众号）的对话内容；以及记录朋友列表的 Friend 和 Friend_Ext。下面两图是朋友表的内容：

![](http://pics.naaln.com/blog/2019-01-14-032451.jpg)

![](http://pics.naaln.com/blog/2019-01-14-032452.jpg)

很明显，微信号是 UsrName，昵称是 NickName，备注名在 ConRemark。

此外在 ConStrRes2 里面（XML 格式）还有一些有用的信息。比如地区、签名、来源、LinkedIn……我们更需要的是头像的地址 HeadImgUrl，下面会用到。

![](http://pics.naaln.com/blog/2019-01-14-032454.jpg)

特别有个属性叫 alias 需要处理。我们知道每个用户最多可以修改一次微信号，那么新的微信号就会保存在 alias 当中。因为很多地方是用微信号作为 key 来索引到用户的（尽管每个用户也有一个数字的 ID），我们对两种微信号都要检查。

既然已经知道所有人的信息，下面就来看聊天记录。不过在这之前，我还遇到了一个意想不到的新问题。

### 消失的 Friend

程序写到一半，在某次备份之后，突然读不到朋友们的名字了。打开 MM.sqlite，发现 Friend 表当中确实几乎已经没有记录。那么微信究竟把这么多信息藏到哪里了？

我发现在同一个文件夹下面还有名叫 WCDB_Contact.sqlite 的文件。打开之后一目了然：

![](http://pics.naaln.com/blog/2019-01-14-032455.jpg)

猜想是因为随着中老年用户大量加入各种群聊，用户表的长度急速增长（聊天室里的陌生人可能也需要记录信息呀！），所以微信在最近的版本里选择了分表，而我刚好赶上了它转存数据的这个时间。

后面那些列都是 BLOB 格式的二进制，打开之后是这样的：

![](http://pics.naaln.com/blog/2019-01-14-032456.jpg)

以人类的视角，我们很容易看出所有内容的含义，只要多一些耐心，都可以直接找到需要的内容。问题在于，让程序怎么分割呢？

![](http://pics.naaln.com/blog/2019-01-14-032457.jpg)

我们来观察一下这位微信号为 suan*******cai 的朋友的信息。图片中选中了他的微信号字符串，那么微信如何知道这是需要的字符串呢？一种猜想是用分隔符，例如 C 字符串的 '\0' 结尾。但是，这字符串之后是 0x1a （或者其他很多可能性），无法与正常字符区分。另一种选择是在文件开始记录每一个变量的偏移量，但是观察其他文件发现开头部分非常短，最多 3 字节，不足以保存这样的内容。

自然只剩字符串的前一字节。0x0e，这刚好是选中字符串的长度。我们再往后看，例如有一个拼音首字母 XXK，刚好前一个字节是 0x03。后面的备注 INI-Mob，所以前一个字节是 0x07。于是这个疑问解决了。

再前面一个字节，例如第一行的 0x12，可以发现在同类每个文件的相应位置都不变。我猜想是下一个字符串的类型。

这样，这种记录的结构我们已经大致了解：

开头若干字节未知信息 --> (1 字节类型说明 --> 1(?) 字节长度 --> 字符串) 若干个

不过，在 dbContact 的上空还飘着两朵乌云：

(1) 文件开头究竟应该跳过几个字节，开始真正的内容？这好像在文件自身当中找不到线索，但在同一列当中是相同的，例如 dbContactRemark 是 0x0a，dbContactProfile 是 0x08 0x?? 0x12。问号表示可能有差别，但长度是确定的。所以相应地，可以人为让每种类型跳过若干个字节。至少我没有找到任何反例。

(2) 如果字符串长度超过一字节的表示范围，怎么办？一种合理的猜想是类似 UTF-8 或者 SQLite 的数值类型的表示法，也就是让某些高位为 1 来表示这个数字还要加上下一个字节。我暂时没有过多检验这个说法，因为唯一涉及这个问题的地方是 dbContactHeadImage 和 dbContactChatRoom。而这二者都有很明显的分隔位置，例如头像的链接总是以 http 开始，到 \/\d+ 为止。我在这里偷懒直接去匹配了。

### 聊天文字记录

有了前面的准备，我们已经可以解析 `Chat_[0-9a-f]{32}` 表，并且以文本形式导出每个对话的聊天记录。怎么知道聊天的对象是谁？Chat_ 后面是 UsrName 或 alias 的 MD5 值。

![](http://pics.naaln.com/blog/2019-01-14-032458.jpg)

首先看一下聊天记录的结构。MesLocalID 是一个比较重要的数字，虽然暂时还用不到。CreateTime 顾名思义，并且应该是 UTC+0 的。Message 就是消息本身。Type 表示消息的类型，可以自己试验一下，最后 Des 应该表示我是否为消息的接收方。

下面简单描述一下我见到过的 Type 和对应的 Message 处理：

10000: 系统消息，就是那种居中的。

34: 语音，消息里会有

47: 表情，

62: 小视频，<videomsg。

50: 视频 / 语音通话，<voipinvitemsg。本来在微信里二者就可以切换，对用户解释得太细也没啥用。

3: 图片。

48: 位置。

42: 名片。

49: 链接。这里面包含的类别比较多，在 Message 里面会有、、、 等信息。微信应该是通过 标签来确定一些特殊的应用，比如 2001 是红包，2000 转账，17 实时位置共享，6 文件。（我试过把它或者后面的模板地址改成别的，好像不管用。）

对于导出文字来说，这些特殊的东西就给用户显示个“[图片]”、“[表情]”吧。

还有一个问题是群聊，特点是用户名为 \d+@chatroom。在群聊当中，每个人（除了自己）的发言前面都会有“微信号:\n”，好让我们知道对方身份。问题在于，有些人在群聊当中可以改自己显示的名字。这个信息如果在新版数据库当中，包含在 dbContactChatRoom 列。它有 ... 的结构，处理起来应该不难。

### 其他多媒体资源

为了给用户初恋般的体验，我还希望能尽量还原聊天的全部内容，这就需要加入对应的图片（头像）、语音、视频、动画表情等元素。

我们自然会想在“Documents/ 微信号的 MD5”文件夹下面找这些内容。这时很容易发现：

(1) Img 文件夹中有一些以 MD5 命名的文件夹，它们对应数据库中的各 Chat_ 表，而具体文件是以数字编号的，这个编号等于对应消息的 MesLocalID（上面提到过）。文件有三种后缀：.pic、.pic_hd、.pic_thum，顾名思义是正常大小的图片、原图、缩略图。基本上是 JPEG 格式吧，这个影响不大。

(2) Video 文件夹类似，有 .video_thum 扩展名的缩略图，以及 .mp4 的视频本体。视频是 AVC+AAC 编码的，不过仍然不重要吧。

(3) Audio 是语音，以前是 3GP 格式，现在打开之后可以看到 SILK_V3 的字样，搜索可以直接发现[编译好的转换程序](https://github.com/kn007/silk-v3-decoder)。不过没有源码，也可以自行搜索其他解决方案。

然而在这个版本中，我始终没有从备份当中找到动画表情和头像这两项资源。怎么回事？

正好那段时间盘古越狱出现了，我把完整的 Documents 和 Library 文件夹复制出来，看了一遍。原来它们在 Library/WechatPrivate 里，而这个文件夹设置成了不备份。这也有道理，因为前面的几个是个人的资源，而头像和表情随时都可以再去下载，所以并不需要放在 iTunes 备份当中。

那么不越狱的情况下，我们怎么获得它们呢？记得上面提到过，在每个好友的 dbContactHeadImage 当中有正常和放大头像的地址；如果看一下含有动画表情的消息，其中也有这个表情的 GIF 地址。好的，下载就可以了。

最后，还有一件小事有点麻烦。

当前用户的微信号和头像在哪？

打开 mmsetting.archive，这是一个 plist 文件，在里面有几项是我的微信号、昵称、头像地址……

![](http://pics.naaln.com/blog/2019-01-14-032458.jpg)

问题在于这里没有很清楚的 key-value 形式，所以只能猜测出来一些找到相应内容的方法。如果能改进一下就更好了。

### 总结

以上描述了找到微信聊天记录涉及的文件的方法，不过讲道理它们都只能算是“有根据的推测”。因为聊天记录这件事不太方便收集测试数据，只能保证它们符合我能找到的记录。

我写了一个[新的微信聊天记录导出工具](https://github.com/tiancaihb/WechatExport-iOS)放在 GitHub 上，请有兴趣的读者尽情地 Fork 走修改之类的！

来源：[查看知乎原文](http://zhuanlan.zhihu.com/p/22474033)