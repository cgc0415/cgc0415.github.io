---
title: 文件校验和（Hash）的计算
date: 2018-10-20 11:45:08
tags: 小工具
---

# 1、Windows系统

## 工具名：certutil --Windows内置的Hash计算工具

## 用法：certutil -hashfile pathToFileToCheck  [HashAlgorithm]

## 参数说明

### pathToFileToCheck -待计算校验和的文件

### HashAlgorithm - Hash算法，目前该工具有以下几种选项：MD2 MD4 MD5 SHA1 SHA256 SHA384 SHA512

###  示例：
{% asset_img calcfilehash.png pic:CalcFileHash 553 78 %}

# 2、Linux系统

## md5sum 等命令