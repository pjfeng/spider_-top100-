

```python
实战_Requests库 + 正则表达式：抓取猫眼-top100电影
2019.03.13

第一步：获取 单页索引页


```


```python
import requests
from requests.exceptions import RequestException
import re

def get_one_page(url):
    try:
        response = requests.get(url)
        if response.status_code == 200:
            return response.text
        return None
    except RequestException:
        return None

def main():
    url = 'http://maoyan.com/board/4'
    html = get_one_page(url)
    print(html)

if __name__ == '__main__':
    main()
```

    <!DOCTYPE html>
    
    <!--[if IE 8]><html class="ie8"><![endif]-->
    <!--[if IE 9]><html class="ie9"><![endif]-->
    <!--[if gt IE 9]><!--><html><!--<![endif]-->
    <head>
      <title>TOP100榜 - 猫眼电影 - 一网打尽好电影</title>
      
      <link rel="dns-prefetch" href="//p0.meituan.net"  />
      <link rel="dns-prefetch" href="//p1.meituan.net"  />
      <link rel="dns-prefetch" href="//ms0.meituan.net" />
      <link rel="dns-prefetch" href="//ms1.meituan.net" />
      <link rel="dns-prefetch" href="//analytics.meituan.com" />
      <link rel="dns-prefetch" href="//report.meituan.com" />
      <link rel="dns-prefetch" href="//frep.meituan.com" />
    
      
      <meta charset="utf-8">
      <meta name="keywords" content="猫眼电影,电影排行榜,热映口碑榜,最受期待榜,国内票房榜,北美票房榜,猫眼TOP100">
      <meta name="description" content="猫眼电影热门榜单,包括热映口碑榜,最受期待榜,国内票房榜,北美票房榜,猫眼TOP100,多维度为用户进行选片决策">
      <meta http-equiv="cleartype" content="yes" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge" />
      <meta name="renderer" content="webkit" />
    
      <meta name="HandheldFriendly" content="true" />
      <meta name="format-detection" content="email=no" />
      <meta name="format-detection" content="telephone=no" />
      <meta name="viewport" content="width=device-width, initial-scale=1">
    
      
      <script>
      cid = "c_wx6zb55";
      ci = 30;
    val = {"subnavId":4};    window.system = {};
    
      window.openPlatform = '';
      window.openPlatformSub = '';
    
      </script>
      <link rel="stylesheet" href="//ms0.meituan.net/mywww/common.4b838ec3.css"/>
    <link rel="stylesheet" href="//ms0.meituan.net/mywww/board-index.92a06072.css"/>
      <script src="//ms0.meituan.net/mywww/stat.74891044.js"></script>
      <script>if(window.devicePixelRatio >= 2) { document.write('<link rel="stylesheet" href="//ms0.meituan.net/mywww/image-2x.8ba7074d.css"/>') }</script>
      <style>
        @font-face {
          font-family: stonefont;
          src: url('//vfile.meituan.net/colorstone/26eac9b995ede31b18f2d47b659de85f3168.eot');
          src: url('//vfile.meituan.net/colorstone/26eac9b995ede31b18f2d47b659de85f3168.eot?#iefix') format('embedded-opentype'),
               url('//vfile.meituan.net/colorstone/e784765b84fa80268e93357c8a4da79b2080.woff') format('woff');
        }
    
        .stonefont {
          font-family: stonefont;
        }
      </style>
    </head>
    <body>
    
    
    <div class="header">
      <div class="header-inner">
            <a href="/" class="logo" data-act="icon-click"></a>
            <div class="city-container" data-val="{currentcityid:30 }">
                <div class="city-selected">
                    <div class="city-name">
                      深圳
                      <span class="caret"></span>
                    </div>
                </div>
                <div class="city-list" data-val="{ localcityid: 30 }">
                    <div class="city-list-header">定位城市：<a class="js-geo-city">深圳</a></div>
                    
                </div>
            </div>
    
    
            <div class="nav">
                <ul class="navbar">
                    <li><a href="/" data-act="home-click"  >首页</a></li>
                    <li><a href="/films" data-act="movies-click" >电影</a></li>
                    <li><a href="/cinemas" data-act="cinemas-click" >影院</a></li> 
                    
                    <li><a href="/board" data-act="board-click"  class="active" >榜单</a></li>
                    <li><a href="/news" data-act="hotNews-click" >热点</a></li>
                </ul>
            </div>
    
            <div class="user-info">
                <div class="user-avatar J-login">
                  <img src="http://p0.meituan.net/movie/7dd82a16316ab32c8359debdb04396ef2897.png">
                  <span class="caret"></span>
                  <ul class="user-menu">
                    <li><a href="javascript:void 0">登录</a></li>
                  </ul>
                </div>
            </div>
    
            <form action="/query" target="_blank" class="search-form" data-actform="search-click">
                <input name="kw" class="search" type="search" maxlength="32" placeholder="找影视剧、影人、影院" autocomplete="off">
                <input class="submit" type="submit" value="">
            </form>
    
            <div class="app-download">
              <a href="/app" target="_blank">
                <span class="iphone-icon"></span>
                <span class="apptext">APP下载</span>
                <span class="caret"></span>
                <div class="download-icon">
                    <p class="down-title">扫码下载APP</p>
                    <p class='down-content'>选座更优惠</p>
                </div>
              </a>
            </div>
      </div>
    </div>
    <div class="header-placeholder"></div>
    
    <div class="subnav">
      <ul class="navbar">
        <li>
          <a data-act="subnav-click" data-val="{subnavClick:7}"
              href="/board/7"
          >热映口碑榜</a>
        </li>
        <li>
          <a data-act="subnav-click" data-val="{subnavClick:6}"
              href="/board/6"
          >最受期待榜</a>
        </li>
        <li>
          <a data-act="subnav-click" data-val="{subnavClick:1}"
              href="/board/1"
          >国内票房榜</a>
        </li>
        <li>
          <a data-act="subnav-click" data-val="{subnavClick:2}"
              href="/board/2"
          >北美票房榜</a>
        </li>
        <li>
          <a data-act="subnav-click" data-val="{subnavClick:4}"
              data-state-val="{subnavId:4}"
              class="active" href="javascript:void(0);"
          >TOP100榜</a>
        </li>
      </ul>
    </div>
    
    
        <div class="container" id="app" class="page-board/index" >
    
    <div class="content">
        <div class="wrapper">
            <div class="main">
                <p class="update-time">2018-08-08<span class="has-fresh-text">已更新</span></p>
                <p class="board-content">榜单规则：将猫眼电影库中的经典影片，按照评分和评分人数从高到低综合排序取前100名，每天上午10点更新。相关数据来源于“猫眼电影库”。</p>
                <dl class="board-wrapper">
                    <dd>
                            <i class="board-index board-index-1">1</i>
        <a href="/films/1203" title="霸王别姬" class="image-link" data-act="boarditem-click" data-val="{movieId:1203}">
          <img src="//ms0.meituan.net/mywww/image/loading_2.e3d934bf.png" alt="" class="poster-default" />
          <img data-src="http://p1.meituan.net/movie/20803f59291c47e1e116c11963ce019e68711.jpg@160w_220h_1e_1c" alt="霸王别姬" class="board-img" />
        </a>
        <div class="board-item-main">
          <div class="board-item-content">
                  <div class="movie-item-info">
            <p class="name"><a href="/films/1203" title="霸王别姬" data-act="boarditem-click" data-val="{movieId:1203}">霸王别姬</a></p>
            <p class="star">
                    主演：张国荣,张丰毅,巩俐
            </p>
    <p class="releasetime">上映时间：1993-01-01(中国香港)</p>    </div>
        <div class="movie-item-number score-num">
    <p class="score"><i class="integer">9.</i><i class="fraction">6</i></p>        
        </div>
    
          </div>
        </div>
    
                    </dd>
                    <dd>
                            <i class="board-index board-index-2">2</i>
        <a href="/films/1297" title="肖申克的救赎" class="image-link" data-act="boarditem-click" data-val="{movieId:1297}">
          <img src="//ms0.meituan.net/mywww/image/loading_2.e3d934bf.png" alt="" class="poster-default" />
          <img data-src="http://p0.meituan.net/movie/283292171619cdfd5b240c8fd093f1eb255670.jpg@160w_220h_1e_1c" alt="肖申克的救赎" class="board-img" />
        </a>
        <div class="board-item-main">
          <div class="board-item-content">
                  <div class="movie-item-info">
            <p class="name"><a href="/films/1297" title="肖申克的救赎" data-act="boarditem-click" data-val="{movieId:1297}">肖申克的救赎</a></p>
            <p class="star">
                    主演：蒂姆·罗宾斯,摩根·弗里曼,鲍勃·冈顿
            </p>
    <p class="releasetime">上映时间：1994-10-14(美国)</p>    </div>
        <div class="movie-item-number score-num">
    <p class="score"><i class="integer">9.</i><i class="fraction">5</i></p>        
        </div>
    
          </div>
        </div>
    
                    </dd>
                    <dd>
                            <i class="board-index board-index-3">3</i>
        <a href="/films/2641" title="罗马假日" class="image-link" data-act="boarditem-click" data-val="{movieId:2641}">
          <img src="//ms0.meituan.net/mywww/image/loading_2.e3d934bf.png" alt="" class="poster-default" />
          <img data-src="http://p0.meituan.net/movie/54617769d96807e4d81804284ffe2a27239007.jpg@160w_220h_1e_1c" alt="罗马假日" class="board-img" />
        </a>
        <div class="board-item-main">
          <div class="board-item-content">
                  <div class="movie-item-info">
            <p class="name"><a href="/films/2641" title="罗马假日" data-act="boarditem-click" data-val="{movieId:2641}">罗马假日</a></p>
            <p class="star">
                    主演：格利高里·派克,奥黛丽·赫本,埃迪·艾伯特
            </p>
    <p class="releasetime">上映时间：1953-09-02(美国)</p>    </div>
        <div class="movie-item-number score-num">
    <p class="score"><i class="integer">9.</i><i class="fraction">1</i></p>        
        </div>
    
          </div>
        </div>
    
                    </dd>
                    <dd>
                            <i class="board-index board-index-4">4</i>
        <a href="/films/4055" title="这个杀手不太冷" class="image-link" data-act="boarditem-click" data-val="{movieId:4055}">
          <img src="//ms0.meituan.net/mywww/image/loading_2.e3d934bf.png" alt="" class="poster-default" />
          <img data-src="http://p0.meituan.net/movie/e55ec5d18ccc83ba7db68caae54f165f95924.jpg@160w_220h_1e_1c" alt="这个杀手不太冷" class="board-img" />
        </a>
        <div class="board-item-main">
          <div class="board-item-content">
                  <div class="movie-item-info">
            <p class="name"><a href="/films/4055" title="这个杀手不太冷" data-act="boarditem-click" data-val="{movieId:4055}">这个杀手不太冷</a></p>
            <p class="star">
                    主演：让·雷诺,加里·奥德曼,娜塔莉·波特曼
            </p>
    <p class="releasetime">上映时间：1994-09-14(法国)</p>    </div>
        <div class="movie-item-number score-num">
    <p class="score"><i class="integer">9.</i><i class="fraction">5</i></p>        
        </div>
    
          </div>
        </div>
    
                    </dd>
                    <dd>
                            <i class="board-index board-index-5">5</i>
        <a href="/films/1247" title="教父" class="image-link" data-act="boarditem-click" data-val="{movieId:1247}">
          <img src="//ms0.meituan.net/mywww/image/loading_2.e3d934bf.png" alt="" class="poster-default" />
          <img data-src="http://p1.meituan.net/movie/f5a924f362f050881f2b8f82e852747c118515.jpg@160w_220h_1e_1c" alt="教父" class="board-img" />
        </a>
        <div class="board-item-main">
          <div class="board-item-content">
                  <div class="movie-item-info">
            <p class="name"><a href="/films/1247" title="教父" data-act="boarditem-click" data-val="{movieId:1247}">教父</a></p>
            <p class="star">
                    主演：马龙·白兰度,阿尔·帕西诺,詹姆斯·肯恩
            </p>
    <p class="releasetime">上映时间：1972-03-24(美国)</p>    </div>
        <div class="movie-item-number score-num">
    <p class="score"><i class="integer">9.</i><i class="fraction">3</i></p>        
        </div>
    
          </div>
        </div>
    
                    </dd>
                    <dd>
                            <i class="board-index board-index-6">6</i>
        <a href="/films/267" title="泰坦尼克号" class="image-link" data-act="boarditem-click" data-val="{movieId:267}">
          <img src="//ms0.meituan.net/mywww/image/loading_2.e3d934bf.png" alt="" class="poster-default" />
          <img data-src="http://p1.meituan.net/movie/0699ac97c82cf01638aa5023562d6134351277.jpg@160w_220h_1e_1c" alt="泰坦尼克号" class="board-img" />
        </a>
        <div class="board-item-main">
          <div class="board-item-content">
                  <div class="movie-item-info">
            <p class="name"><a href="/films/267" title="泰坦尼克号" data-act="boarditem-click" data-val="{movieId:267}">泰坦尼克号</a></p>
            <p class="star">
                    主演：莱昂纳多·迪卡普里奥,凯特·温丝莱特,比利·赞恩
            </p>
    <p class="releasetime">上映时间：1998-04-03</p>    </div>
        <div class="movie-item-number score-num">
    <p class="score"><i class="integer">9.</i><i class="fraction">5</i></p>        
        </div>
    
          </div>
        </div>
    
                    </dd>
                    <dd>
                            <i class="board-index board-index-7">7</i>
        <a href="/films/123" title="龙猫" class="image-link" data-act="boarditem-click" data-val="{movieId:123}">
          <img src="//ms0.meituan.net/mywww/image/loading_2.e3d934bf.png" alt="" class="poster-default" />
          <img data-src="http://p0.meituan.net/movie/b03e9c52c585635d2cb6a3f7c08a8a50112441.jpg@160w_220h_1e_1c" alt="龙猫" class="board-img" />
        </a>
        <div class="board-item-main">
          <div class="board-item-content">
                  <div class="movie-item-info">
            <p class="name"><a href="/films/123" title="龙猫" data-act="boarditem-click" data-val="{movieId:123}">龙猫</a></p>
            <p class="star">
                    主演：日高法子,坂本千夏,糸井重里
            </p>
    <p class="releasetime">上映时间：1988-04-16(日本)</p>    </div>
        <div class="movie-item-number score-num">
    <p class="score"><i class="integer">9.</i><i class="fraction">2</i></p>        
        </div>
    
          </div>
        </div>
    
                    </dd>
                    <dd>
                            <i class="board-index board-index-8">8</i>
        <a href="/films/837" title="唐伯虎点秋香" class="image-link" data-act="boarditem-click" data-val="{movieId:837}">
          <img src="//ms0.meituan.net/mywww/image/loading_2.e3d934bf.png" alt="" class="poster-default" />
          <img data-src="http://p0.meituan.net/movie/da64660f82b98cdc1b8a3804e69609e041108.jpg@160w_220h_1e_1c" alt="唐伯虎点秋香" class="board-img" />
        </a>
        <div class="board-item-main">
          <div class="board-item-content">
                  <div class="movie-item-info">
            <p class="name"><a href="/films/837" title="唐伯虎点秋香" data-act="boarditem-click" data-val="{movieId:837}">唐伯虎点秋香</a></p>
            <p class="star">
                    主演：周星驰,巩俐,郑佩佩
            </p>
    <p class="releasetime">上映时间：1993-07-01(中国香港)</p>    </div>
        <div class="movie-item-number score-num">
    <p class="score"><i class="integer">9.</i><i class="fraction">2</i></p>        
        </div>
    
          </div>
        </div>
    
                    </dd>
                    <dd>
                            <i class="board-index board-index-9">9</i>
        <a href="/films/1212" title="千与千寻" class="image-link" data-act="boarditem-click" data-val="{movieId:1212}">
          <img src="//ms0.meituan.net/mywww/image/loading_2.e3d934bf.png" alt="" class="poster-default" />
          <img data-src="http://p0.meituan.net/movie/b076ce63e9860ecf1ee9839badee5228329384.jpg@160w_220h_1e_1c" alt="千与千寻" class="board-img" />
        </a>
        <div class="board-item-main">
          <div class="board-item-content">
                  <div class="movie-item-info">
            <p class="name"><a href="/films/1212" title="千与千寻" data-act="boarditem-click" data-val="{movieId:1212}">千与千寻</a></p>
            <p class="star">
                    主演：柊瑠美,入野自由,夏木真理
            </p>
    <p class="releasetime">上映时间：2001-07-20(日本)</p>    </div>
        <div class="movie-item-number score-num">
    <p class="score"><i class="integer">9.</i><i class="fraction">3</i></p>        
        </div>
    
          </div>
        </div>
    
                    </dd>
                    <dd>
                            <i class="board-index board-index-10">10</i>
        <a href="/films/2760" title="魂断蓝桥" class="image-link" data-act="boarditem-click" data-val="{movieId:2760}">
          <img src="//ms0.meituan.net/mywww/image/loading_2.e3d934bf.png" alt="" class="poster-default" />
          <img data-src="http://p0.meituan.net/movie/46c29a8b8d8424bdda7715e6fd779c66235684.jpg@160w_220h_1e_1c" alt="魂断蓝桥" class="board-img" />
        </a>
        <div class="board-item-main">
          <div class="board-item-content">
                  <div class="movie-item-info">
            <p class="name"><a href="/films/2760" title="魂断蓝桥" data-act="boarditem-click" data-val="{movieId:2760}">魂断蓝桥</a></p>
            <p class="star">
                    主演：费雯·丽,罗伯特·泰勒,露塞尔·沃特森
            </p>
    <p class="releasetime">上映时间：1940-05-17(美国)</p>    </div>
        <div class="movie-item-number score-num">
    <p class="score"><i class="integer">9.</i><i class="fraction">2</i></p>        
        </div>
    
          </div>
        </div>
    
                    </dd>
                </dl>
    
            </div>
                <div class="pager-main">
                    
      
      <ul class="list-pager">
    
    
    
      
          <li class="active">
        <a class="page_1"
          href="javascript:void(0);" style="cursor: default"
      >1</a>
    
    </li>
      <li >
        <a class="page_2"
          href="?offset=10"
      >2</a>
    
    </li>
      <li >
        <a class="page_3"
          href="?offset=20"
      >3</a>
    
    </li>
      <li >
        <a class="page_4"
          href="?offset=30"
      >4</a>
    
    </li>
      <li >
        <a class="page_5"
          href="?offset=40"
      >5</a>
    
    </li>
    
        <li class="sep">...</li>
          <li >
        <a class="page_10"
          href="?offset=90"
      >10</a>
    
    </li>
    
      
    
    <li>  <a class="page_2"
          href="?offset=10"
      >下一页</a>
    </li>
    </ul>
    
    
                </div>
        </div>
    </div>
    
        </div>
    
    <div class="footer">
        <p class="friendly-links">
          商务合作邮箱：v@maoyan.com
          客服电话：10105335
          违法和不良信息举报电话：4006018900
          <br/>
          投诉举报邮箱：tousujubao@meituan.com
          舞弊线索举报邮箱：wubijubao@maoyan.com
        </p>
        <p class="friendly-links">
            友情链接 :
            <a href="http://www.meituan.com" data-query="utm_source=wwwmaoyan" target="_blank">美团网</a>
            <span></span>
            <a href="http://i.meituan.com/client" data-query="utm_source=wwwmaoyan" target="_blank">美团下载</a>
        </p>
        <p>
            &copy;2016
            猫眼电影 maoyan.com
            <a href="https://tsm.miit.gov.cn/pages/EnterpriseSearchList_Portal.aspx?type=0&keyword=京ICP证160733号&pageNo=1" target="_blank">京ICP证160733号</a>
            <a href="http://www.miibeian.gov.cn" target="_blank">京ICP备16022489号-1</a>
            <a href="http://www.beian.gov.cn/portal/registerSystemInfo?recordcode=11010102003232" target="_blank">京公网安备 11010102003232号</a>
            <a href="/about/licence" target="_blank">网络文化经营许可证</a>
            <a href="http://www.meituan.com/about/rules" target="_blank">电子公告服务规则</a>
        </p>
        <p>北京猫眼文化传媒有限公司</p>
    </div>
    
        <!--[if IE 8]><script src="//ms0.meituan.net/mywww/es5-shim.bbad933f.js"></script><![endif]-->
        <!--[if IE 8]><script src="//ms0.meituan.net/mywww/es5-sham.d6ea26f4.js"></script><![endif]-->
        <script src="//ms0.meituan.net/mywww/common.dc33ab40.js"></script>
    <script src="//ms0.meituan.net/mywww/board-index.4aa00764.js"></script>
    </body>
    </html>
    
    


```python


第二步，对网页进行解析，采用 def parse_one_page(url)

获取到元组信息

```


```python
import requests
from requests.exceptions import RequestException
import re

def get_one_page(url):
    try:
        response = requests.get(url)
        if response.status_code == 200:
            return response.text
        return None
    except RequestException:
        return None

# 第二步，插入的解析页,解析html代码

def parse_one_page(html):
    pattern = re.compile('<dd>.*?board-index.*?>(\d+)</i>.*?data-src="(.*?)".*?name"><a'
                         +'.*?>(.*?)</a>.*?star">(.*?)</p>.*?releasetime">(.*?)</p>'
                         +'.*?integer">(.*?)</i>.*?fraction">(.*?)</i>.*?</dd>', re.S)
    items = re.findall(pattern, html)
    print(items)
    
def main():
    url = 'http://maoyan.com/board/4'
    html = get_one_page(url)
    parse_one_page(html)

if __name__ == '__main__':
    main()
```

    [('1', 'http://p1.meituan.net/movie/20803f59291c47e1e116c11963ce019e68711.jpg@160w_220h_1e_1c', '霸王别姬', '\n                主演：张国荣,张丰毅,巩俐\n        ', '上映时间：1993-01-01(中国香港)', '9.', '6'), ('2', 'http://p0.meituan.net/movie/283292171619cdfd5b240c8fd093f1eb255670.jpg@160w_220h_1e_1c', '肖申克的救赎', '\n                主演：蒂姆·罗宾斯,摩根·弗里曼,鲍勃·冈顿\n        ', '上映时间：1994-10-14(美国)', '9.', '5'), ('3', 'http://p0.meituan.net/movie/54617769d96807e4d81804284ffe2a27239007.jpg@160w_220h_1e_1c', '罗马假日', '\n                主演：格利高里·派克,奥黛丽·赫本,埃迪·艾伯特\n        ', '上映时间：1953-09-02(美国)', '9.', '1'), ('4', 'http://p0.meituan.net/movie/e55ec5d18ccc83ba7db68caae54f165f95924.jpg@160w_220h_1e_1c', '这个杀手不太冷', '\n                主演：让·雷诺,加里·奥德曼,娜塔莉·波特曼\n        ', '上映时间：1994-09-14(法国)', '9.', '5'), ('5', 'http://p1.meituan.net/movie/f5a924f362f050881f2b8f82e852747c118515.jpg@160w_220h_1e_1c', '教父', '\n                主演：马龙·白兰度,阿尔·帕西诺,詹姆斯·肯恩\n        ', '上映时间：1972-03-24(美国)', '9.', '3'), ('6', 'http://p1.meituan.net/movie/0699ac97c82cf01638aa5023562d6134351277.jpg@160w_220h_1e_1c', '泰坦尼克号', '\n                主演：莱昂纳多·迪卡普里奥,凯特·温丝莱特,比利·赞恩\n        ', '上映时间：1998-04-03', '9.', '5'), ('7', 'http://p0.meituan.net/movie/b03e9c52c585635d2cb6a3f7c08a8a50112441.jpg@160w_220h_1e_1c', '龙猫', '\n                主演：日高法子,坂本千夏,糸井重里\n        ', '上映时间：1988-04-16(日本)', '9.', '2'), ('8', 'http://p0.meituan.net/movie/da64660f82b98cdc1b8a3804e69609e041108.jpg@160w_220h_1e_1c', '唐伯虎点秋香', '\n                主演：周星驰,巩俐,郑佩佩\n        ', '上映时间：1993-07-01(中国香港)', '9.', '2'), ('9', 'http://p0.meituan.net/movie/b076ce63e9860ecf1ee9839badee5228329384.jpg@160w_220h_1e_1c', '千与千寻', '\n                主演：柊瑠美,入野自由,夏木真理\n        ', '上映时间：2001-07-20(日本)', '9.', '3'), ('10', 'http://p0.meituan.net/movie/46c29a8b8d8424bdda7715e6fd779c66235684.jpg@160w_220h_1e_1c', '魂断蓝桥', '\n                主演：费雯·丽,罗伯特·泰勒,露塞尔·沃特森\n        ', '上映时间：1940-05-17(美国)', '9.', '2')]
    


```python



第三步，针对以上杂乱的信息进行格式化 提取 

效果：提取 10个 键值对 形式


```


```python
import requests
from requests.exceptions import RequestException
import re

def get_one_page(url):
    try:
        response = requests.get(url)
        if response.status_code == 200:
            return response.text
        return None
    except RequestException:
        return None

# 第二步，插入的解析页,解析html代码

def parse_one_page(html):
    pattern = re.compile('<dd>.*?board-index.*?>(\d+)</i>.*?data-src="(.*?)".*?name"><a'
                         +'.*?>(.*?)</a>.*?star">(.*?)</p>.*?releasetime">(.*?)</p>'
                         +'.*?integer">(.*?)</i>.*?fraction">(.*?)</i>.*?</dd>', re.S)
    items = re.findall(pattern, html)

#第三步，将其变成字典的形式
    for item in items:
        yield {
            'index':item[0],
            'image':item[1],
            'title':item[2],
            'actor':item[3].strip()[3:], # 使用切片-strip功能，去掉 主演：这三个字符
            'time':item[4].strip()[5:],
            'score':item[5]+item[6]
        }

    
def main():
    url = 'http://maoyan.com/board/4'
    html = get_one_page(url)
    for item in parse_one_page(html): # 第三步，提取生成器，打印效果
        print(item)

if __name__ == '__main__':
    main()
```

    {'index': '1', 'image': 'http://p1.meituan.net/movie/20803f59291c47e1e116c11963ce019e68711.jpg@160w_220h_1e_1c', 'title': '霸王别姬', 'actor': '张国荣,张丰毅,巩俐', 'time': '1993-01-01(中国香港)', 'score': '9.6'}
    {'index': '2', 'image': 'http://p0.meituan.net/movie/283292171619cdfd5b240c8fd093f1eb255670.jpg@160w_220h_1e_1c', 'title': '肖申克的救赎', 'actor': '蒂姆·罗宾斯,摩根·弗里曼,鲍勃·冈顿', 'time': '1994-10-14(美国)', 'score': '9.5'}
    {'index': '3', 'image': 'http://p0.meituan.net/movie/54617769d96807e4d81804284ffe2a27239007.jpg@160w_220h_1e_1c', 'title': '罗马假日', 'actor': '格利高里·派克,奥黛丽·赫本,埃迪·艾伯特', 'time': '1953-09-02(美国)', 'score': '9.1'}
    {'index': '4', 'image': 'http://p0.meituan.net/movie/e55ec5d18ccc83ba7db68caae54f165f95924.jpg@160w_220h_1e_1c', 'title': '这个杀手不太冷', 'actor': '让·雷诺,加里·奥德曼,娜塔莉·波特曼', 'time': '1994-09-14(法国)', 'score': '9.5'}
    {'index': '5', 'image': 'http://p1.meituan.net/movie/f5a924f362f050881f2b8f82e852747c118515.jpg@160w_220h_1e_1c', 'title': '教父', 'actor': '马龙·白兰度,阿尔·帕西诺,詹姆斯·肯恩', 'time': '1972-03-24(美国)', 'score': '9.3'}
    {'index': '6', 'image': 'http://p1.meituan.net/movie/0699ac97c82cf01638aa5023562d6134351277.jpg@160w_220h_1e_1c', 'title': '泰坦尼克号', 'actor': '莱昂纳多·迪卡普里奥,凯特·温丝莱特,比利·赞恩', 'time': '1998-04-03', 'score': '9.5'}
    {'index': '7', 'image': 'http://p0.meituan.net/movie/b03e9c52c585635d2cb6a3f7c08a8a50112441.jpg@160w_220h_1e_1c', 'title': '龙猫', 'actor': '日高法子,坂本千夏,糸井重里', 'time': '1988-04-16(日本)', 'score': '9.2'}
    {'index': '8', 'image': 'http://p0.meituan.net/movie/da64660f82b98cdc1b8a3804e69609e041108.jpg@160w_220h_1e_1c', 'title': '唐伯虎点秋香', 'actor': '周星驰,巩俐,郑佩佩', 'time': '1993-07-01(中国香港)', 'score': '9.2'}
    {'index': '9', 'image': 'http://p0.meituan.net/movie/b076ce63e9860ecf1ee9839badee5228329384.jpg@160w_220h_1e_1c', 'title': '千与千寻', 'actor': '柊瑠美,入野自由,夏木真理', 'time': '2001-07-20(日本)', 'score': '9.3'}
    {'index': '10', 'image': 'http://p0.meituan.net/movie/46c29a8b8d8424bdda7715e6fd779c66235684.jpg@160w_220h_1e_1c', 'title': '魂断蓝桥', 'actor': '费雯·丽,罗伯特·泰勒,露塞尔·沃特森', 'time': '1940-05-17(美国)', 'score': '9.2'}
    


```python


第四步：将其存储到文件中
    def write_to_file(content):

```


```python
import requests
from requests.exceptions import RequestException
import re
import json

def get_one_page(url):
    try:
        response = requests.get(url)
        if response.status_code == 200:
            return response.text
        return None
    except RequestException:
        return None

# 第二步，插入的解析页,解析html代码

def parse_one_page(html):
    pattern = re.compile('<dd>.*?board-index.*?>(\d+)</i>.*?data-src="(.*?)".*?name"><a'
                         +'.*?>(.*?)</a>.*?star">(.*?)</p>.*?releasetime">(.*?)</p>'
                         +'.*?integer">(.*?)</i>.*?fraction">(.*?)</i>.*?</dd>', re.S)
    items = re.findall(pattern, html)

#第三步，将其变成字典的形式
    for item in items:
        yield {
            'index':item[0],
            'image':item[1],
            'title':item[2],
            'actor':item[3].strip()[3:], # 使用切片-strip功能，去掉 主演：这三个字符
            'time':item[4].strip()[5:],
            'score':item[5]+item[6]
        }

def write_to_file(content): # 第四步，存储到文件
    with open('result.txt','a') as f:
        f.write(json.dumps(content) + '\n') # 使用json.dump，把其字典形式 转为 字符串，再添加个换行
        f.close()
    
def main():
    url = 'http://maoyan.com/board/4'
    html = get_one_page(url)
    for item in parse_one_page(html): # 第三步，提取生成器，打印效果
        print(item)
        write_to_file(item) # 第四步，将其传入到文件

if __name__ == '__main__':
    main()
```

    {'index': '1', 'image': 'http://p1.meituan.net/movie/20803f59291c47e1e116c11963ce019e68711.jpg@160w_220h_1e_1c', 'title': '霸王别姬', 'actor': '张国荣,张丰毅,巩俐', 'time': '1993-01-01(中国香港)', 'score': '9.6'}
    {'index': '2', 'image': 'http://p0.meituan.net/movie/283292171619cdfd5b240c8fd093f1eb255670.jpg@160w_220h_1e_1c', 'title': '肖申克的救赎', 'actor': '蒂姆·罗宾斯,摩根·弗里曼,鲍勃·冈顿', 'time': '1994-10-14(美国)', 'score': '9.5'}
    {'index': '3', 'image': 'http://p0.meituan.net/movie/54617769d96807e4d81804284ffe2a27239007.jpg@160w_220h_1e_1c', 'title': '罗马假日', 'actor': '格利高里·派克,奥黛丽·赫本,埃迪·艾伯特', 'time': '1953-09-02(美国)', 'score': '9.1'}
    {'index': '4', 'image': 'http://p0.meituan.net/movie/e55ec5d18ccc83ba7db68caae54f165f95924.jpg@160w_220h_1e_1c', 'title': '这个杀手不太冷', 'actor': '让·雷诺,加里·奥德曼,娜塔莉·波特曼', 'time': '1994-09-14(法国)', 'score': '9.5'}
    {'index': '5', 'image': 'http://p1.meituan.net/movie/f5a924f362f050881f2b8f82e852747c118515.jpg@160w_220h_1e_1c', 'title': '教父', 'actor': '马龙·白兰度,阿尔·帕西诺,詹姆斯·肯恩', 'time': '1972-03-24(美国)', 'score': '9.3'}
    {'index': '6', 'image': 'http://p1.meituan.net/movie/0699ac97c82cf01638aa5023562d6134351277.jpg@160w_220h_1e_1c', 'title': '泰坦尼克号', 'actor': '莱昂纳多·迪卡普里奥,凯特·温丝莱特,比利·赞恩', 'time': '1998-04-03', 'score': '9.5'}
    {'index': '7', 'image': 'http://p0.meituan.net/movie/b03e9c52c585635d2cb6a3f7c08a8a50112441.jpg@160w_220h_1e_1c', 'title': '龙猫', 'actor': '日高法子,坂本千夏,糸井重里', 'time': '1988-04-16(日本)', 'score': '9.2'}
    {'index': '8', 'image': 'http://p0.meituan.net/movie/da64660f82b98cdc1b8a3804e69609e041108.jpg@160w_220h_1e_1c', 'title': '唐伯虎点秋香', 'actor': '周星驰,巩俐,郑佩佩', 'time': '1993-07-01(中国香港)', 'score': '9.2'}
    {'index': '9', 'image': 'http://p0.meituan.net/movie/b076ce63e9860ecf1ee9839badee5228329384.jpg@160w_220h_1e_1c', 'title': '千与千寻', 'actor': '柊瑠美,入野自由,夏木真理', 'time': '2001-07-20(日本)', 'score': '9.3'}
    {'index': '10', 'image': 'http://p0.meituan.net/movie/46c29a8b8d8424bdda7715e6fd779c66235684.jpg@160w_220h_1e_1c', 'title': '魂断蓝桥', 'actor': '费雯·丽,罗伯特·泰勒,露塞尔·沃特森', 'time': '1940-05-17(美国)', 'score': '9.2'}
    


```python

第四步：维修，将 result.txt中 unix编码转为 中文形式
            在 write_to_file 中，加入 encoding='utf-8'  和 ‘ensure_ascii=False’
    
```


```python
import requests
from requests.exceptions import RequestException
import re
import json

def get_one_page(url):
    try:
        response = requests.get(url)
        if response.status_code == 200:
            return response.text
        return None
    except RequestException:
        return None

# 第二步，插入的解析页,解析html代码

def parse_one_page(html):
    pattern = re.compile('<dd>.*?board-index.*?>(\d+)</i>.*?data-src="(.*?)".*?name"><a'
                         +'.*?>(.*?)</a>.*?star">(.*?)</p>.*?releasetime">(.*?)</p>'
                         +'.*?integer">(.*?)</i>.*?fraction">(.*?)</i>.*?</dd>', re.S)
    items = re.findall(pattern, html)

#第三步，将其变成字典的形式
    for item in items:
        yield {
            'index':item[0],
            'image':item[1],
            'title':item[2],
            'actor':item[3].strip()[3:], # 使用切片-strip功能，去掉 主演：这三个字符
            'time':item[4].strip()[5:],
            'score':item[5]+item[6]
        }

def write_to_file(content): # 第四步，存储到文件
    with open('result.txt','a',encoding='utf-8') as f:
        f.write(json.dumps(content, ensure_ascii=False) + '\n') # 使用json.dump，把其字典形式 转为 字符串，再添加个换行
        f.close()
    
def main():
    url = 'http://maoyan.com/board/4'
    html = get_one_page(url)
    for item in parse_one_page(html): # 第三步，提取生成器，打印效果
        print(item)
        write_to_file(item) # 第四步，将其传入到文件

if __name__ == '__main__':
    main()
```

    {'index': '1', 'image': 'http://p1.meituan.net/movie/20803f59291c47e1e116c11963ce019e68711.jpg@160w_220h_1e_1c', 'title': '霸王别姬', 'actor': '张国荣,张丰毅,巩俐', 'time': '1993-01-01(中国香港)', 'score': '9.6'}
    {'index': '2', 'image': 'http://p0.meituan.net/movie/283292171619cdfd5b240c8fd093f1eb255670.jpg@160w_220h_1e_1c', 'title': '肖申克的救赎', 'actor': '蒂姆·罗宾斯,摩根·弗里曼,鲍勃·冈顿', 'time': '1994-10-14(美国)', 'score': '9.5'}
    {'index': '3', 'image': 'http://p0.meituan.net/movie/54617769d96807e4d81804284ffe2a27239007.jpg@160w_220h_1e_1c', 'title': '罗马假日', 'actor': '格利高里·派克,奥黛丽·赫本,埃迪·艾伯特', 'time': '1953-09-02(美国)', 'score': '9.1'}
    {'index': '4', 'image': 'http://p0.meituan.net/movie/e55ec5d18ccc83ba7db68caae54f165f95924.jpg@160w_220h_1e_1c', 'title': '这个杀手不太冷', 'actor': '让·雷诺,加里·奥德曼,娜塔莉·波特曼', 'time': '1994-09-14(法国)', 'score': '9.5'}
    {'index': '5', 'image': 'http://p1.meituan.net/movie/f5a924f362f050881f2b8f82e852747c118515.jpg@160w_220h_1e_1c', 'title': '教父', 'actor': '马龙·白兰度,阿尔·帕西诺,詹姆斯·肯恩', 'time': '1972-03-24(美国)', 'score': '9.3'}
    {'index': '6', 'image': 'http://p1.meituan.net/movie/0699ac97c82cf01638aa5023562d6134351277.jpg@160w_220h_1e_1c', 'title': '泰坦尼克号', 'actor': '莱昂纳多·迪卡普里奥,凯特·温丝莱特,比利·赞恩', 'time': '1998-04-03', 'score': '9.5'}
    {'index': '7', 'image': 'http://p0.meituan.net/movie/b03e9c52c585635d2cb6a3f7c08a8a50112441.jpg@160w_220h_1e_1c', 'title': '龙猫', 'actor': '日高法子,坂本千夏,糸井重里', 'time': '1988-04-16(日本)', 'score': '9.2'}
    {'index': '8', 'image': 'http://p0.meituan.net/movie/da64660f82b98cdc1b8a3804e69609e041108.jpg@160w_220h_1e_1c', 'title': '唐伯虎点秋香', 'actor': '周星驰,巩俐,郑佩佩', 'time': '1993-07-01(中国香港)', 'score': '9.2'}
    {'index': '9', 'image': 'http://p0.meituan.net/movie/b076ce63e9860ecf1ee9839badee5228329384.jpg@160w_220h_1e_1c', 'title': '千与千寻', 'actor': '柊瑠美,入野自由,夏木真理', 'time': '2001-07-20(日本)', 'score': '9.3'}
    {'index': '10', 'image': 'http://p0.meituan.net/movie/46c29a8b8d8424bdda7715e6fd779c66235684.jpg@160w_220h_1e_1c', 'title': '魂断蓝桥', 'actor': '费雯·丽,罗伯特·泰勒,露塞尔·沃特森', 'time': '1940-05-17(美国)', 'score': '9.2'}
    


```python

第五步：循环，将10页的内容都抓取过来
1、先看网页结构
2、找到 offset

```


```python
import requests
from requests.exceptions import RequestException
import re
import json

def get_one_page(url):
    try:
        response = requests.get(url)
        if response.status_code == 200:
            return response.text
        return None
    except RequestException:
        return None

# 第二步，插入的解析页,解析html代码

def parse_one_page(html):
    pattern = re.compile('<dd>.*?board-index.*?>(\d+)</i>.*?data-src="(.*?)".*?name"><a'
                         +'.*?>(.*?)</a>.*?star">(.*?)</p>.*?releasetime">(.*?)</p>'
                         +'.*?integer">(.*?)</i>.*?fraction">(.*?)</i>.*?</dd>', re.S)
    items = re.findall(pattern, html)

#第三步，将其变成字典的形式
    for item in items:
        yield {
            'index':item[0],
            'image':item[1],
            'title':item[2],
            'actor':item[3].strip()[3:], # 使用切片-strip功能，去掉 主演：这三个字符
            'time':item[4].strip()[5:],
            'score':item[5]+item[6]
        }

def write_to_file(content): # 第四步，存储到文件
    with open('result100.txt','a',encoding='utf-8') as f:
        f.write(json.dumps(content, ensure_ascii=False) + '\n') # 使用json.dump，把其字典形式 转为 字符串，再添加个换行
        f.close()
    
def main(offset): # 第五步，加入 offset
    url = 'http://maoyan.com/board/4?offset=' + str(offset)
    html = get_one_page(url)
    for item in parse_one_page(html): # 第三步，提取生成器，打印效果
        print(item)
        write_to_file(item) # 第四步，将其传入到文件

if __name__ == '__main__':
    for i in range(10):
        main(i*10)    
```

    {'index': '1', 'image': 'http://p1.meituan.net/movie/20803f59291c47e1e116c11963ce019e68711.jpg@160w_220h_1e_1c', 'title': '霸王别姬', 'actor': '张国荣,张丰毅,巩俐', 'time': '1993-01-01(中国香港)', 'score': '9.6'}
    {'index': '2', 'image': 'http://p0.meituan.net/movie/283292171619cdfd5b240c8fd093f1eb255670.jpg@160w_220h_1e_1c', 'title': '肖申克的救赎', 'actor': '蒂姆·罗宾斯,摩根·弗里曼,鲍勃·冈顿', 'time': '1994-10-14(美国)', 'score': '9.5'}
    {'index': '3', 'image': 'http://p0.meituan.net/movie/54617769d96807e4d81804284ffe2a27239007.jpg@160w_220h_1e_1c', 'title': '罗马假日', 'actor': '格利高里·派克,奥黛丽·赫本,埃迪·艾伯特', 'time': '1953-09-02(美国)', 'score': '9.1'}
    {'index': '4', 'image': 'http://p0.meituan.net/movie/e55ec5d18ccc83ba7db68caae54f165f95924.jpg@160w_220h_1e_1c', 'title': '这个杀手不太冷', 'actor': '让·雷诺,加里·奥德曼,娜塔莉·波特曼', 'time': '1994-09-14(法国)', 'score': '9.5'}
    {'index': '5', 'image': 'http://p1.meituan.net/movie/f5a924f362f050881f2b8f82e852747c118515.jpg@160w_220h_1e_1c', 'title': '教父', 'actor': '马龙·白兰度,阿尔·帕西诺,詹姆斯·肯恩', 'time': '1972-03-24(美国)', 'score': '9.3'}
    {'index': '6', 'image': 'http://p1.meituan.net/movie/0699ac97c82cf01638aa5023562d6134351277.jpg@160w_220h_1e_1c', 'title': '泰坦尼克号', 'actor': '莱昂纳多·迪卡普里奥,凯特·温丝莱特,比利·赞恩', 'time': '1998-04-03', 'score': '9.5'}
    {'index': '7', 'image': 'http://p0.meituan.net/movie/b03e9c52c585635d2cb6a3f7c08a8a50112441.jpg@160w_220h_1e_1c', 'title': '龙猫', 'actor': '日高法子,坂本千夏,糸井重里', 'time': '1988-04-16(日本)', 'score': '9.2'}
    {'index': '8', 'image': 'http://p0.meituan.net/movie/da64660f82b98cdc1b8a3804e69609e041108.jpg@160w_220h_1e_1c', 'title': '唐伯虎点秋香', 'actor': '周星驰,巩俐,郑佩佩', 'time': '1993-07-01(中国香港)', 'score': '9.2'}
    {'index': '9', 'image': 'http://p0.meituan.net/movie/b076ce63e9860ecf1ee9839badee5228329384.jpg@160w_220h_1e_1c', 'title': '千与千寻', 'actor': '柊瑠美,入野自由,夏木真理', 'time': '2001-07-20(日本)', 'score': '9.3'}
    {'index': '10', 'image': 'http://p0.meituan.net/movie/46c29a8b8d8424bdda7715e6fd779c66235684.jpg@160w_220h_1e_1c', 'title': '魂断蓝桥', 'actor': '费雯·丽,罗伯特·泰勒,露塞尔·沃特森', 'time': '1940-05-17(美国)', 'score': '9.2'}
    {'index': '11', 'image': 'http://p0.meituan.net/movie/230e71d398e0c54730d58dc4bb6e4cca51662.jpg@160w_220h_1e_1c', 'title': '乱世佳人', 'actor': '费雯·丽,克拉克·盖博,奥利维娅·德哈维兰', 'time': '1939-12-15(美国)', 'score': '9.1'}
    {'index': '12', 'image': 'http://p1.meituan.net/movie/18e3191039d5e71562477659301f04aa61905.jpg@160w_220h_1e_1c', 'title': '喜剧之王', 'actor': '周星驰,莫文蔚,张柏芝', 'time': '1999-02-13(中国香港)', 'score': '9.2'}
    {'index': '13', 'image': 'http://p1.meituan.net/movie/ba1ed511668402605ed369350ab779d6319397.jpg@160w_220h_1e_1c', 'title': '天空之城', 'actor': '寺田农,鹫尾真知子,龟山助清', 'time': '1992', 'score': '9.1'}
    {'index': '14', 'image': 'http://p1.meituan.net/movie/14a7b337e8063e3ce05a5993ed80176b74208.jpg@160w_220h_1e_1c', 'title': '大闹天宫', 'actor': '邱岳峰,毕克,富润生', 'time': '1965-12-31', 'score': '9.0'}
    {'index': '15', 'image': 'http://p1.meituan.net/movie/39ed7a0941a3604bba78d299b11a18ce119679.jpg@160w_220h_1e_1c', 'title': '辛德勒的名单', 'actor': '连姆·尼森,拉尔夫·费因斯,本·金斯利', 'time': '1993-12-15(美国)', 'score': '9.2'}
    {'index': '16', 'image': 'http://p1.meituan.net/movie/6bc004d57358ee6875faa5e9a1239140128550.jpg@160w_220h_1e_1c', 'title': '音乐之声', 'actor': '朱莉·安德鲁斯,克里斯托弗·普卢默,埃琳诺·帕克', 'time': '1965-03-02(美国)', 'score': '9.0'}
    {'index': '17', 'image': 'http://p0.meituan.net/movie/ae7245920d95c03765fe1615f3a1fe3865785.jpg@160w_220h_1e_1c', 'title': '春光乍泄', 'actor': '张国荣,梁朝伟,张震', 'time': '1997-05-30(中国香港)', 'score': '9.2'}
    {'index': '18', 'image': 'http://p1.meituan.net/movie/0e91ffcfa7e53449216cc29ee8af513a75791.jpg@160w_220h_1e_1c', 'title': '剪刀手爱德华', 'actor': '约翰尼·德普,薇诺娜·瑞德,黛安·韦斯特', 'time': '1990-12-06(美国)', 'score': '8.8'}
    {'index': '19', 'image': 'http://p0.meituan.net/movie/43d259ecbcd53e8bbe902632772281d6327525.jpg@160w_220h_1e_1c', 'title': '美丽人生', 'actor': '罗伯托·贝尼尼,尼可莱塔·布拉斯基,乔治·坎塔里尼', 'time': '1997-12-20(意大利)', 'score': '9.3'}
    {'index': '20', 'image': 'http://p1.meituan.net/movie/c15b7623cce2f51c75562a3baefe507b68290.jpg@160w_220h_1e_1c', 'title': '海上钢琴师', 'actor': '蒂姆·罗斯,普路特·泰勒·文斯,比尔·努恩', 'time': '1998-10-28(意大利)', 'score': '9.2'}
    {'index': '21', 'image': 'http://p1.meituan.net/movie/d981a12f59d3cc92ff666094404ad8f0211220.jpg@160w_220h_1e_1c', 'title': '黑客帝国', 'actor': '基努·里维斯,凯瑞-安·莫斯,劳伦斯·菲什伯恩', 'time': '2000-01-14', 'score': '9.0'}
    {'index': '22', 'image': 'http://p0.meituan.net/movie/932bdfbef5be3543e6b136246aeb99b8123736.jpg@160w_220h_1e_1c', 'title': '指环王3：王者无敌', 'actor': '伊莱贾·伍德,伊恩·麦克莱恩,丽芙·泰勒', 'time': '2004-03-15', 'score': '9.2'}
    {'index': '23', 'image': 'http://p1.meituan.net/movie/b449893ebc63d5c54eb4a5b60341f334383831.jpg@160w_220h_1e_1c', 'title': '加勒比海盗', 'actor': '约翰尼·德普,凯拉·奈特莉,奥兰多·布鲁姆', 'time': '2003-11-21', 'score': '8.9'}
    {'index': '24', 'image': 'http://p1.meituan.net/movie/aacb9ed2a6601bfe515ef0970add1715623792.jpg@160w_220h_1e_1c', 'title': '哈利·波特与魔法石', 'actor': '丹尼尔·雷德克里夫,鲁伯特·格林特,艾玛·沃森', 'time': '2002-01-26', 'score': '9.1'}
    {'index': '25', 'image': 'http://p0.meituan.net/movie/d12a1c198ad9ffac72b5db57feacb449294699.jpg@160w_220h_1e_1c', 'title': '蝙蝠侠：黑暗骑士', 'actor': '克里斯蒂安·贝尔,希斯·莱杰,艾伦·艾克哈特', 'time': '2008-07-18(美国)', 'score': '9.3'}
    {'index': '26', 'image': 'http://p0.meituan.net/movie/8959888ee0c399b0fe53a714bc8a5a17460048.jpg@160w_220h_1e_1c', 'title': '楚门的世界', 'actor': '金·凯瑞,劳拉·琳妮,诺亚·艾默里奇', 'time': '1998-06-01(美国)', 'score': '8.9'}
    {'index': '27', 'image': 'http://p1.meituan.net/movie/53b6f0b66882a53b08896c92076515a8236400.jpg@160w_220h_1e_1c', 'title': '射雕英雄传之东成西就', 'actor': '张国荣,梁朝伟,张学友', 'time': '1993-02-05(中国香港)', 'score': '8.9'}
    {'index': '28', 'image': 'http://p1.meituan.net/movie/0d93b5b585ce29c6688e43f3989fb41f86421.jpg@160w_220h_1e_1c', 'title': '无间道', 'actor': '刘德华,梁朝伟,黄秋生', 'time': '2003-09-05', 'score': '9.1'}
    {'index': '29', 'image': 'http://p1.meituan.net/movie/7bac8bfa6739c18620065132ce9c64fa85110.jpg@160w_220h_1e_1c', 'title': '教父2', 'actor': '阿尔·帕西诺,罗伯特·德尼罗,黛安·基顿', 'time': '1974-12-12(美国)', 'score': '9.0'}
    {'index': '30', 'image': 'http://p0.meituan.net/movie/5cfa597a98b35ee4ee598695942641ba287922.jpg@160w_220h_1e_1c', 'title': '指环王2：双塔奇兵', 'actor': '伊莱贾·伍德,伊恩·麦克莱恩,丽芙·泰勒', 'time': '2003-04-25', 'score': '9.1'}
    {'index': '31', 'image': 'http://p1.meituan.net/movie/4592eef6b6dffcd1d950f55f41ab098f239816.jpg@160w_220h_1e_1c', 'title': '机器人总动员', 'actor': '本·贝尔特,艾丽莎·奈特,杰夫·格尔林', 'time': '2008-06-27(美国)', 'score': '9.3'}
    {'index': '32', 'image': 'http://p0.meituan.net/movie/4c41068ef7608c1d4fbfbe6016e589f7204391.jpg@160w_220h_1e_1c', 'title': '活着', 'actor': '葛优,巩俐,牛犇', 'time': '1994-05-18(法国)', 'score': '9.0'}
    {'index': '33', 'image': 'http://p1.meituan.net/movie/779bcc212a50a2526343362778f6b63c334618.jpg@160w_220h_1e_1c', 'title': '拯救大兵瑞恩', 'actor': '汤姆·汉克斯,马特·达蒙,汤姆·塞兹摩尔', 'time': '1998-07-24(美国)', 'score': '8.9'}
    {'index': '34', 'image': 'http://p1.meituan.net/movie/618e57ddb3173de6bbf2e278946b11f279679.jpg@160w_220h_1e_1c', 'title': '天堂电影院', 'actor': '菲利普·努瓦雷,赛尔乔·卡斯特利托,蒂兹亚娜·罗达托', 'time': '1988-11-17(意大利)', 'score': '9.2'}
    {'index': '35', 'image': 'http://p0.meituan.net/movie/0127b451d5b8f0679c6f81c8ed414bb2432442.jpg@160w_220h_1e_1c', 'title': '哈尔的移动城堡', 'actor': '倍赏千惠子,木村拓哉,美轮明宏', 'time': '2004-11-20(日本)', 'score': '9.0'}
    {'index': '36', 'image': 'http://p0.meituan.net/movie/7787c10ad5e95b03cf83ef9473500d8e282796.jpg@160w_220h_1e_1c', 'title': '忠犬八公的故事', 'actor': 'Forest,理查·基尔,琼·艾伦', 'time': '2010-03-12(英国)', 'score': '9.3'}
    {'index': '37', 'image': 'http://p1.meituan.net/movie/7e471a9171a410ebc9413b2f1de67afc130067.jpg@160w_220h_1e_1c', 'title': '东邪西毒', 'actor': '张国荣,梁朝伟,刘嘉玲', 'time': '1994-09-17', 'score': '8.9'}
    {'index': '38', 'image': 'http://p0.meituan.net/movie/6ab1882a217e848acceb240365043d53329196.jpg@160w_220h_1e_1c', 'title': '幽灵公主', 'actor': '松田洋治,石田百合子,田中裕子', 'time': '1997-07-12(日本)', 'score': '8.9'}
    {'index': '39', 'image': 'http://p1.meituan.net/movie/2f344a9f9575edbcae9f0abe0578bc90339773.jpg@160w_220h_1e_1c', 'title': '盗梦空间', 'actor': '莱昂纳多·迪卡普里奥,渡边谦,约瑟夫·高登-莱维特', 'time': '2010-09-01', 'score': '9.2'}
    {'index': '40', 'image': 'http://p1.meituan.net/movie/c5e76795bf7a78b12a2ffabb4a0c5c11112921.jpg@160w_220h_1e_1c', 'title': '搏击俱乐部', 'actor': '爱德华·诺顿,布拉德·皮特,海伦娜·伯翰·卡特', 'time': '1999-10-15(美国)', 'score': '8.8'}
    {'index': '41', 'image': 'http://p1.meituan.net/movie/d5e5e53ef9bbd98223e83df261b51b84103223.jpg@160w_220h_1e_1c', 'title': '疯狂原始人', 'actor': '尼古拉斯·凯奇,艾玛·斯通,瑞恩·雷诺兹', 'time': '2013-04-20', 'score': '9.5'}
    {'index': '42', 'image': 'http://p1.meituan.net/movie/91f575ec93f019f428d1f33e3ceca7c5115495.jpg@160w_220h_1e_1c', 'title': '阿凡达', 'actor': '萨姆·沃辛顿,佐伊·索尔达娜,米歇尔·罗德里格兹', 'time': '2010-01-04', 'score': '9.0'}
    {'index': '43', 'image': 'http://p1.meituan.net/movie/4a4c84aa103ab47202f1aa907c5542a4128882.jpg@160w_220h_1e_1c', 'title': 'V字仇杀队', 'actor': '娜塔莉·波特曼,雨果·维文,斯蒂芬·瑞', 'time': '2006-03-17(美国)', 'score': '8.8'}
    {'index': '44', 'image': 'http://p0.meituan.net/movie/4f9638ba234c3fb673f23a09968db875371576.jpg@160w_220h_1e_1c', 'title': '风之谷', 'actor': '岛本须美,永井一郎,坂本千夏', 'time': '1992', 'score': '8.9'}
    {'index': '45', 'image': 'http://p0.meituan.net/movie/7cd18fcf0b4f9180500124711e81492994030.jpg@160w_220h_1e_1c', 'title': '放牛班的春天', 'actor': '热拉尔·朱尼奥,尚-巴堤·莫里耶,玛丽·布奈尔', 'time': '2004-10-16', 'score': '8.9'}
    {'index': '46', 'image': 'http://p1.meituan.net/movie/5896de3c1474277730e321c9b1db04a9205644.jpg@160w_220h_1e_1c', 'title': '当幸福来敲门', 'actor': '威尔·史密斯,贾登·史密斯,坦迪·牛顿', 'time': '2008-01-17', 'score': '8.9'}
    {'index': '47', 'image': 'http://p0.meituan.net/movie/df15efd261060d3094a73ef679888d4f238149.jpg@160w_220h_1e_1c', 'title': '十二怒汉', 'actor': '亨利·方达,李·科布,马丁·鲍尔萨姆', 'time': '1957-04-13(美国)', 'score': '9.1'}
    {'index': '48', 'image': 'http://p1.meituan.net/movie/1d0fa86bcf7a44484b9c16ac6af5be68191952.jpg@160w_220h_1e_1c', 'title': '速度与激情5', 'actor': '范·迪塞尔,保罗·沃克,道恩·强森', 'time': '2011-05-12', 'score': '9.2'}
    {'index': '49', 'image': 'http://p1.meituan.net/movie/8194ae885ed9419aadf35c196af86ba4239039.jpg@160w_220h_1e_1c', 'title': '驯龙高手', 'actor': '杰伊·巴鲁切尔,杰拉德·巴特勒,亚美莉卡·费雷拉', 'time': '2010-05-14', 'score': '9.0'}
    {'index': '50', 'image': 'http://p1.meituan.net/movie/f8e9d5a90224746d15dfdbd53d4fae3d209420.jpg@160w_220h_1e_1c', 'title': '勇敢的心', 'actor': '梅尔·吉布森,苏菲·玛索,帕特里克·麦高汉', 'time': '1995-05-24(美国)', 'score': '8.8'}
    {'index': '51', 'image': 'http://p0.meituan.net/movie/85c2bfba6025bfbfb53291ae5924c215308805.jpg@160w_220h_1e_1c', 'title': '神偷奶爸', 'actor': '史蒂夫·卡瑞尔,杰森·席格尔,拉塞尔·布兰德', 'time': '2010-07-09(美国)', 'score': '9.0'}
    {'index': '52', 'image': 'http://p0.meituan.net/movie/47dd790e19dad72b50580641de5608c5199014.jpg@160w_220h_1e_1c', 'title': '飞屋环游记', 'actor': '爱德华·阿斯纳,乔丹·长井,鲍勃·彼德森', 'time': '2009-08-04', 'score': '8.9'}
    {'index': '53', 'image': 'http://p1.meituan.net/movie/5ca6ffcbb994a51cd6215e7c4fff2d9b71039.jpg@160w_220h_1e_1c', 'title': '黑客帝国3：矩阵革命', 'actor': '基努·里维斯,雨果·维文,凯瑞-安·莫斯', 'time': '2003-11-05', 'score': '8.8'}
    {'index': '54', 'image': 'http://p0.meituan.net/movie/457a35fda360cb72090fa6dcbd1db3c1275333.jpg@160w_220h_1e_1c', 'title': '怦然心动', 'actor': '玛德琳·卡罗尔,卡兰·麦克奥利菲,艾丹·奎因', 'time': '2010-08-06(美国)', 'score': '8.9'}
    {'index': '55', 'image': 'http://p0.meituan.net/movie/4bb144bc0a674ba6908349018fd092e6330929.jpg@160w_220h_1e_1c', 'title': '三傻大闹宝莱坞', 'actor': '阿米尔·汗,黄渤,卡琳娜·卡普尔', 'time': '2011-12-08', 'score': '9.1'}
    {'index': '56', 'image': 'http://p0.meituan.net/movie/e71affe126eeb4f8bfcc738cbddeebc8288766.jpg@160w_220h_1e_1c', 'title': '断背山', 'actor': '希斯·莱杰,杰克·吉伦哈尔,米歇尔·威廉姆斯', 'time': '2006-01-13(美国)', 'score': '9.0'}
    {'index': '57', 'image': 'http://p0.meituan.net/movie/7cb7965469cb7ff95613714389f1ea3d87743.jpg@160w_220h_1e_1c', 'title': '闻香识女人', 'actor': '阿尔·帕西诺,克里斯·奥唐纳,加布里埃尔·安瓦尔', 'time': '1992-12-23(美国)', 'score': '8.8'}
    {'index': '58', 'image': 'http://p1.meituan.net/movie/0b507aa44c4dfbbcc91949b69b1b39a168922.jpg@160w_220h_1e_1c', 'title': '鬼子来了', 'actor': '姜文,姜宏波,陈强', 'time': '2000-05-12(法国戛纳)', 'score': '8.9'}
    {'index': '59', 'image': 'http://p1.meituan.net/movie/4dddd98730274c3b1464ff0a0ad195e5233381.jpg@160w_220h_1e_1c', 'title': '飞越疯人院', 'actor': '杰克·尼科尔森,路易丝·弗莱彻,威尔·萨姆森', 'time': '1975-11-19(美国)', 'score': '8.8'}
    {'index': '60', 'image': 'http://p1.meituan.net/movie/92198a6fc8c3f5d13aa1bdf203572c0f99438.jpg@160w_220h_1e_1c', 'title': '美国往事', 'actor': '罗伯特·德尼罗,詹姆斯·伍兹,伊丽莎白·麦戈文', 'time': '1984-02-17(美国)', 'score': '9.1'}
    {'index': '61', 'image': 'http://p1.meituan.net/movie/75c0d3eb584be030a01f2e26741a8f41251454.jpg@160w_220h_1e_1c', 'title': '致命魔术', 'actor': '休·杰克曼,克里斯蒂安·贝尔,迈克尔·凯恩', 'time': '2006-10-20(美国)', 'score': '8.8'}
    {'index': '62', 'image': 'http://p0.meituan.net/movie/34998e31c6d07475f1add6b8b16fd21d192579.jpg@160w_220h_1e_1c', 'title': '少年派的奇幻漂流', 'actor': '苏拉·沙玛,伊尔凡·可汗,塔布', 'time': '2012-11-22', 'score': '9.1'}
    {'index': '63', 'image': 'http://p0.meituan.net/movie/7b7d1f8aa36d7a15463ce6942708a1a7265296.jpg@160w_220h_1e_1c', 'title': '美丽心灵', 'actor': '罗素·克劳,詹妮弗·康纳利,艾德·哈里斯', 'time': '2001-12-21(美国)', 'score': '8.8'}
    {'index': '64', 'image': 'http://p1.meituan.net/movie/68fa7db99e958c47d7aa07d015845a6f335154.jpg@160w_220h_1e_1c', 'title': '哈利·波特与死亡圣器（下）', 'actor': '丹尼尔·雷德克里夫,鲁伯特·格林特,艾玛·沃森', 'time': '2011-08-04', 'score': '9.0'}
    {'index': '65', 'image': 'http://p0.meituan.net/movie/7ec873ba943f13e3c63789d899bd0e23256871.jpg@160w_220h_1e_1c', 'title': '夜访吸血鬼', 'actor': '汤姆·克鲁斯,布拉德·皮特,克斯汀·邓斯特', 'time': '1994-11-11(美国)', 'score': '8.8'}
    {'index': '66', 'image': 'http://p0.meituan.net/movie/92eb862c42c49f8e41e459c369c4512b226610.jpg@160w_220h_1e_1c', 'title': '大话西游之月光宝盒', 'actor': '周星驰,莫文蔚,吴孟达', 'time': '2014-10-24', 'score': '9.6'}
    {'index': '67', 'image': 'http://p1.meituan.net/movie/96bb58f3e9d213fb0438987d16d27561379209.jpg@160w_220h_1e_1c', 'title': '蝙蝠侠：黑暗骑士崛起', 'actor': '克里斯蒂安·贝尔,迈克尔·凯恩,加里·奥德曼', 'time': '2012-08-27', 'score': '8.9'}
    {'index': '68', 'image': 'http://p1.meituan.net/movie/484171372de45945e8bbbcc97db57e09136701.jpg@160w_220h_1e_1c', 'title': '钢琴家', 'actor': '艾德里安·布洛迪,艾米莉娅·福克斯,米哈乌·热布罗夫斯基', 'time': '2002-09-25(法国)', 'score': '8.8'}
    {'index': '69', 'image': 'http://p0.meituan.net/movie/fcc17667b8343131101eeb4c67d90bf9150883.jpg@160w_220h_1e_1c', 'title': '无敌破坏王', 'actor': '约翰·C·赖利,萨拉·西尔弗曼,简·林奇', 'time': '2012-11-06', 'score': '9.0'}
    {'index': '70', 'image': 'http://p1.meituan.net/movie/6d0510f326bf145dcf49a901fb949b77278838.jpg@160w_220h_1e_1c', 'title': '倩女幽魂', 'actor': '张国荣,王祖贤,午马', 'time': '2011-04-30', 'score': '9.1'}
    {'index': '71', 'image': 'http://p0.meituan.net/movie/2526f77c650bf7cf3d5ee2dccdeac332244951.jpg@160w_220h_1e_1c', 'title': '本杰明·巴顿奇事', 'actor': '布拉德·皮特,凯特·布兰切特,塔拉吉·P·汉森', 'time': '2008-12-25(美国)', 'score': '8.8'}
    {'index': '72', 'image': 'http://p1.meituan.net/movie/7ed07b8ea8c0e0d0c7b685d20e3ec64e232004.jpg@160w_220h_1e_1c', 'title': '初恋这件小事', 'actor': '马里奥·毛瑞尔,平采娜·乐维瑟派布恩,阿查拉那·阿瑞亚卫考', 'time': '2012-06-05', 'score': '8.8'}
    {'index': '73', 'image': 'http://p0.meituan.net/movie/9e9f12cfc1f54c973dda6c85bd3a139d334520.jpg@160w_220h_1e_1c', 'title': '新龙门客栈', 'actor': '张曼玉,梁家辉,甄子丹', 'time': '2012-02-24', 'score': '8.8'}
    {'index': '74', 'image': 'http://p1.meituan.net/movie/8ad5a0f521fb15637dfdf9cab38d414453783.jpg@160w_220h_1e_1c', 'title': '甜蜜蜜', 'actor': '黎明,张曼玉,曾志伟', 'time': '2015-02-13', 'score': '9.2'}
    {'index': '75', 'image': 'http://p0.meituan.net/movie/7874ba1378033b0b491df0cc56c43d25221208.jpg@160w_220h_1e_1c', 'title': '触不可及', 'actor': '弗朗索瓦·克鲁塞,奥玛·希,安娜·勒尼', 'time': '2011-11-02(法国)', 'score': '9.1'}
    {'index': '76', 'image': 'http://p0.meituan.net/movie/40/9791315.jpg@160w_220h_1e_1c', 'title': '熔炉', 'actor': '孔刘,郑有美,金智英', 'time': '2011-09-22(韩国)', 'score': '8.8'}
    {'index': '77', 'image': 'http://p1.meituan.net/movie/dc2246233a6f5ac1e34c7176b602c8ca174557.jpg@160w_220h_1e_1c', 'title': '大话西游之大圣娶亲', 'actor': '周星驰,朱茵,莫文蔚', 'time': '2014-10-24', 'score': '8.8'}
    {'index': '78', 'image': 'http://p1.meituan.net/movie/bc7b6ababa54e11577d45c05e84a33af54072.jpg@160w_220h_1e_1c', 'title': '小鞋子', 'actor': '默罕默德·阿米尔·纳吉,Kamal Mirkarimi,Behzad Rafi', 'time': '1999-01-22(美国)', 'score': '9.1'}
    {'index': '79', 'image': 'http://p0.meituan.net/movie/4cc4c55c29b77b090485ce9943bf6f87274708.jpg@160w_220h_1e_1c', 'title': '素媛', 'actor': '李来,薛耿求,严志媛', 'time': '2013-10-02(韩国)', 'score': '9.1'}
    {'index': '80', 'image': 'http://p0.meituan.net/movie/5420be40e3b755ffe04779b9b199e935256906.jpg@160w_220h_1e_1c', 'title': '萤火之森', 'actor': '内山昂辉,佐仓绫音,后藤弘树', 'time': '2011-09-17(日本)', 'score': '9.0'}
    {'index': '81', 'image': 'http://p0.meituan.net/movie/3985eaf3858bea0f2a3d966bf7ee2103178217.jpg@160w_220h_1e_1c', 'title': '窃听风暴', 'actor': '乌尔里希·穆埃,塞巴斯蒂安·科赫,马蒂娜·格德克', 'time': '2006-03-23(德国)', 'score': '9.0'}
    {'index': '82', 'image': 'http://p1.meituan.net/movie/a0e0426a4390f5ecb49d25770a184dc0150779.jpg@160w_220h_1e_1c', 'title': '穿条纹睡衣的男孩', 'actor': '阿萨·巴特菲尔德,维拉·法米加,大卫·休里斯', 'time': '2008-09-12(英国)', 'score': '9.0'}
    {'index': '83', 'image': 'http://p0.meituan.net/movie/4abc8c932cfacfc0089e2883765d02d1295222.jpg@160w_220h_1e_1c', 'title': '时空恋旅人', 'actor': '瑞秋·麦克亚当斯,多姆纳尔·格里森,比尔·奈伊', 'time': '2013-09-04(英国)', 'score': '8.9'}
    {'index': '84', 'image': 'http://p0.meituan.net/movie/ce262f261f69fc3d679020402336a4af270365.jpg@160w_220h_1e_1c', 'title': '借东西的小人阿莉埃蒂', 'actor': '志田未来,神木隆之介,大竹忍', 'time': '2010-07-17(日本)', 'score': '8.8'}
    {'index': '85', 'image': 'http://p0.meituan.net/movie/b5ff0216e689b3fcc065590c48cd5105255305.jpg@160w_220h_1e_1c', 'title': '恐怖直播', 'actor': '河正宇,李璟荣,李大为', 'time': '2013-07-31(韩国)', 'score': '8.8'}
    {'index': '86', 'image': 'http://p1.meituan.net/movie/6a6e74b2c289f9fa4433dd2dc04a7741331638.jpg@160w_220h_1e_1c', 'title': '7号房的礼物', 'actor': '柳承龙,郑镇荣,朴信惠', 'time': '2013-01-23(韩国)', 'score': '8.9'}
    {'index': '87', 'image': 'http://p0.meituan.net/movie/7373dbba07b50ce6f24336edb96b2ea4271536.jpg@160w_220h_1e_1c', 'title': '海豚湾', 'actor': '里克·奥巴瑞,路易·西霍尤斯,哈迪·琼斯', 'time': '2009-07-31(美国)', 'score': '8.9'}
    {'index': '88', 'image': 'http://p1.meituan.net/movie/c835b3588d0061ed3b992388a0a96f15160913.jpg@160w_220h_1e_1c', 'title': '忠犬八公物语', 'actor': '仲代达矢,春川真澄,井川比佐志', 'time': '1987-08-01(日本)', 'score': '9.0'}
    {'index': '89', 'image': 'http://p1.meituan.net/movie/b553d13f30100db731ab6cf45668e52d94703.jpg@160w_220h_1e_1c', 'title': '上帝之城', 'actor': '亚历桑德雷·罗德里格斯,艾莉丝·布拉加,莱安德鲁·菲尔米诺', 'time': '2002-08-30(巴西)', 'score': '8.9'}
    {'index': '90', 'image': 'http://p0.meituan.net/movie/8fabf3894b7d12d3d2f6e66404813670265761.jpg@160w_220h_1e_1c', 'title': '辩护人', 'actor': '宋康昊,郭度沅,吴达洙', 'time': '2013-12-18(韩国)', 'score': '8.8'}
    {'index': '91', 'image': 'http://p1.meituan.net/movie/73349facab53529ab9e079c6c8c7c059281729.jpg@160w_220h_1e_1c', 'title': '七武士', 'actor': '三船敏郎,志村乔,千秋实', 'time': '1954-04-26(日本)', 'score': '9.1'}
    {'index': '92', 'image': 'http://p1.meituan.net/movie/2c0a5fedf4b43d142121b91c6ccabe1b59051.jpg@160w_220h_1e_1c', 'title': '一一', 'actor': '吴念真,金燕玲,李凯莉', 'time': '2000-09-20(法国)', 'score': '8.9'}
    {'index': '93', 'image': 'http://p1.meituan.net/movie/30310858fdab34c7a17cfd7ec8ad8bfc112201.jpg@160w_220h_1e_1c', 'title': '完美的世界', 'actor': '凯文·科斯特纳,克林特·伊斯特伍德,T·J·劳瑟', 'time': '1993-11-24(美国)', 'score': '8.9'}
    {'index': '94', 'image': 'http://p0.meituan.net/movie/0018b57299d0d4540330a31244c880a9112971.jpg@160w_220h_1e_1c', 'title': '海洋', 'actor': '雅克·贝汉,姜文,兰斯洛特·贝汉', 'time': '2011-08-12', 'score': '9.0'}
    {'index': '95', 'image': 'http://p1.meituan.net/movie/36a893c53a13f9bb934071b86ae3b5c492427.jpg@160w_220h_1e_1c', 'title': '爱·回家', 'actor': '俞承豪,金艺芬,童孝熙', 'time': '2002-04-05(韩国)', 'score': '9.0'}
    {'index': '96', 'image': 'http://p1.meituan.net/movie/9bff56ed3ea38bb1825daa1d354bc92352781.jpg@160w_220h_1e_1c', 'title': '黄金三镖客', 'actor': '克林特·伊斯特伍德,李·范·克里夫,埃里·瓦拉赫', 'time': '1966-12-23(意大利)', 'score': '8.9'}
    {'index': '97', 'image': 'http://p1.meituan.net/movie/ed50b58bf636d207c56989872a91f4cf305138.jpg@160w_220h_1e_1c', 'title': '我爱你', 'actor': '宋在浩,李顺才,尹秀晶', 'time': '2011-02-17(韩国)', 'score': '9.0'}
    {'index': '98', 'image': 'http://p1.meituan.net/movie/a1634f4e49c8517ae0a3e4adcac6b0dc43994.jpg@160w_220h_1e_1c', 'title': '迁徙的鸟', 'actor': '雅克·贝汉,Philippe Labro', 'time': '2001-12-12(法国)', 'score': '9.1'}
    {'index': '99', 'image': 'http://p0.meituan.net/movie/885fc379c614a2b4175587b95ac98eb95045650.jpg@160w_220h_1e_1c', 'title': '阿飞正传', 'actor': '张国荣,张曼玉,刘德华', 'time': '2018-06-25', 'score': '8.8'}
    {'index': '100', 'image': 'http://p0.meituan.net/movie/3e5f5f3aa4b7e5576521e26c2c7c894d253975.jpg@160w_220h_1e_1c', 'title': '英雄本色', 'actor': '狄龙,张国荣,周润发', 'time': '2017-11-17', 'score': '9.2'}
    


```python


第六步：如果想实现 秒抓 的效果，需要引入一个 进程池，提供指定的进程，
        明显提高抓取效率

```


```python
import requests
from requests.exceptions import RequestException
from multiprocessing import Pool
import re
import json

def get_one_page(url):
    try:
        response = requests.get(url)
        if response.status_code == 200:
            return response.text
        return None
    except RequestException:
        return None

# 第二步，插入的解析页,解析html代码

def parse_one_page(html):
    pattern = re.compile('<dd>.*?board-index.*?>(\d+)</i>.*?data-src="(.*?)".*?name"><a'
                         +'.*?>(.*?)</a>.*?star">(.*?)</p>.*?releasetime">(.*?)</p>'
                         +'.*?integer">(.*?)</i>.*?fraction">(.*?)</i>.*?</dd>', re.S)
    items = re.findall(pattern, html)

#第三步，将其变成字典的形式
    for item in items:
        yield {
            'index':item[0],
            'image':item[1],
            'title':item[2],
            'actor':item[3].strip()[3:], # 使用切片-strip功能，去掉 主演：这三个字符
            'time':item[4].strip()[5:],
            'score':item[5]+item[6]
        }

def write_to_file(content): # 第四步，存储到文件
    with open('result1010.txt','a',encoding='utf-8') as f:
        f.write(json.dumps(content, ensure_ascii=False) + '\n') # 使用json.dump，把其字典形式 转为 字符串，再添加个换行
        f.close()
    
def main(offset): # 第五步，加入 offset
    url = 'http://maoyan.com/board/4?offset=' + str(offset)
    html = get_one_page(url)
    for item in parse_one_page(html): # 第三步，提取生成器，打印效果
        print(item)
        write_to_file(item) # 第四步，将其传入到文件

if __name__ == '__main__':
    for i in range(10):
        main(i*10)    
    pool = Pool()
    pool.map(main, [i*10 for i in range(10)])
```

    {'index': '1', 'image': 'http://p1.meituan.net/movie/20803f59291c47e1e116c11963ce019e68711.jpg@160w_220h_1e_1c', 'title': '霸王别姬', 'actor': '张国荣,张丰毅,巩俐', 'time': '1993-01-01(中国香港)', 'score': '9.6'}
    {'index': '2', 'image': 'http://p0.meituan.net/movie/283292171619cdfd5b240c8fd093f1eb255670.jpg@160w_220h_1e_1c', 'title': '肖申克的救赎', 'actor': '蒂姆·罗宾斯,摩根·弗里曼,鲍勃·冈顿', 'time': '1994-10-14(美国)', 'score': '9.5'}
    {'index': '3', 'image': 'http://p0.meituan.net/movie/54617769d96807e4d81804284ffe2a27239007.jpg@160w_220h_1e_1c', 'title': '罗马假日', 'actor': '格利高里·派克,奥黛丽·赫本,埃迪·艾伯特', 'time': '1953-09-02(美国)', 'score': '9.1'}
    {'index': '4', 'image': 'http://p0.meituan.net/movie/e55ec5d18ccc83ba7db68caae54f165f95924.jpg@160w_220h_1e_1c', 'title': '这个杀手不太冷', 'actor': '让·雷诺,加里·奥德曼,娜塔莉·波特曼', 'time': '1994-09-14(法国)', 'score': '9.5'}
    {'index': '5', 'image': 'http://p1.meituan.net/movie/f5a924f362f050881f2b8f82e852747c118515.jpg@160w_220h_1e_1c', 'title': '教父', 'actor': '马龙·白兰度,阿尔·帕西诺,詹姆斯·肯恩', 'time': '1972-03-24(美国)', 'score': '9.3'}
    {'index': '6', 'image': 'http://p1.meituan.net/movie/0699ac97c82cf01638aa5023562d6134351277.jpg@160w_220h_1e_1c', 'title': '泰坦尼克号', 'actor': '莱昂纳多·迪卡普里奥,凯特·温丝莱特,比利·赞恩', 'time': '1998-04-03', 'score': '9.5'}
    {'index': '7', 'image': 'http://p0.meituan.net/movie/b03e9c52c585635d2cb6a3f7c08a8a50112441.jpg@160w_220h_1e_1c', 'title': '龙猫', 'actor': '日高法子,坂本千夏,糸井重里', 'time': '1988-04-16(日本)', 'score': '9.2'}
    {'index': '8', 'image': 'http://p0.meituan.net/movie/da64660f82b98cdc1b8a3804e69609e041108.jpg@160w_220h_1e_1c', 'title': '唐伯虎点秋香', 'actor': '周星驰,巩俐,郑佩佩', 'time': '1993-07-01(中国香港)', 'score': '9.2'}
    {'index': '9', 'image': 'http://p0.meituan.net/movie/b076ce63e9860ecf1ee9839badee5228329384.jpg@160w_220h_1e_1c', 'title': '千与千寻', 'actor': '柊瑠美,入野自由,夏木真理', 'time': '2001-07-20(日本)', 'score': '9.3'}
    {'index': '10', 'image': 'http://p0.meituan.net/movie/46c29a8b8d8424bdda7715e6fd779c66235684.jpg@160w_220h_1e_1c', 'title': '魂断蓝桥', 'actor': '费雯·丽,罗伯特·泰勒,露塞尔·沃特森', 'time': '1940-05-17(美国)', 'score': '9.2'}
    {'index': '11', 'image': 'http://p0.meituan.net/movie/230e71d398e0c54730d58dc4bb6e4cca51662.jpg@160w_220h_1e_1c', 'title': '乱世佳人', 'actor': '费雯·丽,克拉克·盖博,奥利维娅·德哈维兰', 'time': '1939-12-15(美国)', 'score': '9.1'}
    {'index': '12', 'image': 'http://p1.meituan.net/movie/18e3191039d5e71562477659301f04aa61905.jpg@160w_220h_1e_1c', 'title': '喜剧之王', 'actor': '周星驰,莫文蔚,张柏芝', 'time': '1999-02-13(中国香港)', 'score': '9.2'}
    {'index': '13', 'image': 'http://p1.meituan.net/movie/ba1ed511668402605ed369350ab779d6319397.jpg@160w_220h_1e_1c', 'title': '天空之城', 'actor': '寺田农,鹫尾真知子,龟山助清', 'time': '1992', 'score': '9.1'}
    {'index': '14', 'image': 'http://p1.meituan.net/movie/14a7b337e8063e3ce05a5993ed80176b74208.jpg@160w_220h_1e_1c', 'title': '大闹天宫', 'actor': '邱岳峰,毕克,富润生', 'time': '1965-12-31', 'score': '9.0'}
    {'index': '15', 'image': 'http://p1.meituan.net/movie/39ed7a0941a3604bba78d299b11a18ce119679.jpg@160w_220h_1e_1c', 'title': '辛德勒的名单', 'actor': '连姆·尼森,拉尔夫·费因斯,本·金斯利', 'time': '1993-12-15(美国)', 'score': '9.2'}
    {'index': '16', 'image': 'http://p1.meituan.net/movie/6bc004d57358ee6875faa5e9a1239140128550.jpg@160w_220h_1e_1c', 'title': '音乐之声', 'actor': '朱莉·安德鲁斯,克里斯托弗·普卢默,埃琳诺·帕克', 'time': '1965-03-02(美国)', 'score': '9.0'}
    {'index': '17', 'image': 'http://p0.meituan.net/movie/ae7245920d95c03765fe1615f3a1fe3865785.jpg@160w_220h_1e_1c', 'title': '春光乍泄', 'actor': '张国荣,梁朝伟,张震', 'time': '1997-05-30(中国香港)', 'score': '9.2'}
    {'index': '18', 'image': 'http://p1.meituan.net/movie/0e91ffcfa7e53449216cc29ee8af513a75791.jpg@160w_220h_1e_1c', 'title': '剪刀手爱德华', 'actor': '约翰尼·德普,薇诺娜·瑞德,黛安·韦斯特', 'time': '1990-12-06(美国)', 'score': '8.8'}
    {'index': '19', 'image': 'http://p0.meituan.net/movie/43d259ecbcd53e8bbe902632772281d6327525.jpg@160w_220h_1e_1c', 'title': '美丽人生', 'actor': '罗伯托·贝尼尼,尼可莱塔·布拉斯基,乔治·坎塔里尼', 'time': '1997-12-20(意大利)', 'score': '9.3'}
    {'index': '20', 'image': 'http://p1.meituan.net/movie/c15b7623cce2f51c75562a3baefe507b68290.jpg@160w_220h_1e_1c', 'title': '海上钢琴师', 'actor': '蒂姆·罗斯,普路特·泰勒·文斯,比尔·努恩', 'time': '1998-10-28(意大利)', 'score': '9.2'}
    {'index': '21', 'image': 'http://p1.meituan.net/movie/d981a12f59d3cc92ff666094404ad8f0211220.jpg@160w_220h_1e_1c', 'title': '黑客帝国', 'actor': '基努·里维斯,凯瑞-安·莫斯,劳伦斯·菲什伯恩', 'time': '2000-01-14', 'score': '9.0'}
    {'index': '22', 'image': 'http://p0.meituan.net/movie/932bdfbef5be3543e6b136246aeb99b8123736.jpg@160w_220h_1e_1c', 'title': '指环王3：王者无敌', 'actor': '伊莱贾·伍德,伊恩·麦克莱恩,丽芙·泰勒', 'time': '2004-03-15', 'score': '9.2'}
    {'index': '23', 'image': 'http://p1.meituan.net/movie/b449893ebc63d5c54eb4a5b60341f334383831.jpg@160w_220h_1e_1c', 'title': '加勒比海盗', 'actor': '约翰尼·德普,凯拉·奈特莉,奥兰多·布鲁姆', 'time': '2003-11-21', 'score': '8.9'}
    {'index': '24', 'image': 'http://p1.meituan.net/movie/aacb9ed2a6601bfe515ef0970add1715623792.jpg@160w_220h_1e_1c', 'title': '哈利·波特与魔法石', 'actor': '丹尼尔·雷德克里夫,鲁伯特·格林特,艾玛·沃森', 'time': '2002-01-26', 'score': '9.1'}
    {'index': '25', 'image': 'http://p0.meituan.net/movie/d12a1c198ad9ffac72b5db57feacb449294699.jpg@160w_220h_1e_1c', 'title': '蝙蝠侠：黑暗骑士', 'actor': '克里斯蒂安·贝尔,希斯·莱杰,艾伦·艾克哈特', 'time': '2008-07-18(美国)', 'score': '9.3'}
    {'index': '26', 'image': 'http://p0.meituan.net/movie/8959888ee0c399b0fe53a714bc8a5a17460048.jpg@160w_220h_1e_1c', 'title': '楚门的世界', 'actor': '金·凯瑞,劳拉·琳妮,诺亚·艾默里奇', 'time': '1998-06-01(美国)', 'score': '8.9'}
    {'index': '27', 'image': 'http://p1.meituan.net/movie/53b6f0b66882a53b08896c92076515a8236400.jpg@160w_220h_1e_1c', 'title': '射雕英雄传之东成西就', 'actor': '张国荣,梁朝伟,张学友', 'time': '1993-02-05(中国香港)', 'score': '8.9'}
    {'index': '28', 'image': 'http://p1.meituan.net/movie/0d93b5b585ce29c6688e43f3989fb41f86421.jpg@160w_220h_1e_1c', 'title': '无间道', 'actor': '刘德华,梁朝伟,黄秋生', 'time': '2003-09-05', 'score': '9.1'}
    {'index': '29', 'image': 'http://p1.meituan.net/movie/7bac8bfa6739c18620065132ce9c64fa85110.jpg@160w_220h_1e_1c', 'title': '教父2', 'actor': '阿尔·帕西诺,罗伯特·德尼罗,黛安·基顿', 'time': '1974-12-12(美国)', 'score': '9.0'}
    {'index': '30', 'image': 'http://p0.meituan.net/movie/5cfa597a98b35ee4ee598695942641ba287922.jpg@160w_220h_1e_1c', 'title': '指环王2：双塔奇兵', 'actor': '伊莱贾·伍德,伊恩·麦克莱恩,丽芙·泰勒', 'time': '2003-04-25', 'score': '9.1'}
    {'index': '31', 'image': 'http://p1.meituan.net/movie/4592eef6b6dffcd1d950f55f41ab098f239816.jpg@160w_220h_1e_1c', 'title': '机器人总动员', 'actor': '本·贝尔特,艾丽莎·奈特,杰夫·格尔林', 'time': '2008-06-27(美国)', 'score': '9.3'}
    {'index': '32', 'image': 'http://p0.meituan.net/movie/4c41068ef7608c1d4fbfbe6016e589f7204391.jpg@160w_220h_1e_1c', 'title': '活着', 'actor': '葛优,巩俐,牛犇', 'time': '1994-05-18(法国)', 'score': '9.0'}
    {'index': '33', 'image': 'http://p1.meituan.net/movie/779bcc212a50a2526343362778f6b63c334618.jpg@160w_220h_1e_1c', 'title': '拯救大兵瑞恩', 'actor': '汤姆·汉克斯,马特·达蒙,汤姆·塞兹摩尔', 'time': '1998-07-24(美国)', 'score': '8.9'}
    {'index': '34', 'image': 'http://p1.meituan.net/movie/618e57ddb3173de6bbf2e278946b11f279679.jpg@160w_220h_1e_1c', 'title': '天堂电影院', 'actor': '菲利普·努瓦雷,赛尔乔·卡斯特利托,蒂兹亚娜·罗达托', 'time': '1988-11-17(意大利)', 'score': '9.2'}
    {'index': '35', 'image': 'http://p0.meituan.net/movie/0127b451d5b8f0679c6f81c8ed414bb2432442.jpg@160w_220h_1e_1c', 'title': '哈尔的移动城堡', 'actor': '倍赏千惠子,木村拓哉,美轮明宏', 'time': '2004-11-20(日本)', 'score': '9.0'}
    {'index': '36', 'image': 'http://p0.meituan.net/movie/7787c10ad5e95b03cf83ef9473500d8e282796.jpg@160w_220h_1e_1c', 'title': '忠犬八公的故事', 'actor': 'Forest,理查·基尔,琼·艾伦', 'time': '2010-03-12(英国)', 'score': '9.3'}
    {'index': '37', 'image': 'http://p1.meituan.net/movie/7e471a9171a410ebc9413b2f1de67afc130067.jpg@160w_220h_1e_1c', 'title': '东邪西毒', 'actor': '张国荣,梁朝伟,刘嘉玲', 'time': '1994-09-17', 'score': '8.9'}
    {'index': '38', 'image': 'http://p0.meituan.net/movie/6ab1882a217e848acceb240365043d53329196.jpg@160w_220h_1e_1c', 'title': '幽灵公主', 'actor': '松田洋治,石田百合子,田中裕子', 'time': '1997-07-12(日本)', 'score': '8.9'}
    {'index': '39', 'image': 'http://p1.meituan.net/movie/2f344a9f9575edbcae9f0abe0578bc90339773.jpg@160w_220h_1e_1c', 'title': '盗梦空间', 'actor': '莱昂纳多·迪卡普里奥,渡边谦,约瑟夫·高登-莱维特', 'time': '2010-09-01', 'score': '9.2'}
    {'index': '40', 'image': 'http://p1.meituan.net/movie/c5e76795bf7a78b12a2ffabb4a0c5c11112921.jpg@160w_220h_1e_1c', 'title': '搏击俱乐部', 'actor': '爱德华·诺顿,布拉德·皮特,海伦娜·伯翰·卡特', 'time': '1999-10-15(美国)', 'score': '8.8'}
    {'index': '41', 'image': 'http://p1.meituan.net/movie/d5e5e53ef9bbd98223e83df261b51b84103223.jpg@160w_220h_1e_1c', 'title': '疯狂原始人', 'actor': '尼古拉斯·凯奇,艾玛·斯通,瑞恩·雷诺兹', 'time': '2013-04-20', 'score': '9.5'}
    {'index': '42', 'image': 'http://p1.meituan.net/movie/91f575ec93f019f428d1f33e3ceca7c5115495.jpg@160w_220h_1e_1c', 'title': '阿凡达', 'actor': '萨姆·沃辛顿,佐伊·索尔达娜,米歇尔·罗德里格兹', 'time': '2010-01-04', 'score': '9.0'}
    {'index': '43', 'image': 'http://p1.meituan.net/movie/4a4c84aa103ab47202f1aa907c5542a4128882.jpg@160w_220h_1e_1c', 'title': 'V字仇杀队', 'actor': '娜塔莉·波特曼,雨果·维文,斯蒂芬·瑞', 'time': '2006-03-17(美国)', 'score': '8.8'}
    {'index': '44', 'image': 'http://p0.meituan.net/movie/4f9638ba234c3fb673f23a09968db875371576.jpg@160w_220h_1e_1c', 'title': '风之谷', 'actor': '岛本须美,永井一郎,坂本千夏', 'time': '1992', 'score': '8.9'}
    {'index': '45', 'image': 'http://p0.meituan.net/movie/7cd18fcf0b4f9180500124711e81492994030.jpg@160w_220h_1e_1c', 'title': '放牛班的春天', 'actor': '热拉尔·朱尼奥,尚-巴堤·莫里耶,玛丽·布奈尔', 'time': '2004-10-16', 'score': '8.9'}
    {'index': '46', 'image': 'http://p1.meituan.net/movie/5896de3c1474277730e321c9b1db04a9205644.jpg@160w_220h_1e_1c', 'title': '当幸福来敲门', 'actor': '威尔·史密斯,贾登·史密斯,坦迪·牛顿', 'time': '2008-01-17', 'score': '8.9'}
    {'index': '47', 'image': 'http://p0.meituan.net/movie/df15efd261060d3094a73ef679888d4f238149.jpg@160w_220h_1e_1c', 'title': '十二怒汉', 'actor': '亨利·方达,李·科布,马丁·鲍尔萨姆', 'time': '1957-04-13(美国)', 'score': '9.1'}
    {'index': '48', 'image': 'http://p1.meituan.net/movie/1d0fa86bcf7a44484b9c16ac6af5be68191952.jpg@160w_220h_1e_1c', 'title': '速度与激情5', 'actor': '范·迪塞尔,保罗·沃克,道恩·强森', 'time': '2011-05-12', 'score': '9.2'}
    {'index': '49', 'image': 'http://p1.meituan.net/movie/8194ae885ed9419aadf35c196af86ba4239039.jpg@160w_220h_1e_1c', 'title': '驯龙高手', 'actor': '杰伊·巴鲁切尔,杰拉德·巴特勒,亚美莉卡·费雷拉', 'time': '2010-05-14', 'score': '9.0'}
    {'index': '50', 'image': 'http://p1.meituan.net/movie/f8e9d5a90224746d15dfdbd53d4fae3d209420.jpg@160w_220h_1e_1c', 'title': '勇敢的心', 'actor': '梅尔·吉布森,苏菲·玛索,帕特里克·麦高汉', 'time': '1995-05-24(美国)', 'score': '8.8'}
    {'index': '51', 'image': 'http://p0.meituan.net/movie/85c2bfba6025bfbfb53291ae5924c215308805.jpg@160w_220h_1e_1c', 'title': '神偷奶爸', 'actor': '史蒂夫·卡瑞尔,杰森·席格尔,拉塞尔·布兰德', 'time': '2010-07-09(美国)', 'score': '9.0'}
    {'index': '52', 'image': 'http://p0.meituan.net/movie/47dd790e19dad72b50580641de5608c5199014.jpg@160w_220h_1e_1c', 'title': '飞屋环游记', 'actor': '爱德华·阿斯纳,乔丹·长井,鲍勃·彼德森', 'time': '2009-08-04', 'score': '8.9'}
    {'index': '53', 'image': 'http://p1.meituan.net/movie/5ca6ffcbb994a51cd6215e7c4fff2d9b71039.jpg@160w_220h_1e_1c', 'title': '黑客帝国3：矩阵革命', 'actor': '基努·里维斯,雨果·维文,凯瑞-安·莫斯', 'time': '2003-11-05', 'score': '8.8'}
    {'index': '54', 'image': 'http://p0.meituan.net/movie/457a35fda360cb72090fa6dcbd1db3c1275333.jpg@160w_220h_1e_1c', 'title': '怦然心动', 'actor': '玛德琳·卡罗尔,卡兰·麦克奥利菲,艾丹·奎因', 'time': '2010-08-06(美国)', 'score': '8.9'}
    {'index': '55', 'image': 'http://p0.meituan.net/movie/4bb144bc0a674ba6908349018fd092e6330929.jpg@160w_220h_1e_1c', 'title': '三傻大闹宝莱坞', 'actor': '阿米尔·汗,黄渤,卡琳娜·卡普尔', 'time': '2011-12-08', 'score': '9.1'}
    {'index': '56', 'image': 'http://p0.meituan.net/movie/e71affe126eeb4f8bfcc738cbddeebc8288766.jpg@160w_220h_1e_1c', 'title': '断背山', 'actor': '希斯·莱杰,杰克·吉伦哈尔,米歇尔·威廉姆斯', 'time': '2006-01-13(美国)', 'score': '9.0'}
    {'index': '57', 'image': 'http://p0.meituan.net/movie/7cb7965469cb7ff95613714389f1ea3d87743.jpg@160w_220h_1e_1c', 'title': '闻香识女人', 'actor': '阿尔·帕西诺,克里斯·奥唐纳,加布里埃尔·安瓦尔', 'time': '1992-12-23(美国)', 'score': '8.8'}
    {'index': '58', 'image': 'http://p1.meituan.net/movie/0b507aa44c4dfbbcc91949b69b1b39a168922.jpg@160w_220h_1e_1c', 'title': '鬼子来了', 'actor': '姜文,姜宏波,陈强', 'time': '2000-05-12(法国戛纳)', 'score': '8.9'}
    {'index': '59', 'image': 'http://p1.meituan.net/movie/4dddd98730274c3b1464ff0a0ad195e5233381.jpg@160w_220h_1e_1c', 'title': '飞越疯人院', 'actor': '杰克·尼科尔森,路易丝·弗莱彻,威尔·萨姆森', 'time': '1975-11-19(美国)', 'score': '8.8'}
    {'index': '60', 'image': 'http://p1.meituan.net/movie/92198a6fc8c3f5d13aa1bdf203572c0f99438.jpg@160w_220h_1e_1c', 'title': '美国往事', 'actor': '罗伯特·德尼罗,詹姆斯·伍兹,伊丽莎白·麦戈文', 'time': '1984-02-17(美国)', 'score': '9.1'}
    {'index': '61', 'image': 'http://p1.meituan.net/movie/75c0d3eb584be030a01f2e26741a8f41251454.jpg@160w_220h_1e_1c', 'title': '致命魔术', 'actor': '休·杰克曼,克里斯蒂安·贝尔,迈克尔·凯恩', 'time': '2006-10-20(美国)', 'score': '8.8'}
    {'index': '62', 'image': 'http://p0.meituan.net/movie/34998e31c6d07475f1add6b8b16fd21d192579.jpg@160w_220h_1e_1c', 'title': '少年派的奇幻漂流', 'actor': '苏拉·沙玛,伊尔凡·可汗,塔布', 'time': '2012-11-22', 'score': '9.1'}
    {'index': '63', 'image': 'http://p0.meituan.net/movie/7b7d1f8aa36d7a15463ce6942708a1a7265296.jpg@160w_220h_1e_1c', 'title': '美丽心灵', 'actor': '罗素·克劳,詹妮弗·康纳利,艾德·哈里斯', 'time': '2001-12-21(美国)', 'score': '8.8'}
    {'index': '64', 'image': 'http://p1.meituan.net/movie/68fa7db99e958c47d7aa07d015845a6f335154.jpg@160w_220h_1e_1c', 'title': '哈利·波特与死亡圣器（下）', 'actor': '丹尼尔·雷德克里夫,鲁伯特·格林特,艾玛·沃森', 'time': '2011-08-04', 'score': '9.0'}
    {'index': '65', 'image': 'http://p0.meituan.net/movie/7ec873ba943f13e3c63789d899bd0e23256871.jpg@160w_220h_1e_1c', 'title': '夜访吸血鬼', 'actor': '汤姆·克鲁斯,布拉德·皮特,克斯汀·邓斯特', 'time': '1994-11-11(美国)', 'score': '8.8'}
    {'index': '66', 'image': 'http://p0.meituan.net/movie/92eb862c42c49f8e41e459c369c4512b226610.jpg@160w_220h_1e_1c', 'title': '大话西游之月光宝盒', 'actor': '周星驰,莫文蔚,吴孟达', 'time': '2014-10-24', 'score': '9.6'}
    {'index': '67', 'image': 'http://p1.meituan.net/movie/96bb58f3e9d213fb0438987d16d27561379209.jpg@160w_220h_1e_1c', 'title': '蝙蝠侠：黑暗骑士崛起', 'actor': '克里斯蒂安·贝尔,迈克尔·凯恩,加里·奥德曼', 'time': '2012-08-27', 'score': '8.9'}
    {'index': '68', 'image': 'http://p1.meituan.net/movie/484171372de45945e8bbbcc97db57e09136701.jpg@160w_220h_1e_1c', 'title': '钢琴家', 'actor': '艾德里安·布洛迪,艾米莉娅·福克斯,米哈乌·热布罗夫斯基', 'time': '2002-09-25(法国)', 'score': '8.8'}
    {'index': '69', 'image': 'http://p0.meituan.net/movie/fcc17667b8343131101eeb4c67d90bf9150883.jpg@160w_220h_1e_1c', 'title': '无敌破坏王', 'actor': '约翰·C·赖利,萨拉·西尔弗曼,简·林奇', 'time': '2012-11-06', 'score': '9.0'}
    {'index': '70', 'image': 'http://p1.meituan.net/movie/6d0510f326bf145dcf49a901fb949b77278838.jpg@160w_220h_1e_1c', 'title': '倩女幽魂', 'actor': '张国荣,王祖贤,午马', 'time': '2011-04-30', 'score': '9.1'}
    {'index': '71', 'image': 'http://p0.meituan.net/movie/2526f77c650bf7cf3d5ee2dccdeac332244951.jpg@160w_220h_1e_1c', 'title': '本杰明·巴顿奇事', 'actor': '布拉德·皮特,凯特·布兰切特,塔拉吉·P·汉森', 'time': '2008-12-25(美国)', 'score': '8.8'}
    {'index': '72', 'image': 'http://p1.meituan.net/movie/7ed07b8ea8c0e0d0c7b685d20e3ec64e232004.jpg@160w_220h_1e_1c', 'title': '初恋这件小事', 'actor': '马里奥·毛瑞尔,平采娜·乐维瑟派布恩,阿查拉那·阿瑞亚卫考', 'time': '2012-06-05', 'score': '8.8'}
    {'index': '73', 'image': 'http://p0.meituan.net/movie/9e9f12cfc1f54c973dda6c85bd3a139d334520.jpg@160w_220h_1e_1c', 'title': '新龙门客栈', 'actor': '张曼玉,梁家辉,甄子丹', 'time': '2012-02-24', 'score': '8.8'}
    {'index': '74', 'image': 'http://p1.meituan.net/movie/8ad5a0f521fb15637dfdf9cab38d414453783.jpg@160w_220h_1e_1c', 'title': '甜蜜蜜', 'actor': '黎明,张曼玉,曾志伟', 'time': '2015-02-13', 'score': '9.2'}
    {'index': '75', 'image': 'http://p0.meituan.net/movie/7874ba1378033b0b491df0cc56c43d25221208.jpg@160w_220h_1e_1c', 'title': '触不可及', 'actor': '弗朗索瓦·克鲁塞,奥玛·希,安娜·勒尼', 'time': '2011-11-02(法国)', 'score': '9.1'}
    {'index': '76', 'image': 'http://p0.meituan.net/movie/40/9791315.jpg@160w_220h_1e_1c', 'title': '熔炉', 'actor': '孔刘,郑有美,金智英', 'time': '2011-09-22(韩国)', 'score': '8.8'}
    {'index': '77', 'image': 'http://p1.meituan.net/movie/dc2246233a6f5ac1e34c7176b602c8ca174557.jpg@160w_220h_1e_1c', 'title': '大话西游之大圣娶亲', 'actor': '周星驰,朱茵,莫文蔚', 'time': '2014-10-24', 'score': '8.8'}
    {'index': '78', 'image': 'http://p1.meituan.net/movie/bc7b6ababa54e11577d45c05e84a33af54072.jpg@160w_220h_1e_1c', 'title': '小鞋子', 'actor': '默罕默德·阿米尔·纳吉,Kamal Mirkarimi,Behzad Rafi', 'time': '1999-01-22(美国)', 'score': '9.1'}
    {'index': '79', 'image': 'http://p0.meituan.net/movie/4cc4c55c29b77b090485ce9943bf6f87274708.jpg@160w_220h_1e_1c', 'title': '素媛', 'actor': '李来,薛耿求,严志媛', 'time': '2013-10-02(韩国)', 'score': '9.1'}
    {'index': '80', 'image': 'http://p0.meituan.net/movie/5420be40e3b755ffe04779b9b199e935256906.jpg@160w_220h_1e_1c', 'title': '萤火之森', 'actor': '内山昂辉,佐仓绫音,后藤弘树', 'time': '2011-09-17(日本)', 'score': '9.0'}
    {'index': '81', 'image': 'http://p0.meituan.net/movie/3985eaf3858bea0f2a3d966bf7ee2103178217.jpg@160w_220h_1e_1c', 'title': '窃听风暴', 'actor': '乌尔里希·穆埃,塞巴斯蒂安·科赫,马蒂娜·格德克', 'time': '2006-03-23(德国)', 'score': '9.0'}
    {'index': '82', 'image': 'http://p1.meituan.net/movie/a0e0426a4390f5ecb49d25770a184dc0150779.jpg@160w_220h_1e_1c', 'title': '穿条纹睡衣的男孩', 'actor': '阿萨·巴特菲尔德,维拉·法米加,大卫·休里斯', 'time': '2008-09-12(英国)', 'score': '9.0'}
    {'index': '83', 'image': 'http://p0.meituan.net/movie/4abc8c932cfacfc0089e2883765d02d1295222.jpg@160w_220h_1e_1c', 'title': '时空恋旅人', 'actor': '瑞秋·麦克亚当斯,多姆纳尔·格里森,比尔·奈伊', 'time': '2013-09-04(英国)', 'score': '8.9'}
    {'index': '84', 'image': 'http://p0.meituan.net/movie/ce262f261f69fc3d679020402336a4af270365.jpg@160w_220h_1e_1c', 'title': '借东西的小人阿莉埃蒂', 'actor': '志田未来,神木隆之介,大竹忍', 'time': '2010-07-17(日本)', 'score': '8.8'}
    {'index': '85', 'image': 'http://p0.meituan.net/movie/b5ff0216e689b3fcc065590c48cd5105255305.jpg@160w_220h_1e_1c', 'title': '恐怖直播', 'actor': '河正宇,李璟荣,李大为', 'time': '2013-07-31(韩国)', 'score': '8.8'}
    {'index': '86', 'image': 'http://p1.meituan.net/movie/6a6e74b2c289f9fa4433dd2dc04a7741331638.jpg@160w_220h_1e_1c', 'title': '7号房的礼物', 'actor': '柳承龙,郑镇荣,朴信惠', 'time': '2013-01-23(韩国)', 'score': '8.9'}
    {'index': '87', 'image': 'http://p0.meituan.net/movie/7373dbba07b50ce6f24336edb96b2ea4271536.jpg@160w_220h_1e_1c', 'title': '海豚湾', 'actor': '里克·奥巴瑞,路易·西霍尤斯,哈迪·琼斯', 'time': '2009-07-31(美国)', 'score': '8.9'}
    {'index': '88', 'image': 'http://p1.meituan.net/movie/c835b3588d0061ed3b992388a0a96f15160913.jpg@160w_220h_1e_1c', 'title': '忠犬八公物语', 'actor': '仲代达矢,春川真澄,井川比佐志', 'time': '1987-08-01(日本)', 'score': '9.0'}
    {'index': '89', 'image': 'http://p1.meituan.net/movie/b553d13f30100db731ab6cf45668e52d94703.jpg@160w_220h_1e_1c', 'title': '上帝之城', 'actor': '亚历桑德雷·罗德里格斯,艾莉丝·布拉加,莱安德鲁·菲尔米诺', 'time': '2002-08-30(巴西)', 'score': '8.9'}
    {'index': '90', 'image': 'http://p0.meituan.net/movie/8fabf3894b7d12d3d2f6e66404813670265761.jpg@160w_220h_1e_1c', 'title': '辩护人', 'actor': '宋康昊,郭度沅,吴达洙', 'time': '2013-12-18(韩国)', 'score': '8.8'}
    {'index': '91', 'image': 'http://p1.meituan.net/movie/73349facab53529ab9e079c6c8c7c059281729.jpg@160w_220h_1e_1c', 'title': '七武士', 'actor': '三船敏郎,志村乔,千秋实', 'time': '1954-04-26(日本)', 'score': '9.1'}
    {'index': '92', 'image': 'http://p1.meituan.net/movie/2c0a5fedf4b43d142121b91c6ccabe1b59051.jpg@160w_220h_1e_1c', 'title': '一一', 'actor': '吴念真,金燕玲,李凯莉', 'time': '2000-09-20(法国)', 'score': '8.9'}
    {'index': '93', 'image': 'http://p1.meituan.net/movie/30310858fdab34c7a17cfd7ec8ad8bfc112201.jpg@160w_220h_1e_1c', 'title': '完美的世界', 'actor': '凯文·科斯特纳,克林特·伊斯特伍德,T·J·劳瑟', 'time': '1993-11-24(美国)', 'score': '8.9'}
    {'index': '94', 'image': 'http://p0.meituan.net/movie/0018b57299d0d4540330a31244c880a9112971.jpg@160w_220h_1e_1c', 'title': '海洋', 'actor': '雅克·贝汉,姜文,兰斯洛特·贝汉', 'time': '2011-08-12', 'score': '9.0'}
    {'index': '95', 'image': 'http://p1.meituan.net/movie/36a893c53a13f9bb934071b86ae3b5c492427.jpg@160w_220h_1e_1c', 'title': '爱·回家', 'actor': '俞承豪,金艺芬,童孝熙', 'time': '2002-04-05(韩国)', 'score': '9.0'}
    {'index': '96', 'image': 'http://p1.meituan.net/movie/9bff56ed3ea38bb1825daa1d354bc92352781.jpg@160w_220h_1e_1c', 'title': '黄金三镖客', 'actor': '克林特·伊斯特伍德,李·范·克里夫,埃里·瓦拉赫', 'time': '1966-12-23(意大利)', 'score': '8.9'}
    {'index': '97', 'image': 'http://p1.meituan.net/movie/ed50b58bf636d207c56989872a91f4cf305138.jpg@160w_220h_1e_1c', 'title': '我爱你', 'actor': '宋在浩,李顺才,尹秀晶', 'time': '2011-02-17(韩国)', 'score': '9.0'}
    {'index': '98', 'image': 'http://p1.meituan.net/movie/a1634f4e49c8517ae0a3e4adcac6b0dc43994.jpg@160w_220h_1e_1c', 'title': '迁徙的鸟', 'actor': '雅克·贝汉,Philippe Labro', 'time': '2001-12-12(法国)', 'score': '9.1'}
    {'index': '99', 'image': 'http://p0.meituan.net/movie/885fc379c614a2b4175587b95ac98eb95045650.jpg@160w_220h_1e_1c', 'title': '阿飞正传', 'actor': '张国荣,张曼玉,刘德华', 'time': '2018-06-25', 'score': '8.8'}
    {'index': '100', 'image': 'http://p0.meituan.net/movie/3e5f5f3aa4b7e5576521e26c2c7c894d253975.jpg@160w_220h_1e_1c', 'title': '英雄本色', 'actor': '狄龙,张国荣,周润发', 'time': '2017-11-17', 'score': '9.2'}
    
