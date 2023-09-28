在ETHDenver的Devtopia舞台上，Scroll的联合创始人Haichen Shen发表了主题为 Scroll 构建 zkEVM 和 zk Rollup 的挑战的演讲，并同步了最新 Alpha 测试网的情况。

![](img/Scroll%20测试网的最新进展-1.png)

Scroll是一个 EVM 等效的zk-Rollup以太坊扩容方案
![](img/Scroll%20测试网的最新进展-2.png)


在演讲最开始，Haichen强调了Scroll一直以来的原则，一是社区驱动的方式同社区开放构建，二是确保安全性和稳定的版本发布，三是强调证明者和排序器去中心化的重要性
![](img/Scroll%20测试网的最新进展-3.png)

以下是对开发zkEVM的社区贡献者，其中大多数来自于Scroll团队和PSE团队，还有一些其他的社区成员。
![](img/Scroll%20测试网的最新进展-4.png)

对于2月27日，Scroll 在 Goerli 上最新上线的 Alpha 测试网。目前是已经是 EVM 等效的，证明已经可以在 Goerli 测试网上验证。
![](img/Scroll%20测试网的最新进展-5.png)

而 Alpha 测试网的发布，意味着 Scroll 已经达到了路线图的第三阶段。
![](img/Scroll%20测试网的最新进展-6.png)
下一步就是第四阶段：zkEVM的主网上线。
![](img/Scroll%20测试网的最新进展-15.png)
对于社区关心的距离主网上线的进度，Haichen 公布了目前阶段需要完成的任务，首先是要构建完整的zkEVM 电路，目前还缺少一些不常见的错误约束，也还需要添加一些预编译合约。随后会进行zkEVM电路和跨链桥合约的审计，然后进行最后的优化。
![](img/Scroll%20测试网的最新进展-16.png)




演讲的后半部分，Haichen 分享了 Scroll 在构建 zkEVM 和 zkRollup 过程中遇到的挑战。主要从三个方面来说，第一是编写zk电路，第二是编写zkEVM，第三是构建zk-Rollup。
![](img/Scroll%20测试网的最新进展-7.png)
![](img/Scroll%20测试网的最新进展-8.png)

在编写zk电路中，主要有两个难点。其一是开发的逻辑，正常程序中根据输入x，y，函数foo得到输出z，在zk电路中，则是根据输入x，y，foo(x,y)，输出是否有效的判断，因此在zk电路中需要考虑到有效和无效的所有情况，确保电路的约束成立。
![](img/Scroll%20测试网的最新进展-9.png)

其二是有限域的操作，是包含有限个元素的域，这些元素通常是素数。在所用的BN-254曲线中为254位的值，因此要表示EVM的256位，需要拆解成两部分。
![](img/Scroll%20测试网的最新进展-10.png)

在编写zkEVM中，Haichen 拆解了zk和EVM。在EVM中有三个组成部分，Executor, Stack, Memory。
![](img/Scroll%20测试网的最新进展-11.png)
zk部分将需要对EVM的执行过程中进行一一的约束。EVM电路将约束Executor正确执行过程；RAM电路将约束Stack，Memory的读写正确；Bytecode电路将约束EVM读取的bytecode的正确性；MPT电路将约束存储的读写正确；TX电路将约束交易的有效性；ECDSA电路将约束交易中签名的正确性；Keccak电路则将约束Keccak哈希函数的正确计算；还有其他的一些约束等等。所有这些的约束组合在一起，就组成了zkEVM。
![](img/Scroll%20测试网的最新进展-12.png)

在构建zk-Rollup方面，去中心化证明者网络需要对证明者进行激励。
![](img/Scroll%20测试网的最新进展-13.png)
当后续去中心化排序器后，情况会变得更复杂，需要协调证明者网络和排序器网络，目前Scroll 正在进行开放研究，欢迎有想法的开发者加入研究探讨。
![](img/Scroll%20测试网的最新进展-14.png)
![](img/Scroll%20测试网的最新进展-18.png)

对于想要体验 Scroll 的 Alpha测试网的用户，需要寻求帮助的用户，以及想要加入 Scroll 的小伙伴，可以分别扫描下方的 Testnet, Discord, Hiring 二维码。
- Testnet: https://scroll.io/alpha
- Discord: https://discord.com/invite/scroll
- Hiring: https://scroll.io/join-us
![](img/Scroll%20测试网的最新进展-17.png)
