# 知识点：HTTP 临时重定向（302）
  HTTP 302 Found 状态码表示资源已被临时移动至响应头中 Location 所指定的新URL。浏览器会自动发起对新地址的请求并重定向用户，同时由于此移动属于临时性，搜索引擎通常不会将原 URL 的链接权重传递给新资源。
  在网页中使用F12，在“网络”可以看到网络请求。
# writeup
* 打开靶场 → 看到一个按钮 “Give me Flag”
* 点击按钮 → 页面一闪 → 什么 flag 都没有
* 地址栏从 index.php 变成 index.html
  ## 解法1：使用curl工具访问 index.php 即可得到 flag
  curl -v http://challenge-7957ec149f5cc08a.sandbox.ctfhub.com:10800/index.php
  ## 解法2：挂上 BurpSuite 之后访问 index.php
# 题目想考什么
 * HTTP 302：服务器对你说：“东西不在这儿，去隔壁房间拿。”然后浏览器自动帮你跑腿。
 * 临时重定向：隔壁房间不一定有全部信息，原房间里可能偷偷塞了 flag。
 * 抓包 / 禁止跳转：把“跑腿小哥”拉住，自己去原房间看一眼。
