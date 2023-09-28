Covalent 是一个统一的 API，提供对可扩展历史区块链数据的快速可靠访问。 开发人员可以利用Covalent的API服务将分散的应用程序无缝部署到Scroll的Sepolia测试网上

## 测试网速览
Scroll正在构建一个完全等效EVM的通用zk-Rollup，目的是扩展以太坊网络。

| Chain name                 | `scroll-sepolia-testnet`                                                       |
| -------------------------- | ------------------------------------------------------------------------------ |
| Chain ID                   | `534351`                                                                       |
| Block explorer             | [https://sepolia-blockscout.scroll.io/](https://sepolia-blockscout.scroll.io/) |
| Blocktime                  | 60 seconds                                                                     |
| Historical balances        | ✅                                                                             |
| NFT assets and metadata    | ✅                                                                             |
| Query via SQL on Increment | ✅                                                                                |

## 网络状态

Covalent 提供日，周，月，年四个周期的活跃账户数，交易数量和活跃代币地址统计。
Scroll Sepolia 测试网主网在 2023 月 8 月 20 日拥有 20279 个每天都在进行交易的活跃钱包地址。

## 代码示例

### 获取地址的代币余额
通常用于获取地址持有的原生、ERC20和ERC721和ERC1155代币。响应包括现货价格和其他元数据。
https://api.covalenthq.com/v1/{chainName}/address/{walletAddress}/balances_v2/

### 获取地址的最近交易 （v3）
通常用于获取和呈现涉及地址的最新事务。常见于钱包应用程序中。
https://api.covalenthq.com/v1/{chainName}/address/{walletAddress}/transactions_v3/


### 获取一段时间内的历史投资组合价值
通常用于呈现按代币细分的地址的每日投资组合余额。时间范围是用户可配置的，默认为 30 天。
https://api.covalenthq.com/v1/{chainName}/address/{walletAddress}/portfolio_v2/


### 获取区块
通常用于为区块浏览器获取和渲染单个块
https://api.covalenthq.com/v1/{chainName}/block_v2/{blockHeight}/