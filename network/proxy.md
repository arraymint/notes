(1)socks5代理，采用socks协议的代理服务器，是一种通用的代理服务器。
(2)http proxy，采用http协议代理服务器，主要代理浏览器访问网页。

```shell
export http_proxy="socks5://127.0.0.1:10808"
```
上述在socks5上模拟http代理
你会发现其中只能代理页面(ifconfig.me)
google.com等页面则不能代理

而proxychains基于socks5则可以直接代理任何页面

比如idea的也是http代理，即使选择了socks5，也是在socks5基础之上模拟http代理，作用域缩小了