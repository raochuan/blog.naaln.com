---
layout: post
title: 搞定了自己的手机谷歌地图
date: 2011/05/11 20:00:00
categories: 
- 随笔
tags: 
---

之前一直用google earth来制订线路，弊端是导出的KML文件如果导入到手机上的手机谷歌地图的话，就会有较大的误差。这个我在之前的帖子里面也提到了，应是谷歌软件自身的一些版本差异导致。不过今天研究谷歌地图的时候有所收获，尝试了一下，也算给出了一个解决办法。   首先访问ditu.google.com，这个地址是谷歌地图网页版的界面。 先注册一个谷歌账户，注册之后用账户登录谷歌地图才能绘制轨迹并保存到“我的地图”中。 用新注册的账户登录谷歌，就可以使用谷歌地图的进阶功能。 点击“我的地图”，准备创建轨迹。 

![][1] 点击“开始”之后，地图左上角就出现三个标识，点击第三个开始划线 

![][2] 因为一般的城市道路谷歌地图都会给出标记，而一些非机动车道或者人行道没有标记，所以我就用塘朗山的盘山路来做个例子。 画完轨迹之后，点击最后一个路径点，则轨迹生成，并弹出窗口进行标识。 

![][3] 输入轨迹名称，然后点击右边的小蓝框。 在里面确定好线形与颜色，就可以保存了。不过那个沿道路显示不用勾，如果打钩的话，像本次绘制的非机动车道轨迹就会被强制移动到最近的谷歌地图所记录的机动车道上去，很麻烦。 

![][4] 这时点击左边窗口完成就可以完成这张“我的地图”的保存。 如果要对这张地图命名，则点击修改就可以了。 

![][5] 接下来要做的事情就要在手机上执行了。 我的手机是HTC的touch3G，自带GPS芯片，同时支持A-GPS功能。所谓A-GPS就是移动运营商根据你的手机接入基站提供大致的范围信息给手机，手机在这个基础上搜星，获取方位的速度比单纯的GPS搜星快很多。 我的手机是windows mobile系统，装了对应的手机谷歌地图。目前塞班、安卓、WM均有对应版本的手机谷歌地图 

![][6] 进入软件之后，系统很快对当前位置进行定位。 

![][7] 因为我现在室内，所以定位偏差范围较大。室外的话控制在80米内问题不大。 首先登录你的谷歌账户 

![][8] 点击加入纵横，输入您的谷歌账户并登录 

![][9] 登录之后调整图层 

![][10] 将“卫星视图”与“纵横”均勾选，并点击“浏览图层”。 

![][11] 点击“我的地图”，稍等片刻就能打开你在网页上保存的地图界面。 

![][12] 点击刚才在网页上保存的标题，则系统开始载入地图。 

![][13] 

![][14] 放大看看 

![][15] 

![][16] 

![][17] 再发个网页的截图对比一下 

![][18] 

![][19] 基本吻合。 呵呵，我觉得以后做好轨迹以后，带上手机，就能放心地去山里探路啦！（记得带多一块电池哦） 最后补充一点，以上操作均需要在有手机信号的地方才能执行，因为谷歌手机地图需要从互联网下载卫星图跟路线信息。当然，完全没信号也不是不能用，如果你事先在手机上过了一遍路径的话，手机里面会有地图的缓存，只要打开kml文件的话，就能获取路径信息并显示出来，但不能确定你所在的位置。这种情况下，手机地图就仅能发挥一般纸质地图的功效了。 至于kml文件，你在谷歌地图网页上所制作的路径也是可以导出的。这里就要用到火狐浏览器，因为IE我尝试了一下不太好下载，火狐则非常方便。 在地图上方点击在google地球中查看 

![][20] 弹出窗口，将KML文件保存到本机，并拖到手机储存卡内即可。 

![][21] 此kml文件仅能提供谷歌地图网页与手机谷歌地图使用，如果导入到谷歌地球中，仍会有很大的漂移。 再补充一句，晚上装了个追星快手，才算是真正GPS定位了。在室外用追星获取坐标之后，再启动谷歌地图，并在设置中打开GPS定位，就能获取10m左右的定位精度。上文其实一直是在A-GPS的环境下进行，并未实现最高精度的A-GPS定位。这在山区某些单基站覆盖条件下可能带来较大误差。

[1]: https://ww2.sinaimg.cn/large/006tNc79gw1f50zaqbvxbj30b006cgm0

[2]: https://ww1.sinaimg.cn/large/006tNc79gw1f50zbchr28j30jx06dt9s

[3]: https://ww4.sinaimg.cn/large/006tNc79gw1f50zbo0w55j30ou0c8tcl

[4]: https://ww4.sinaimg.cn/large/006tNc79gw1f50zbw88x1j30by076gm6

[5]: https://ww3.sinaimg.cn/large/006tNc79gw1f50zc5csxpj30cr08674u

[6]: https://ww1.sinaimg.cn/large/006tNc79gw1f50zcbz909j306o08wjrx

[7]: https://ww2.sinaimg.cn/large/006tNc79gw1f50zcib2ojj306o08wdgu

[8]: https://ww3.sinaimg.cn/large/006tNc79gw1f50zcp4z90j306o08wgme

[9]: https://ww3.sinaimg.cn/large/006tNc79gw1f50zcvdlghj306o08wq3j

[10]: https://ww3.sinaimg.cn/large/006tNc79gw1f50zd4afskj306o08wq3t

[11]: https://ww2.sinaimg.cn/large/006tNc79gw1f50zdbjv4ij306o08w0tf

[12]: https://ww2.sinaimg.cn/large/006tNc79gw1f50zdjohgpj306o08wq3b

[13]: https://ww2.sinaimg.cn/large/006tNc79gw1f50zds8cdlj306o08w3yv

[14]: https://ww3.sinaimg.cn/large/006tNc79gw1f50zdydvavj306o08wmy6

[15]: https://ww2.sinaimg.cn/large/006tNc79gw1f50ze4lrc1j306o08w750

[16]: https://ww2.sinaimg.cn/large/006tNc79gw1f50zen49klj306o08wjs6

[17]: https://ww3.sinaimg.cn/large/006tNc79gw1f50zeycsgsj306o08w74w

[18]: https://ww3.sinaimg.cn/large/006tNc79gw1f50zf7semdj30hu0bs40w

[19]: https://ww2.sinaimg.cn/large/006tNc79gw1f50zffn7snj30fs0asq4u

[20]: https://ww4.sinaimg.cn/large/006tNc79gw1f50zfq1ol3j30hu0b1tbj

[21]: https://ww3.sinaimg.cn/large/006tNc79gw1f50zfx9eywj30fc0aigmz
