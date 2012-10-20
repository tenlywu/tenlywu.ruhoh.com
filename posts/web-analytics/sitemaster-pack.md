---
title: SiteMaster 监控内容
date: '2012-09-20'
description: SiteMaster 发包内容与功能依赖关系。
categories: 网站分析
tags: [监测技术]
---


## 核心包（开放调用）

### V 包 —— 访问（Visit）


### P 包 —— 页面浏览（PageView）

**调用方法**
**参数说明**
**调用示例**
**发包示例**

### T 包 —— 自定义互动（CustomAction）

**调用方法**

    _smq.push(['custom', 'category', 'action', 'opt_label', opt_value, opt_isbounce])

**参数说明**

* `必选` **category**  
字符类型，将自定义互动归入的类别。

* `必选` **action**  
字符类型，给互动定义名称或类型。

* `可选` **opt_label**  
字符类型，标记此互动额外的信息。

* `可选` **opt_value**  
数值类型，将互动赋予权重价值。

* `可选` **opt_isbounce**  
数值类型，1：用户在跳出页如果触发了此事件，仍然算跳出。0：用户在跳出页如果触发了此事件，不算跳出(默认为0)。

**调用示例**

	_smq.push(['custom', '商品', '购买', '红酒', 200, 1])
	_smq.push(['custom', '商品', '购买', '', '', 1])
	_smq.push(['custom', '商品', '购买', '', 280])
	_smq.push(['custom', '商品', '购买'])
	//注意 category，action，opt_label 是字符类型，需要使用单引号。

**发包示例**

### E 包 —— 电子商务（E-Commerce）

接收电子商务信息。

## 辅助包（封闭调用）

### K 包 —— 点击（Click）

判断用户非链接点击。

### H 包 —— 心跳（Heart）

判断延时，活跃，闲置功能。

### S 包 —— 滚动（Scroll）

注意力热图。

### X 包 —— 关闭（Close）

清空缓存，定义关闭，计算时间。

## 冷藏包（未来再启用）

### I 包 —— 输入（Input）

记录用户输入内容。

### C 包 —— 复制（Copy）

记录用户复制内容。

### M 包 —— 鼠标（Mouse）

记录鼠标移动轨迹。