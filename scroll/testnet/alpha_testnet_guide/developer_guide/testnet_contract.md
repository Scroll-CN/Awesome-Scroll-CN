# Alpha测试网合约

## 网络信息

| 网络名字 | Goerli 测试网                                                         | Scroll Alpha 测试网                  |
| -------- | ---------------------------------------------------------------------- | --------------------------------- |
| RPC URL  | https://endpoints.omniatech.io/v1/eth/goerli/public | https://alpha-rpc.scroll.io/l2 |
| Chain ID | 5                                                                 | 534353                            |
| 代币符号 | ETH                                  | ETH                     |
| 区块链浏览器   |     https://goerli.etherscan.io/                                                                  |      https://blockscout.scroll.io/                          |


## Scroll 合约

### Rollup
- L1 Rollup: `0x3C584eC7f0f2764CC715ac3180Ae9828465E9833`

### 跨链桥
-   L1 Messenger: `0x5260e38080BFe97e6C4925d9209eCc5f964373b6`
-   L1 Gateway Router: `0xe5E30E7c24e4dFcb281A682562E53154C15D3332`
-   L2 Messenger: `0xb75d7e84517e1504C151B270255B087Fd746D34C`
-   L2 Gateway Router: `0x6d79Aa2e4Fbf80CF8543Ad97e294861853fb0649`

### L2 预部署合约

-   Message Queue: `0x5300000000000000000000000000000000000000`
-   Block Container: `0x5300000000000000000000000000000000000001`
-   Gas Price Oracle: `0x5300000000000000000000000000000000000002`
-   Whitelist: `0x5300000000000000000000000000000000000003`
-   WETH L2: `0x5300000000000000000000000000000000000004`
-   Transaction Fee Vault: `0x5300000000000000000000000000000000000005`


## 协议

### Uniswap V3

- 前端网页: [https://uniswap-v3.scroll.io/](https://uniswap-v3.scroll.io/)

- 核心合约
	- Core Factory: `0x1A6427f912D7F28E69612bF6f929E2b389F6691d`
	- NFT Position Manager: `0xa76cCE552d0B010AdC43c1ba11FC62Ee6544F65f`
	- Router: `0x111690A4468ba9b57d08280b2166AFf2bAC65248`
-   其他合约    
	- multicall2Address: `0xF6CB7D5783bfCB2e5622f9eB6D505116De193887`
	- proxyAdminAddress: `0x120Fc90ee2443b7936De720B05e58Cd5aF2514C4`
	- tickLensAddress: `0x98b25433c945cC23Ace8Bf8efc31B7a09b4Af946`
	- nftDescriptorLibraryAddressV1_3_0: `0x1d420BB5674Faaf0F14b6F23650bf616AE2d32b9`
	- nonfungibleTokenPositionDescriptorAddressV1_3_0: `0x5989F08f81C489D3E7e4A797d5D35De059f7c75c`
	- descriptorProxyAddress: `0x72eDCB712Db47851A608535954702461162C7a4B`
	- v3MigratorAddress: `0x87d91da448a77870Fc42783dbE57D1c6B9321A2D`
	- v3StakerAddress: `0xDA25ef37b15db8B8c3f669eA0F7a886DEb02dcd5`
	- quoterV2Address: `0x747e3E3668bD5E036E4524380B5B1d6d1B62Fdb8`