
3 月 31 日至 4 月 2 日，在这个为期 3 天的活动中，我们将 ZK Hack 社区的成员聚集在一起，试验并构建一些很酷的基于 zk 的应用程序！
Scroll 为部署在Scroll上的应用提供了总计 5000 美元的赏金，

# Fruity Friends
![](fruity_friends.png)
第一名是由[@guelord_](https://twitter.com/guelowrd)和[@madztheo](https://twitter.com/madztheo)一起构建的名为 Fruity Friends 的项目。它解决了在不愿意透露自己兴趣的情况下，如何匹配据有共同兴趣的双方。Fruity Friends 的解决方案是通过检查交集的大小是否大于 0。
隐私集合交集的文献表明最实用的方案是引入第三方来检查交集。具体来说，爱丽丝和鲍勃是需要匹配的双方，史蒂夫是负责检查的第三方。首先让爱丽丝和鲍勃就史蒂夫不知道的秘密达成一致。他们使用这个秘密作为盐值来对他们集合中的每个项目做哈希。然后他们将经过哈希处理的集合传递给史蒂夫。由于爱丽丝和鲍勃的盐值相同，因此相同的项目将产生相同的哈希。史蒂夫将能够分辨出它们是否相同但不会知道这些物品到底是什么。这在一定程度上解决了问题。
另一个需要解决的问题是，史蒂夫可以决定将爱丽丝的哈希处理后的集合发送给拥有相同秘密的鲍勃，然后鲍勃可以推断出爱丽丝的集合内容，因为可能的元素列表很可能是已知的并且大小有限。更好的解决方案可能是使用同态加密和/或多方计算，但是可能过于复杂超出了本次黑客松的范围。

- Devfolio: https://devfolio.co/projects/fruity-friends-ef88
- Demo: https://zk-fruits-front-end.vercel.app/
- Github：https://github.com/madztheo/zk-fruits-noir-project
- 合约地址：https://blockscout.scroll.io/address/0x3a7249aBcb0F9353cD75E1381d4D73dEB50b1467/transactions#address-tabs


# ZK-ZK-zk-EVM

由@MattWy337构建的ZK-ZK-zk-EVM，以获得第二名。其在Scroll 构建了 Aztec Connet，使得Scroll 拥有了自己的隐私结算层。

Scroll 是唯一可以支持 Aztec Connect 隐私层的 ZK-EVM，因为它支持字节码级别，也就是支持预编译（AC 重度依赖于此）。我们认为，在 2023 年的 zkEVM 大战中，这是 Scroll 的 ZKEVM 相对于其他 zkEVM 的巨大价值支柱。

- Devfolio: https://devfolio.co/projects/zkzkzkevm-493c
- Github: https://github.com/mwyatt896/aztec-connect-sc