# flowerss bot

[![Build Status](https://github.com/indes/flowerss-bot/workflows/Release/badge.svg)](https://github.com/indes/flowerss-bot/actions?query=workflow%3ARelease)
[![Test Status](https://github.com/indes/flowerss-bot/workflows/Test/badge.svg)](https://github.com/indes/flowerss-bot/actions?query=workflow%3ATest)
![Build Docker Image](https://github.com/indes/flowerss-bot/workflows/Build%20Docker%20Image/badge.svg)
[![Go Report Card](https://goreportcard.com/badge/github.com/indes/flowerss-bot)](https://goreportcard.com/report/github.com/indes/flowerss-bot)
![GitHub](https://img.shields.io/github/license/indes/flowerss-bot.svg)

[安装与使用文档](https://flowerss-bot.now.sh/)  

<img src="https://github.com/rssflow/img/raw/master/images/rssflow_demo.gif" width = "300"/>

## Features

- 常见的 RSS Bot 该有的功能
- 支持 Telegram 应用内 instant view
- 支持为 Group 和 Channel 订阅 RSS 消息
- 丰富的订阅设置

## 安装与使用

详细安装与使用方法请查阅项目[使用文档](https://flowerss-bot.now.sh/)。  

部署
二进制部署
从 Releases 页面下载对应的版本解压运行即可。

Docker 部署
1.下载配置文件 在项目目录下新建 config.yml 文件

`mkdir ~/flowerss &&\`
`wget -O ~/flowerss/config.yml \
    https://raw.githubusercontent.com/indes/flowerss-bot/master/config.yml.sample`

2.修改配置文件

`vim ~/flowerss/config.yml`

修改配置文件中sqlite路径（如果使用sqlite作为数据库）：

`sqlite:
  path: /root/.flowerss/data.db`

3.运行

`docker run -d -v ~/flowerss:/root/.flowerss indes/flowerss-bot`

源码编译部署
`git clone https://github.com/indes/flowerss-bot && cd flowerss-bot`
`make build`
`./flowerss-bot`

配置
根据以下模板，新建 `config.yml` 文件。

```
bot_token: XXX
#多个telegraph_token可采用数组格式：
# telegraph_token:
#  - token_1
#  - token_2
telegraph_token: xxxx
user_agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/51.0.2704.103 Safari/537.36
preview_text: 0
disable_web_page_preview: false
socks5: 127.0.0.1:1080
update_interval: 10
error_threshold: 100
telegram:
  endpoint: https://xxx.com/
mysql:
  host: 127.0.0.1
  port: 3306
  user: user
  password: pwd
  database: flowerss
sqlite:
  path: ./data.db
allowed_users:
  - 123
  - 234
```
配置说明：
```
配置项	含义	是否必填
bot_token	Telegram Bot Token	必填
telegraph_token	Telegraph Token, 用于转存原文到 Telegraph	可忽略（不转存原文到 Telegraph ）
preview_text	纯文字预览字数（不借助Telegraph）	可忽略（默认0, 0为禁用）
user_agent	User Agent	可忽略
disable_web_page_preview	是否禁用 web 页面预览	可忽略（默认 false, true 为禁用）
update_interval	RSS 源扫描间隔（分钟）	可忽略（默认 10）
error_threshold	源最大出错次数	可忽略（默认 100）
socks5	用于无法正常 Telegram API 的环境	可忽略（能正常连接上 Telegram API 服务器）
mysql	MySQL 数据库配置	可忽略（使用 SQLite ）
sqlite	SQLite 配置	可忽略（已配置mysql时，该项失效）
telegram.endpoint	自定义telegram bot api url	可忽略（使用默认api url）
allowed_users	允许使用bot的用户telegram id，	可忽略，为空时所有用户都能使用bot
 PREVIOUS
```

使用命令：

```
/sub [url] 订阅（url 为可选）
/unsub [url] 取消订阅（url 为可选）
/list 查看当前订阅
/set 设置订阅
/check 检查当前订阅
/setfeedtag [sub id] [tag1] [tag2] 设置订阅标签（最多设置三个Tag，以空格分割）
/setinterval [interval] [sub id] 设置订阅刷新频率（可设置多个sub id，以空格分割）
/activeall 开启所有订阅
/pauseall 暂停所有订阅
/import 导入 OPML 文件
/export 导出 OPML 文件
/unsuball 取消所有订阅
/help 帮助
```
详细使用方法请查阅项目[使用文档](https://flowerss-bot.now.sh/#/usage)。 
