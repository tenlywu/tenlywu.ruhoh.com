---
title: 网站来源的两种切分方式 [终稿]
date: '2012-08-17'
description: SiteMaster 有两种切分方式将网站流量集合像蛋糕一样进行完整切分。
categories: 网站分析
tags: [来源]
---

当把网站的所有的 `访问` 作为一个大的集合时，每一次 `访问` 行为就是这个集合里的个体。

SiteMaster 有两种切分方式将这个集合像蛋糕一样进行完整切分。

## 一、根据 `访问` 的登陆页 smt 参数与来源地址

切分为以下五种来源：

* 推广（能继续细分`项目`、`媒体`、`广告位`、`创意`、`关键字`）
* 搜索（能继续细分`搜索引擎`、`关键字`）
* 引荐（能继续细分`来源主机名`、`网站路径`）
* 社交（能继续细分`社会网站`、`用户ID`）
* 直接（不能继续细分）

附注划分的流程逻辑：

> V：所有 `访问` 的集合。  
> X：所有 `登陆页地址` 带有合法 smt 参数的 `访问`。—— 称为 “推广” 来源。  
> Y：所有 `登陆页地址` 不带有合法 smt 参数的 `访问`。—— 称为 “非推广” 来源。

> * Y1： `来源地址` 的 `主机名` 在搜索引擎域名列表中的 `访问`。—— 称为 “搜索” 来源。  
> * Y2： `来源地址` 的 `主机名` 在社会化媒体域名列表中的 `访问`。—— 称为 “社交” 来源。  
> * Y3： `来源地址` 的 `主机名` 在不在搜索引擎与社会化媒体列表的 `访问`。—— 称为 “引荐” 来源。  
> * Y4： `来源地址` 为空的 `访问`。—— 称为 “直接” 来源。  

> ### X Y1 Y2 Y3 Y4 五集合无交集，且并集为 V。

### smt 参数定义

SMT(SiteMaster Tracker) 来源参数，是用来标注 `访问` 为特定推广渠道的 URL 变量，分为五个：

* 简称 `smt_cp`：Campaign 项目
* 简称 `smt_md`：Medium 媒体
* 简称 `smt_pl`：Placement 广告位
* 简称 `smt_ct`：Creative 创意
* 简称 `smt_kw`：Keywords 关键字

合法的 SMT 参数定义：`smt_cp`，`smt_md`，`smt_pl`是必选参数，其它两个为可选参数，必选参数缺失则不合法。注意这些参数在 URL 中使用，所以需要保证字符的合法性。

#### 奇妙的 smt_b 参数

为了实现与广告端的整合，`smt_b` 参数是一个将项目、媒体、广告位、创意、关键字打包在一起的参数，SiteMaster 系统会自动解析 `smt_b` 参数，扩充成五个开放参数的值。

如果 `smt_b` 与 `smt_**`(五个开放参数) 共存，它的优先级更高，会覆盖开放参数的值。

> 在 TrackMaster 产品中，勾选在项目属性中 `启用 smt_b 参数跟踪` 功能后，所有的跳转链接将自动带上 `smt_b` 参数。

#### 举例：

http://abc.cn/?smt_cp=Q2launch&smt_pl=newone&smt_md=sina

http://abc.cn/?smt_cp=bigband&smt_pl=cpc&smt_md=google&smt_ct=fashion&smt_kw=guitar

http://abc.cn/?smt_b=C0B0A090807060587EBEE0C


## 二、根据 `访问` 的 Cookie 历史

切分为两种情况：

* 有 `符合条件的` AdMaster Cookie 历史。
* 无 `符合条件的` AdMaster Cookie 历史。

### 符合条件的 AdMaster Cookie 历史

Cookie 是记录用户互联网匿名行为信息的小文件。AdMaster Cookie 记录了用户与 AdMaster 所监测广告接触的历史匿名化信息。

> 例：CookieID 为 10002 的用户，在两个某时间看过 广告A 与 广告B，那么 AdMaster Cookie 会记录这些信息。

符合条件的历史，是指 `访问` 发生时，只追溯最近 30 天的，且与所访问网站相关联的广告项目，所对应的 Cookie 历史。在 TrackMaster 系统项目属性中，项目的`CampaignID` 与 网站的`SiteID` 是多对多的关系。

举例说明，当某访问发生时，带有了 AdMaster Cookie 历史如下：

	2012-02-01 22:22:22 曝光了 项目201/媒体104/广告位401/创意0 的广告
	2012-02-02 22:22:22 曝光了 项目101/媒体101/广告位101/创意101 的广告
	2012-02-02 22:22:25 点击了 项目101/媒体101/广告位101/创意101 的广告
	2012-02-03 12:02:22 点击了 项目104/媒体104/广告位104/创意0 的广告
	2012-02-12 22:22:22 曝光了 项目201/媒体104/广告位401/创意0 的广告
	2012-02-22 22:22:22 曝光了 项目201/媒体104/广告位403/创意0 的广告
	2012-03-09 17:21:39 点击了 项目304/媒体401/广告位204/创意201 的广告

如果访问的 网站 只与 **项目201** 关联，则只分析 `访问` 产生时 Cookie 中最近 30 天的历史，并忽略未关联项目的历史：

	2012-02-12 22:22:22 曝光了 项目201/媒体104/广告位401/创意0 的广告
	2012-02-22 22:22:22 曝光了 项目201/媒体104/广告位403/创意0 的广告

### 整合引导 分为 曝光引导 与 点击引导

如果分析符合条件的 AdMaster Cookie 历史后，如果存在至少一条 AdMaster 广告历史，则这次访问称之是 `整合引导`。而最近的一次历史为：

* 点击，则该访问是由 `点击引导` 的。归入该历史的特定项目、媒体、广告位、创意点击引导，关键字维度(研发中)。
* 曝光，则该访问是由 `曝光引导` 的。归入该历史的特定项目、媒体、广告位、创意曝光引导，关键字维度(研发中)。

通过整合引导、曝光引导、点击引导，可以分析广告（细分到项目、媒体、广告位、创意、关键字）五个维度下的曝光、点击、访问（曝光引导的、点击引导的）的数据，此及之间的转化与这些访问的相关指标（访问平均持续时间、跳出率等等）

> 通过 Cookie 历史进行访问的切分，需要在 TrackMaster 的项目属性中勾选 `启用 SiteMaster Cookie 打通`。

## 三、两种切分方式的关系

如果两种切分方式都被勾选了，通过这两种切分 `访问` 的方式，可以得到一种二维关系表。

![image]({{urls.media}}/img/2012/traffic-source.png)