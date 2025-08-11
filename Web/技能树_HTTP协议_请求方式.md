# writeup-2025/08/11
## 启动环境后提示
HTTP Method is GET

Use CTF**B Method, I will give you flag.


Hint: If you got 「HTTP Method Not Allowed」 Error, you should request index.php.
## 方法一：使用curl工具
* 题目给出提示：CTF\*\*B 明显是 CTFHUB
* 题目让你用的是 CTFHUB 这个单词本身作为 HTTP 方法
* 是让你用 一个自定义的、非标准的 HTTP 方法名，可以用 -X 强行指定 任意字符串作为方法名
* 直接尝试用 CTFHUB 作为 HTTP 方法，在终端用 curl 发送自定义方法：curl -X CTFHUB http://challenge-d448cd253f52cf7d.sandbox.ctfhub.com:10800/index.php
* 得到flag
  
