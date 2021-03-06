## 前后端交互流程

前端发送请求-->后端接收请求->后端发送响应->前端接受响应

通常情况下的前端和后端的语言是不同的，比如前端使用JavaScript（TypeScript等），后端使用Java（GoLang等）。

编程语言和人类语言是类似的，不同的语言是无法交流的。

这时候就需要中间沟通的信使——HTTP协议。

HTTP使得前后端交互得以实现，前后端只需要按照HTTP的格式进行处理数据即可。

## HTTP协议

HTTP报文的包含了两个部分：请求和响应。

请求包含请求头、请求体；响应包含响应头、响应体。



[HTTP协议 - RFC2616](https://tools.ietf.org/html/rfc2616)

### 请求报文

#### 请求头

示例：

```http
GET / HTTP/1.1
Host: www.google.com
```

参数：

Accept
Accept-Charset
Accept-Encoding
Accept-Language
Authorization
Expect
From
Host
If-Match
If-Modified-Since
If-None-Match
If-Range
If-Unmodified-Since
Max-Forwards
Proxy-Authorization
Range
Referer
TE
User-Agent

#### 请求体

请求体内容格式由请求体`Content-Type`决定。



请求头：Content-Type: application/x-www-form-urlencoded

请求体：表达式格式，例如：`usernmae=xxx&password=xxx`



请求头：Content-Type: application/json

请求体：json格式，示例：

```json
{
    "username": "xxx",
    "password": "xxx"
}
```



请求头：Content-Type: application/plain

请求体：text格式



请求头：Content-Type: application/javascript

请求体：js格式



请求头：Content-Type: application/html

请求体：html



请求头：Content-Type: application/xml

请求体：xml格式



请求头：Content-Type: application/octet-stream

请求体：二进制字节流

### 响应报文

#### 响应头

示例：

```http
HTTP/1.1 200 OK
Content-Length: 3059
Server: GWS/2.0
Date: Sat, 11 Jan 2003 02:44:04 GMT
Content-Type: text/html
Cache-control: private
Set-Cookie: PREF=ID=73d4aef52e57bae9:TM=1042253044:LM=1042253044:S=SMCc_HRPCQiqy
X9j; expires=Sun, 17-Jan-2038 19:14:07 GMT; path=/; domain=.google.com
Connection: keep-alive
```

参数：

Accept-Ranges
Age
ETag
Location
Proxy-Authenticate
Retry-After
Server
Vary
WWW-Authenticate

状态码：

| 状态码 | 具体含义                                           | 常见状态           |
| :----- | :------------------------------------------------- | :----------------- |
| 1xx    | 提示信息，表示目前是协议处理的中间状态；           |                    |
| 2xx    | 成功，报文已经收到并被正确处理；                   | 200、204、206      |
| 3xx    | 重定向，资源位置发生变动，需要客户端重新发送请求； | 301、302、304      |
| 4xx    | 客户端错误，请求报文有误，服务器无法处理；         | 400、403、404      |
| 5xx    | 服务器错误，服务器在处理请求时内部发生了错误。     | 500、501、502、503 |

[http状态码 - wiki百科](https://zh.wikipedia.org/wiki/HTTP%E7%8A%B6%E6%80%81%E7%A0%81)

## 前端

### 语言

JavaScript、TypeScript等。

TypeScript是JavaScript超集，在JavaScript基础上增加了面向对象与静态类型，使项目便于维护。

### 库

axios是一款优秀的js库，用于实现AJAX。

具有相同功能的还有：XMLHttpRequest、Fetch等。

### 调试工具

Browser console，请学会使用浏览器的控制台。

## 后端

### 语言

Java、Python、GoLang等，Java使用较多。

### 框架

`Spring Framework`是一款优秀的框架，基于`Spring`开发的针对web的框架。

