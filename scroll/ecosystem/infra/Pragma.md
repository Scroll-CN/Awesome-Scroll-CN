![](img/pragma_banner.png)

Pragma是去中心化，透明和可组合的预言机网络，利用最先进的零知识密码学，与最大的做市商和最具流动性的交易所合作，根据他们签署的高质量、强大的数据并为其加盖时间戳，并将其直接发送到链上。

你可以在此处找到Scroll Alpha 测试网支持的资产列表。当前的 Pragma Network 地址是：

|网络|地址|浏览器|
|---|---|---|
|Scroll Alpha 测试网|0xbb91Ed469258069Ff2590CA11E1800DE05Bf6Ec7|[浏览器](https://blockscout.scroll.io/address/0xbb91Ed469258069Ff2590CA11E1800DE05Bf6Ec7)|

# 技术规范
## 结构体
### `BaseEntry`

```
struct BaseEntry {        
	uint256 timestamp;        
	bytes32 source;        
	bytes32 publisher;    
}
```

基本要素，包括发布时间、数据来源和数据发布者。

### `SpotEntry`

```
struct SpotEntry {        
	BaseEntry base;        
	bytes32 pairId;        
	uint256 price;        
	uint256 volume;    
}
```

现货结构，包括基本条目以及有关资产对的现货价格的各种信息（现货对id，例如ETH/USD及其相关价格和交易量）

### `SpotEntryStorage`

```
struct SpotEntryStorage {        
	uint128 timestamp;        
	bytes16 pairId;        
	uint128 price;        
	uint128 volume;    
}
```

现货存储结构，其中包含有关特定来源的资产对的不同信息：时间戳、现货对Id、价格和数量。

## 方法

### `getSpot`
此函数会将所选来源的所有数据聚合为给定现货对 ID 的中位数值

- **输入**
	- `pairId`：要获取中位数的现货对的 ID (bytes32)。
	- `sources`：用于聚合的数据源列表（bytes32 列表）。
 - **返回值**
	- `price`：给定pair_id的所有选定源的聚合结果，基于中值算法（uint256）。乘以`10**decimals`. 
	-  `decimals`：该值已移动的位数，以实现更高的精度 (uint256)。 
	- `lastUpdatedTimestamp`：最近聚合条目的时间戳 (uint256)。
	- `numSourcesAggregated`：最终结果中的来源数量。应当对应于输入源列表的长度 (uint256)。


### `getSpotEntries`

此函数将从选定的数据源中检索给定现货对 ID 的最新条目。根据时间戳选择条目；但是，当前时间戳与发布时间戳之间最多只能存在一小时的差异。

- **输入**
	- `pairId`：要获取中位数的现货对的 ID (bytes32)。
	- `sources`：用于聚合的数据源列表（bytes32 列表）。
 - **返回值**
	- `entries`：条目列表，给定输入现货对Id和来源。每个条目都是一个`SpotEntryStorage`
	- `lastUpdatedTimestamp`：最近聚合条目的时间戳 (uint256)。