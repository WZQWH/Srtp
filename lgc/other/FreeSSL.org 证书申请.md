---
title: FreeSSL.org 证书申请
tags: FreeSSL,证书,https
grammar_cjkRuby: true
date: 2018-6-25
---


## 证书申请

- 打开 [网站](https://freessl.org/) ，输入要创建证书的域名

- 填入常用邮箱，并配置一些参数（默认配置就 ok）

	![配置项](./images/1529892737106.jpg)
	
- DNS 验证，按照给出的 `TXT 记录` 和 `记录值` 去做域名解析

	![DNS 验证](./images/1529892998831.jpg)
	
- 域名解析成功后，点击验证，验证成功，则下载证书


## nginx 配置 https

- 参考上篇 [阿里云 https 域名解析](https://github.com/myArticle/StoryWriter/blob/master/%E9%98%BF%E9%87%8C%E4%BA%91%20https%20%E5%9F%9F%E5%90%8D%E9%85%8D%E7%BD%AE.md) 的 nginx 配置