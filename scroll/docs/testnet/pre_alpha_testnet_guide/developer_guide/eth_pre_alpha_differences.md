# 以太坊和Pre-Alpha测试网区别

以太坊主网的 EVM 和 Scroll 修改设计的 zkEVM 之间存在许多技术细节差异。你可以在如下看到现在存在的这些差异。

对于开源贡献者和基础设施建设者，请联系我们的团队以获得更多支持。

{% hint style="info" %}
对于一般的 Solidity 开发者来说，这些细节不会影响你的开发体验。
{% endhint %}

## EVM 操作码

| Opcode                      | Solidity Equivalent | Ethereum                                                                                   | Scroll                                  |
| --------------------------- | ------------------- | ------------------------------------------------------------------------------------------ | --------------------------------------- |
| `BLOCKHASH`                 | `block.blockhash`   | **输入：** 从栈顶开始的`blocknumber`，有效范围\[`NUMBER -256`, `NUMBER-1`] **输出：** 给定区块的哈希，如果不在有效范围内，返回0 | 匹配以太坊,但限制输入范围的`blocknumber`为`NUMBER -1` |
| `COINBASE`                  | `block.coinbase`    | 在以太坊 Clique 中，是签名者的以太坊地址                                                                   | 目前匹配以太坊，将变更为指向一个预部署的费用池合约               |
| `DIFFICULTY` / `PREVRANDAO` | `block.difficulty`  | PoS后，为前一个区块的 `random` 值                                                                    | 返回0                                     |
| `SELFDESTRUCT`              | `selfdestruct`      | 计划作废，并用 `SENDALL` 替换                                                                       | 在排序器中禁用，未来会采用以太坊的方案                     |

## State Account

### Additional Fields

我们将在当前`StateAccount`对象中添加两个字段：`PoseidonCodehash`和`CodeSize`。

```typescript
type StateAccount struct {
	Nonce    uint64
	Balance  *big.Int
	Root     common.Hash // merkle root of the storage trie
	KeccakCodeHash []byte // still the Keccak codehash
	// added fields
	PoseidonCodeHash []byte // the Poseidon codehash
	CodeSize uint64
}
```

### Codehash

与此相关，我们为每个合约字节码维护两种类型的代码哈希：Keccak 哈希和 Poseidon 哈希。

保留 `KeccakCodeHash` 是为了保持`EXTCODEHASH` 的兼容性，`PoseidonCodeHash`用于验证 zkEVM 中加载的字节码的正确性，因为Poseiden 哈希效率更高。

### Code Size

验证时 `EXTCODESIZE`，将整个合约数据加载到 zkEVM 中是代价很大。相反，我们在合约创建期间将合约大小存储在存储中。这样，我们就不需要加载代码——存储证明足以验证这个操作码。

## Block Time

Pre-Alpha 测试网的目标是恒定的 3 秒出块时间。这比理想情况下以太坊的 12 秒更短且更一致。

选择 3 秒的出块时间有两个原因：

* 更快、更稳定的出块时间可以带来更快的反馈和更好的用户体验
* 当我们优化测试网中的 zkEVM 电路时，即使我们保持每个区块或batch的较小的Gas上限时，我们仍然可以达到比以太坊更高的吞吐量。

## 未来的 EIPs

我们密切关注所有以太坊采用的新EIP，并将在合适的时候采用它们。如果你对更多细节感兴趣，请访问[我们的社区论坛](https://community.scroll.io)或[Discord](https://discord.gg/scroll)。
