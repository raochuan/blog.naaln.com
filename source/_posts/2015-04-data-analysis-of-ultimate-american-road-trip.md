---
layout: post
title: 数据分析美国公路的终极路线
date: 2015/04/25 19:07:37
categories: 
- 旅行
tags: 
---

这个帖子来自 Know More（Wonkblog的社交媒体网站）。

当你有一个算法的时候谁还需要地图呢？数据学家兰迪·奥尔森以前研究的[最佳搜索路径算法][1]曾在书籍《Where’s Waldo》中找到戴着眼镜的主人公，并且他还使用这种算法来计算最终美国公路路线。

在探索新闻主编特雷西的催促下，奥尔森开始寻找一条最快行驶路线，路线将经过所有48个州的国家自然地标，国家历史遗址，国家公园和国家纪念碑。同时还包括华盛顿特区，又在加利福尼亚州增加了一个地方，总共50目的地。这里是途径：

![imrs.png][2]

在50个目的地之间计算一条最快的行驶路线（有2500条独立的路径），理论上需要花费非常多的时间。但奥尔森使用了一种他在《Where's Waldo?》中[寻找主人公的遗传算法][3]。该算法最先计算少数的解决方案，选取最好的一个，然后比较其他解决方案，直到它不能找到一个更好的。下面算法是《Where's Waldo?》的示意图：

![DeadlyJampackedFishingcat.gif][4]

其结果是这个[路线图][5]，其中包括停止在大峡谷，阿拉莫，弗农山，雅园，白宫，自由女神像，等等。您可以在任何一个洲出发，并按任意一个方向的行驶。

在你不睡觉，不停车，交通不拥堵的情况下，奥尔森计算出这将需要驾驶大约9.33天。在实际情况中，你可能需要空闲的两到三个月来安排这个史诗级的美国公路之旅。

奥尔森还创建了一个[美国获奖城市的地图路线图][6]。这条路线经过美国48个州的 Trip Advisor 评选的“最佳参观城市” 和克利夫兰（为方便起见）。

> 原文 [A data genius computes the ultimate American road trip][7] -- By Ana Swanson

 [1]: http://www.randalolson.com/2015/02/03/heres-waldo-computing-the-optimal-search-strategy-for-finding-waldo/

 [2]: https://ww3.sinaimg.cn/large/006tNc79gw1f5106nb8nsj30dw07ngmu

 [3]: http://www.randalolson.com/2015/02/03/heres-waldo-computing-the-optimal-search-strategy-for-finding-waldo/

 [4]: https://ww2.sinaimg.cn/large/006tNc79gw1f51086elr4j30iy0cwmyq

 [5]: http://blog.naaln.com/2015/04/computing-optimal-road-across-US

 [6]: http://rhiever.github.io/optimal-roadtrip-usa/popular-cities.html

 [7]: http://www.washingtonpost.com/blogs/wonkblog/wp/2015/03/10/a-data-genius-computes-the-ultimate-american-road-trip/
