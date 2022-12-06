# 交易所 EVT 集成方案

## 一. 介绍

### 1. EVT是什么

### 2. EVT vs NFT

### 3. 应用场景

电影、音乐、元宇宙道具、元宇宙虚拟形象等

## 二. 总体架构

![evt-infrastructure](../res/evt-infrastructure.png)

总体架构介绍

## 二. 方案集成

![huobi_evt](../res/huobi_evt.png)

- 流程图优化 @Minter
- `NewKeeper` 接入文档 @Alen
- `NewPlayer` 接入文档 @Pony, @James, @Ouli
- 解析 tokenUri demo @wangyifan
- 媒体资源格式说明文档,   @Alen, @Minter,
- 文档格式优化  @Jude, @Damon

### 1. 业务流程

#### EVT 合约发行

由 EVT-Core 联合资源方发行 EVT， 上传至 IPFS, 同时创建 EVT Contact，由合作方同步资源信息至合作方 CDN


#### Mint EVT

由 EVT-Core Mint 一定数量的 EVT 到交易所的 NEW 地址。


#### 维护 EVT 播放列表

由交易所维护 EVT 播放列表


#### 用户购买 EVT

由交易所在平台购买 `EVT`,交易所服务中心化记账。


#### 用户播放 EVT

用户请求交易所服务器进行播放，先有交易所服务器鉴权，通过之后，交易所服务器到 `NewKeeper` 请求播放密钥,请求成功之后，
将密钥和播放链接返回交易所客户端，客户端将播放内容设置到 `NewPlayer` 进行播放观看。

### 2. 接入示例

- 如何解析EVT合约
  - 解析 tokenUri demo @wangyifan
  - 媒体资源格式说明文档,   @Alen, @Minter,

- `NewKeeper` 接入文档 @Alen
  - 步骤
  - Demo

## 三. NewKeepr API（具体API说明）

## 四. NewPlayer SDK

- [Android-sdk & demo](https://gitlab.weinvent.org/wave/business/wave-websites/evt-player-android)
- [iOS-sdk & demo](https://gitlab.weinvent.org/wave/business/wave-websites/evt-player-ios)

## 五. EVT-lib

## 六. 更新记录

## 七. 引用