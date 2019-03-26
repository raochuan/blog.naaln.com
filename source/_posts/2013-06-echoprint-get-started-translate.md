---
layout: post
title: Echoprint Get started（翻译）
date: 2013/06/17 12:04:00
categories: 
- 技术
tags: 
- echoprint
- 翻译
---

欢迎来到EchoprintEchoprint 是一个开源的音乐是识别系统，他允许任何人在他们自己的应用上构建音乐指纹识别系统。感谢[The Echo Nest][1]的技术支持，以及[Musicbrainz][2]的合作。 

→ [Home / FAQ][3]

→ [Download from GitHub][4]

→ [How it works][5]

→ [Get started][6]

→ [Contact / Support][7]

→ [Data access][8]

→ [Server][9]

→ [Codegen][10]

→ [Twitter - @echonest][11]

![请输入图片描述][12] 

# 开始 

让我帮助你开始使用Echoprint！ 

*   我想要在我的电脑或者服务器上识别一首歌 

*   我想要在一个音乐库中删除重复的歌曲 

*   我想要在iOS 平台上识别一首歌曲 

*   我想要运行Echoprint来识别自己的数据 

如果你想要很好的使用Echoprint，加入Echoprint [Google](https://groups.google.com/forum/?fromgroups#!forum/echoprint) 小组是一个很好的方法。 

## 我想要在我的电脑或者服务器上识别一首歌 

很好！阅读 codegen [readme](https://github.com/whyliam/echoprint-codegen/blob/master/README.md)，你可以在GitHub中获取。在你自己的平台中安装（你必须把所有的文件编译，否着还有缺少文件的报告）。 

<script src="https://gist.github.com/1764256.js?file=gistfile1.txt"></script>

你可以通过刚才的代码进行Echo Nest的音乐识别。

## 我想要在一个音乐库中删除重复的歌曲 

第一步查阅 [server README][13] 。你需要作的是启动本地的服务器（不需要Solr或在Tokyo Tyrant ）或者启动整个堆栈，取决于你要去重复的数据的大小。第二步，用fp.ingest提取这个目录，接着用fp.query_fp() 对每个轨道进行查询。 

## 我想要在iOS 平台上识别一首歌曲 

最简单的方法是启动 [echoprint-ios-sample][14]，但是这离一个产品app有很大的距离——这只是一个演示。但是它包含关于如何计算从麦克风输入或文件在用户的iPod音乐库中，以及如何查询歌曲/识别服务的信息。 

## 我想要运行Echoprint来识别自己的数据 

查阅[server README][15] ，[fastingest][16] 阅读。获取[data][17]。

原文: [http://echoprint.me/][19] 

翻译: [Liam][20]

 [1]: http://the.echonest.com/

 [2]: http://musicbrainz.org/

 [3]: http://blog.naaln.com/2013/06/echoprint-home-faq-translations

 [4]: http://github.com/echonest/

 [5]: http://blog.naaln.com/2013/06/echoprint-how-it-works-translation

 [6]: http://blog.naaln.com/2013/06/echoprint-get-started-translate

 [7]: http://echoprint.me/contact

 [8]: http://blog.naaln.com/2013/06/echoprint-data-access-translation

 [9]: http://blog.naaln.com/2013/06/echoprint-server-translation

 [10]: http://blog.naaln.com/2013/06/echoprint-codegen-translation

 [11]: http://twitter.com/echonest

 [12]: https://ww1.sinaimg.cn/large/006tNc79gw1f5122w03sfj306y028748

 [13]: https://github.com/echonest/echoprint-server/blob/master/README.md

 [14]: https://github.com/echonest/echoprint-ios-sample

 [15]: https://github.com/echonest/echoprint-server/blob/master/README.md

 [16]: https://github.com/echonest/echoprint-server/blob/master/util/fastingest.py

 [17]: http://echoprint.me/data

 [19]: http://echoprint.me/start

 [20]: http://blog.naaln.com/2013/06/echoprint-get-started-translate
