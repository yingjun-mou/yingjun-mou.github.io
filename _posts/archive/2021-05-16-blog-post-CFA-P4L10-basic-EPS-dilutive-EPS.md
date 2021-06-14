---
title: 'EPS - Basic vs Dilutive'
date: 2021-05-16
permalink: /posts/2021/05/Basic EPS and Dilutive EPS/
tags:
  - CFA
---



EPS - Basic vs Dilutive 
======


## 1. How to calculate EPS(Earnings per share 每股收益)?

**1. Where will see the two types of EPS**: 
1. Simple capital structure (no dilutive securities) on reports basic EPS. 
2. But compelx capital structure containing dilutive securities needs to report BOTH. But when reveal it to client, need to use the relatively lower one(lower client's expectation)

**2. Formula for Basic EPS**: 
- Basic EPS = (NI - DIV_preferred stock) / Weighted average number of common share outstanding 
1. 判断并计算分母是关键 --- 四种情况
2. Weighted by time: **New issue**, **Repurchases**
3. Not weighted by time: **Stock split**, **Stock dividend**
4. 为什么要拆分股票？往往是因为最小交易单位是一手100股，当每股单价太高时，即使买一手总价也太贵，使得散户投资门槛过高。拆分不影响总市值。
5. Give weights based on the time, e.g. 1/1 --- 12/12, 2/1 --- 11/12
6. Repurchase: Minus, not plus (it's a liability)
7. Stock dividend: multiply all the PREVIOUS shares items by the 1+x
8. Stock split:  multiply all the PREVIOUS shares numbner by ratio

**3. Formula for Dilutive EPS (Complicated)**: 
- ADD some extra items  on both top and bottom of the Basic EPS
- For nominator: (1) Convertible preferred dividend (2) Convertible debt interest * (1 - tax rate)
- For denominator: (1) Shares from conversion of conv. pfd. shares (2) Shares from conversion of conv. debt (3) Shares issuable from options/warrants