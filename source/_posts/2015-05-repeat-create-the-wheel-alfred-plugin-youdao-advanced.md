---
layout: post
title: 重复造轮子之Alfred有道插件  进阶篇
date: 2015/05/06 00:20:00
categories: 
- 技术
tags: 
- alfred
---

首先感谢 [deanishe][1] 为Alfred Workflow添加了 Python 框架库支持，自定义 Workflow 仅需要通过 Python 完成输入和输出的转换，最后输出到 Alfred 即可。这大大方便了我这种不会`PHP`开发的程序员

我想写的第一个自定义Alfred Workflow是有道翻译,它支持在Alfred中直接进行关键词翻译并直接展示翻译结果。

`Alfred Workflow`的教程确实十分的难写

> 会 coding 的不看教程就能写，不会 coding 的写了教程也还是一知半解

**我就简单的说一下这个流程吧**

我们先点击左下角新建一个`Blank Workflow`

![](https://ww1.sinaimg.cn/large/006tNc79gw1fahq559xxdj30ds08y0tc.jpg)

填入想要的信息如：

![](https://ww4.sinaimg.cn/large/006tNc79gw1fahq568gp9j30uc0my43k.jpg)

点击确认`save`后开始编写`Workflow`

我们先建立一个`script filter`

![](https://ww3.sinaimg.cn/large/006tNc79gw1fahq58jtaqj30g406sjs8.jpg)

然后填入一下的信息

![](https://ww1.sinaimg.cn/large/006tNc79gw1fahq5bvbatj312i0xkn5d.jpg)

然后我们进入文件所在的目录

![](https://ww1.sinaimg.cn/large/006tNc79gw1fahq5exr0hj30g40auabb.jpg)

首先下载[deanishe][2]提供的`alfred-workflow`python包，在新建一个`youdao.py`的文件。里面写上需要执行的代码：

```
  # -*- coding: utf-8 -*-
  
  import re
  import urllib
  from workflow import Workflow, ICON_WEB, web
  import sys
  reload(sys)
  sys.setdefaultencoding('utf8')

  #这是不完整的代码
  if __name__ == '__main__':
  wf = Workflow(update_settings={
     'github_slug': 'liszd/whyliam.workflows.youdao',
     'frequency': 7
  })

  sys.exit(wf.run(main))
  if wf.update_available:
     wf.start_update()
```

在[https://github.com/liszd/whyliam.workflows.youdao/blob/master/youdao.py][3]查看代码

然后新建`Copoy to Clipborad`

![](https://ww3.sinaimg.cn/large/006tNc79gw1fahq5gnw2jj30j60ahdhe.jpg)

用线连起来就是了。

当然这个只是*不完整的*简单的教程。

详细的源码请看 [https://github.com/liszd/whyliam.workflows.youdao][4]

 [1]: http://www.deanishe.net/alfred-workflow

 [2]: http://www.deanishe.net/alfred-workflow

 [3]: https://github.com/liszd/whyliam.workflows.youdao/blob/master/youdao.py

 [4]: https://github.com/liszd/whyliam.workflows.youdao
