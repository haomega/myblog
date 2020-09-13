---
title: "HTML 起手与常用标签"
date: 2020-07-09T21:41:46+08:00
draft: false
---

# 概念

WWW：Word Wide Web 万维网，包含URL、HTTP和HTML。

W3C：万维网联盟，主要负责万维网协议的制定。

HTTP=Hyper Text Transfer Protocol 超文本传输协议。

HTML=Hyper Text Markup Lanauage 超文本标记语言。


万维网于1900年由李爵士发明，

# 常用标签

## a Tag

超链接标签，通过`<a>`标签，网页互相连接，组成了丰富多彩的网络内容形式。

### 属性

#### href
网址：
* https://google.com
* http://google.com
* //google.com 根据网页协议自动选择协议

路径：
* /a/b或a/b
* index.html或/index.html
伪协议：
* `javascript:代码;`可以执行Javascript代码，通常用于`javascript:;`不起任何作用。
* `mailto:邮箱`或`tel:手机号`

id

`href=#id` 跳转页面的指定id位置

#### target

href中的连接打开位置，比如常用的\_blank在新窗口打开。

浏览器内置（window）
* \_blank
* \_top
* \_parent
* \_sef 默认选项，本窗口

用户自定义：
* window name
* iframe name


## img Tag

图片标签，img标签会发起HTTP GET请求来加载图片资源。

### 属性

* alt
* height/width
* src

### 事件

* onload
* onerror 图片加载失败是，可以通过这个事件设置一个替换图片。


## table Tag

完整的table示例：
```html
<table>
	<thead>
		<tr>
			<th>标题</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>内容</td>
		</tr>
	</tbody>
	<tfoot>
		<tr>
			<td>表格Foot</td>
		</tr>
	</tfoot>
</table>
```

### 相关的样式

* table-layout
* border-collapse 消除表格中间烦人的空隙
* border-spacing

