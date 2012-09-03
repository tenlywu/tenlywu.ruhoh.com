---
title: SiteMaster 监控内容
date: '2012-08-17'
description: 
categories: 网站分析
tags: [监测技术]
---
### V包 访问（Visit）

当监测代码 sm.js 加载进行异步处理后，发起的第一个页面浏览监测请求时会发送 V 包。

调用方法

	_smq.push(['pageview']);

### P包 页面浏览（PageView）

当非访问的第一次页面浏览请求时，会发送 P 包。

调用方法

	_smq.push(['pageview']);

参数说明

* path (必选) 页面路径，不包含协议和host的url,以斜杠开始 /welcome?uid=1293
* title (必选) 页面标题，不选为当前页面真实的标题

调用示例

    _smq.push(['pageview', '/user/1/follow', '关注张三'])

使用场景：用户点击“注册”按钮后弹出悬浮层，测试可以在“注册”链接上加上此事件。再如，用户在下载文件的时候，可以在链接的 onclick 事件上加入以上代码。这样，在 SiteMaster 后台，用户定义的页面路径的浏览量可以作为该文件的下载量。


### T包 自定义互动（CustomAction）

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


### E 包 —— 电子商务（E-Commerce）包

> 开放调用：是

调用方法
第一步，添加订单
> _smq.push(['addTrans', id, store, total, tax, fare, city, province])

###参数说明

* id (必填) 订单唯一id号
* store (必填) 订单所属店铺名称
* total (必填) 订单总金额, 数字类型，小数点后最多两位
* tax (选填) 税金，数字类型，小数点后最多两位
* fare (选填) 运费，数字类型，小数点后最多两位
* city (选填) 所在城市名称
* province (选填) 所在省份名称

###例子
> _smq.push(['addTrans', 201208081251, '红酒屋', 12034.78, 1200.00, 100.00, '石家庄', '河北'])
> _smq.push(['addTrans', 201208081251, '红酒屋', 12034.78, 0, 0, '', '河北'])

第二步，添加商品
> _smq.push(['addItem', id, name, category, price, amount])

###参数说明

* id (必填) 商品唯一id号
* name (必填) 商品名称
* category (必填) 商品所属分类名称
* price (必填) 商品价格，数字类型，小数点后最多两位
* amount (选填) 购买数量，默认为1

###例子
> _smq.push(['addItem', 1203983, '1978拉菲', '高档红酒', 1200.00, 5])
> _smq.push(['addItem', 1203983, '1978拉菲', '高档红酒', 1200.00])

第三步，跟踪数据
> _smq.push(['trackTrans'])


## 辅助包

### K包 点击（Click）



### H包 心跳（Heart）

## I 包 —— 输入（Input）包

## C 包 —— 复制（Copy）包

## S 包 —— 滚动（Scroll）包

## X 包 —— 关闭（Close）包

## M 包 —— 鼠标（Mouse）包