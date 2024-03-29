---
title: ubuntu18.04 安装 shadowsocks 实现科学上网
tags: ubuntu,科学上网
grammar_cjkRuby: true
---


## 准备
---

- ubuntu18.04 系统的电脑一台
- shadowsocks 的客户端配置文件一份


## 步骤
---

- **安装 shadowsocks 服务**
- **新建配置文件 shadowsocks.json**
- **配置浏览器代理**
- **配置系统自启 shadowsocks 服务**


## 实践
---


- **安装 shadowsocks 服务**

- - 安装 shadowsocks

	``` dos?linenums
	sudo apt install shadowsocks
	```

- - 通过 sslocal 命名查看是否安装成功

- **新建配置文件 shadowsocks.json**

- - 先安装 vim

	``` dos?linenums
	sudo apt install vim
	sudo apt install vim-gtk3
	sudo apt install vim-tiny
	sudo apt install neovim
	sudo apt install vim-athena
	sudo apt install vim-gtk
	sudo apt install vim-nox
	```
	
- - 通过 vim 命令去新建文件 shadowsocks.json 

	``` dos?linenums
	vim /home/jialei/shadowsocks.json
	```
	
- - 写入配置内容
	
	``` json?linenums
	{
		"server":"[server-IP]",
		"server_port": [server-port],
		"local_port": 1080,
		"password": "[server-password]",
		"timeout": 600,
		"method": "aes-256-cfb"
	}
	```
	
	
- **配置浏览器代理**

- - 下载浏览器插件 [SwitchyOmega](https://github.com/FelisCatus/SwitchyOmega/releases/)
- - - 火狐浏览器下载文件 [proxy_switchyomega-2.5.11-an.fx.xpi](https://github.com/FelisCatus/SwitchyOmega/releases/download/v2.5.11/proxy_switchyomega-2.5.11-an.fx.xpi)
- - - 谷歌浏览器下载文件 [SwitchyOmega_Chromium.crx](https://github.com/FelisCatus/SwitchyOmega/releases/download/v2.5.11/SwitchyOmega_Chromium.crx)
 - - 添加插件，新建情景模式 shadowsocks
 - - - 配置情景模式 shadowsocks 的代理服务器

	| Scheme | Protocol | Server | Port |
	| -- | -- | -- | -- |
	| (default) | SOCKS5 | 127.0.0.1 | 1080 |

 - - - 配置情景模式 auto switch 

	| Condition Type | Condition Details | Profile |
	| -- | -- | -- |
	| Host wildcard | \*.google.com | shadowsocks |
	| | Add condition | |
	| | ... | |
	| Default |  | [Direct] |

- - - Import online rule lists, 输入链接 https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt

- - 通过 sslocal 运行服务，然后输入网址 www.google.com 测试

	``` dos?linenums
	sslocal -c /home/jialei/shadowsocks.json
	```
	
	
- **配置系统自启 shadowsocks 服务**

- - 安装 supervisor 管理 sslocal 启动

	``` dos?linenums
	sudo apt install supervisor
	```

- - 新建配置文件 shadowsocks.conf

	``` dos?linenums
	sudo vim /etc/supervisor/conf.d/shadowsocks.conf
	```
	
- - 写入配置内容

	``` dsconfig?linenums
	[program:shadowsocks]
	command=sslocal -c /home/jialei/shadowsocks.json
	autostart=true
	autorestart=true
	user=root
	log_stderr=true
	logfile=/var/log/shadowsocks.log
	```
	
- - 新建配置文件 rc.local

	``` dos?linenums
	sudo vim /etc/rc.local
	```
	
- - 写入配置内容

	``` dos?linenums
	service supervisor start
	```
	
- - 重启电脑后，打开浏览器输入 www.google.com 测试

- 关闭服务

	``` dos
	sudo service supervisor stop
	```

- 开启服务

	``` dos
	sudo service supervisor start
	```


## 完
