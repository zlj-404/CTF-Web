# 题目
打开题目，显示hello guest. only admin can get flag
# WriteUp
## 解法1：使用开发者工具
  * F12->应用程序->左侧栏找到cookie
  * 点击目标域名，右侧表格会出现 Name / Value 列表，找到 admin 这一行，Value 列是 0
  * 双击编辑value值，改为1，保存好以后，刷新页面，出现flag

## 解法2：使用burpsuit
  * 挂上 BurpSuite 之后访问题目页面，在“代理-HTTP历史”里可以看到两个GET请求
  * 其中第二个GET请求访问http://challenge-7bc25cbdc425c4ea.sandbox.ctfhub.com:10080/favicon.ico
  * 把这个请求放入“重发器”修改Cookie: admin=0为Cookie: admin=1后发送获得响应页面里包含Flag

# 相关概念
  * Cookie 欺骗 指把浏览器里原本由服务器种下的一段 Cookie 抓出来，改掉里面的关键字段（如身份标志、权限标志、积分等），再发回服务器，从而骗过程序的身份/权限校验
  * Cookie 认证 服务器依靠浏览器每次请求自动带上的 Cookie 来识别“这是谁”。只要 Cookie 里某个字段等于预期值，就认为已通过认证。
  * Cookie 伪造 和“欺骗”基本同义，更强调“从无到有”地造出一段符合服务器校验规则的假 Cookie（例如自己算签名、伪造 JWT、重放别人的 SessionID 等）

# CTF 中常见的 3 类考法
  ## 直接改值型:
    页面提示“hello guest, only admin can get flag”，抓包看到 Cookie: admin=0，把 0 改成 1 即可
  ## 编码/加密型:
    Cookie 值经过 Base64、Hex、JSON、JWT 等编码或加密，需要先解码再改明文，再编码回去。  
    例：mycookie=ZGVtb0BkYmFwcHNlY3VyaXR5LmNvbS4uLg== → base64 解码 → 改邮箱 → 再 base64 编码
  ## 签名验证型:
    服务器在 Cookie 末尾加了一段 hash / HMAC / JWT 签名，单纯改明文会导致签名校验失败。  
    需要：
    * 找到签名密钥（源码泄露、弱密钥爆破、提示信息）
    * 重新计算合法签名
    * 或者利用“none 算法”“密钥混淆”等 JWT 绕过技巧
