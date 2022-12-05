# 火币 EVT 方案

![huobi_evt](../res/huobi_evt.png)

- 流程图优化 @Minter
- `NewKeeper` 接入文档 @Alen
- `NewPlayer` 接入文档 @Pony, @James, @Ouli
- 解析 tokenUri demo @wangyifan
- 媒体资源格式说明文档,   @Alen, @Minter,
- 文档格式优化  @Jude, @Damon

## EVT 合约发行

由 EVT-Core 联合资源方发行 EVT， 上传至 IPFS, 同时创建 EVT Contact，由合作方同步资源信息至合作方 CDN


## Mint EVT

由 EVT-Core Mint 一定数量的 EVT 到合作方(火币)的 NEW 地址。


## 维护 EVT 播放列表

由合作方(火币)维护 EVT 播放列表


## 用户购买 EVT

合作方用户(火币)在平台购买 `EVT`,合作方(火币)服务中心化记账。


## 用户播放 EVT

用户请求合作方(火币)服务器进行播放，先有合作方(火币)服务器鉴权，通过之后，合作方(火币)服务器到 `NewKeeper` 请求播放密钥,请求成功之后，
将密钥和播放链接返回合作方(火币)客户端，客户端将播放内容设置到 `NewPlayer` 进行播放观看。