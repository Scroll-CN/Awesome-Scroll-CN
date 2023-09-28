## 目标
构造并发送使 Scroll 证明器无法生成其证明的交易。

## Github Repo
- l2geth: [https://github.com/scroll-tech/go-ethereum](https://github.com/scroll-tech/go-ethereum)  
- circuits: [https://github.com/scroll-tech/zkevm-circuits](https://github.com/scroll-tech/zkevm-circuits)  
- circuits sepc: [https://github.com/scroll-tech/zkevm-specs/tree/master/specs](https://github.com/scroll-tech/zkevm-specs/tree/master/specs)  
- contracts: [https://github.com/scroll-tech/scroll/tree/develop/contracts](https://github.com/scroll-tech/scroll/tree/develop/contracts)

## Scroll 工作流概览

1. 打包区块：排序器（l2geth 签名器实例）从 L2 内存池和 L1（Rollup同步服务）收集交易，并将其打包到 L2 区块中。它还提供 p2p 和 RPC 访问，以便其他 l2geth 节点可以连接和同步链
2. 数据可用性：Rollup中继器收集 L2 区块（ l2getth 中的 API, eth_getBlockByHash），将它们打包成批次(Batches)并提交给 L1 Rollup合约
	1. https://github.com/scroll-tech/scroll/blob/develop/contracts/src/L1/rollup/ScrollChain.sol#L164
3. 生成证明：证明者接收批次，收集详细的踪迹(trace)（scroll_getBlockTraceByNumberOrHash l2getth 中的 API），并生成 ZK 证明。
	1. https://github.com/scroll-tech/go-ethereum/blob/develop/eth/tracers/api_blocktrace.go#L19
4. 最终确认：Rollup中继器验证证明并将其提交给 L1 Rollup 合约。


## 可能的漏洞原因

### l2geth 和 zkevm 电路的不一致

Scroll 交易证明首先通过在 l2geth EVM 中执行它来生成踪迹来建立的，然后Scroll 电路约束该踪迹步骤，无法证明交易中 geth EVM 和电路之间的任何不一致的行为。

例子：
evm 创建的 calldatasize 为 0，但电路将 calldatasize 作为 tx.data 长度进行处理
- [fix calldataload when tx.to = null by lispc · Pull Request #909 · scroll-tech/zkevm-circuits · GitHub](https://github.com/scroll-tech/zkevm-circuits/pull/909/files)

### 生成的踪迹中缺少信息

如果生成的踪迹中缺少电路验证所需的任何信息，则交易无法被证明。

踪迹生成逻辑：
[api\_blocktrace.go](https://github.com/scroll-tech/go-ethereum/blob/develop/eth/tracers/api_blocktrace.go#L19)

例子：
生成踪迹时，没有 tx.data 的交易将被归类为非合约调用，从而导致其代码从踪迹中排除。
因此，由于跟踪中缺少代码信息，因此无法证明合约回退调用事务。
- [fix(trace): fix contract call's \`ByteCode\` by mask-pp · Pull Request #465 · scroll-tech/go-ethereum · GitHub](https://github.com/scroll-tech/go-ethereum/pull/465)

### 绕过电路容量检查
由于电路容量有限，超过阈值的交易无法被证明。为了解决这个问题，Scroll 会启动交易的预执行，并生成踪迹。然后，它利用此踪迹来计算交易的容量使用情况。如果容量超过所摄的限制，则跳过执行和证明。

如果可以绕过电路溢出检查，则可以发送无法证明的tx。
- [worker.go](https://github.com/scroll-tech/go-ethereum/blob/develop/miner/worker.go#L875)

容量检查器
[capacity\_checker.rs](https://github.com/scroll-tech/zkevm-circuits/blob/develop/prover/src/zkevm/capacity_checker.rs)


### 处理 Geth 踪迹时总线映射 ( bus-mapping ) 出错
总线映射是一个设计用于解析 EVM 执行踪迹并操作所有数据的crate，如果总线映射无法解析某些操作码步骤或解析行为与 evm 不一致，也会导致交易无法被证明。

总线映射 ( bus-mapping ) ：
[bus-mapping](https://github.com/scroll-tech/zkevm-circuits/tree/develop/bus-mapping)


## RPC
发送交易至Scroll L2 测试网，而不是 sepolia 测试网。
[Site Unreachable](https://sepolia-rpc.scroll.io)

## 一些想法
- 存储冲突
- 代码哈希模糊（Scroll Geth使用波塞冬计算代码哈希进行电路证明，如果L2Geth和电路的哈希实现之间存在差异，则交易变得无法证明）。
- 短地址攻击 https://medium.com/golem-project/how-to-find-10m-by-just-reading-blockchain-6ae9d39fcd95
- 代理调用预编译合约
- 预编译合约 Revert
- is_code检查错误（确定操作码片段是代码还是数据）
- 1/64 CALL gas减少 https://medium.com/iovlabs-innovation-stories/the-dark-side-of-ethereum-1-64th-call-gas-reduction-ba661778568c
- [EIP-2929: Gas cost increases for state access opcodes](https://eips.ethereum.org/EIPS/eip-2929)

## 奖励

Scroll的交易（区块）有三种确认状态：“Precommitted”、“Committed”和“Finalized”。

Precommitted 表示交易已由排序器确认，Committed 表示交易字节已提交到 L1，Finalized 表示交易的证明已经正确生成并在 L1 得到验证。

成功发送无法被最终确认的交易被视为实现了Bounty目标并有资格获得赏金。

验证流程：
1. 在 https://scroll.io/rollupscan 打开Rollup浏览器，搜索包含已发送交易的区块。
2. 检查交易的批处理状态。如果即使在提交 2 小时后仍无法确认交易，则可能无法正确生成证明。
3. 联系 Scroll 团队成员提供交易哈希和相关信息，来确认交易是否是批处理(Batches)未被最终确认的原因。

对于确定的每个无法证明的交易类型，将提供 5,000 美元的奖励。重复提交同一类型将没有资格获得额外奖励。如果两个人发现相同的漏洞类型，奖励将授予第一个提交交易的人。

如果在l2geth和合约中发现任何其他导致资金损失的漏洞（gas掉期除外），奖励将根据受影响的资金确定，最高奖励为100,000美元。

## 资格限制

现有员工（包括Contractor）、供应商（审计公司）、合作伙伴没有资格参与漏洞赏金计划。

## 联系方式

加入以下小组，联系Scroll 工作人员以获取测试ETH并提交报告。

Telegram: [https://t.me/+XmC8N1u8oQ80NTlh](https://t.me/+XmC8N1u8oQ80NTlh)
微信：