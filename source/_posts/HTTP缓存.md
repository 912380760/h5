---
title: HTTP缓存
date: 2019-08-14 18:07:49
tags: http
---

## 浏览器通过HTTP标头指令来指示浏览器何时缓存响应及缓存多久
## 通过 ETag(验证令牌) / If-None-Match
服务器生成并返回一个随机令牌(通常是文件内容的哈希值或某个其他指纹),
下次请求时客户端自动在"If-None-Match" HTTP请求标头内提供ETag令牌,
服务器根据当前资源核对令牌.如果未发生变化,服务器将返回"304".
![avatar](/h5/images/etag.png)

## Cache-Control
- no-cache
必须先与服务器确认响应是否发生变化,因此如果同时存在ETag,no-cache是可以缓存的
- no-store
直接禁止浏览器以及所有中间缓存存储任何版本的响应.
- public
浏览器和CDN(代理服务器)都可缓存
- private
只有浏览器能缓存,CDN不能缓存
- max-age
缓存最长时间(单位秒),例如,"max-age=60"表示接下来的60秒缓存和重用响应

## Last-Modified / If-Modified-Since
- Last-Modified
 服务器在响应请求时，告诉浏览器资源的最后修改时间。
- If-Modified-Since
再次请求服务器时，通过此字段通知服务器上次请求时，服务器返回的资源最后修改时间。
服务器收到请求后发现有头If-Modified-Since 则与被请求资源的最后修改时间进行比对。
若资源的最后修改时间大于If-Modified-Since，说明资源又被改动过，则响应整片资源内容，返回状态码200；
若资源的最后修改时间小于或等于If-Modified-Since，说明资源无新修改，则响应HTTP 304，告知浏览器继续使用所保存的cache。

## Expires
Expires的值为服务端返回的到期时间,即下一次请求时,请求时间小于服务端返回的到期时间,直接使用缓存数据.
不过Expires是HTTP 1.0的东西,另一个问题是到期时间由服务端生成,但是客户端时间和服务端时间有误差,可能导致存储命中误差.所以现在一般使用[Cache-Control](#Cache-Control).

![avatar](/h5/images/snipaste.png.png)

## 各种刷新
- 浏览器中输入地址,回车
服务器缓存策略
- F5
去服务器检验缓存是否过期,再使用服务器缓存策略
- Ctrl + F5
不缓存,所有请求都直接去服务器拿
