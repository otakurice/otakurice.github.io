---
title: hexo 添加网易云音乐歌单
date: 2018-07-20 22:21:01
tags:
- 命令合辑
categories:
- 前端
---
### 添加网易云音乐单曲
获取网易云音乐歌曲页面的外链方法
![](https://user-gold-cdn.xitu.io/2018/7/21/164ba88025ca3ca3?w=666&h=293&f=jpeg&s=46956)

![](https://user-gold-cdn.xitu.io/2018/7/21/164ba89fa5d3c72e?w=751&h=630&f=png&s=94132)
根据个人勾选选项，选择后将html代码复制，套上如下div即可。
```html
<div id="music163player">
    <iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=280 height=86 src="//music.163.com/outchain/player?type=2&id=28885472&auto=1&height=66">
    </iframe>
</div>
```
修改**主题文件夹**下layout\\_macro\sidebar.swig文件(这是侧边栏路径)，将上述代码贴入到想放的位置。

### 添加歌单
如果想要添加歌单，网易云的歌单页面也有生成外链的按钮。
![](https://user-gold-cdn.xitu.io/2018/7/21/164ba8597778a771?w=688&h=384&f=jpeg&s=55773)
```html
<div id="music163player">
  <iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=450 src="//music.163.com/outchain/player?type=0&id=2324520604&auto=1&height=430">
  </iframe>
</div>
```

<!-- 使用一个开源项目**Aplayer**
将下面代码贴到layout\\_macro\sidebar.swig文件中

```
<script src="https://cdn.bootcss.com/aplayer/1.6.0/APlayer.min.js"></script>
<script src="https://api.i-meto.com/music/player.js"></script>
```

在需要的位置添加播放器：

```
<div class="aplayer" data-id="2324520604" data-server="netease" data-type="playlist" data-mode="random" data-autoplay="false"></div>
```

设置参数如下：（粗体为必填项）

- **data-id**: 歌曲/专辑/歌单 ID
- **data-server**: 音乐平台，支持如下参数
  + netease （网易云音乐）
  + tencent （qq音乐）
  + xiami （虾米音乐）
  + kugou （酷狗音乐）
  + baidu （百度音乐）
- **data-type**: 请求类型，支持如下参数
  + song （单曲）
  + album （专辑）
  + playlist （歌单）
  + search （搜索）
- data-mode: 播放模式
  + random （随机）
  + single （单曲）
  + circulation （列表循环）
  + order （列表）
- data-autoplay: 自动播放
  + true
  + false -->
