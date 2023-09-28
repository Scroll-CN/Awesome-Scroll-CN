Pyth提供各种资产类别的实时定价数据，包括加密货币，股票，外汇和商品。此库允许您在基于 EVM 的网络上使用这些实时价格。
合约地址：`0xA2aa501b19aff244D90cc15a4Cf739D2725B5729`
https://sepolia-blockscout.scroll.io/address/0xA2aa501b19aff244D90cc15a4Cf739D2725B5729
价格对ID列表：
https://pyth.network/developers/price-feed-ids#pyth-evm-testnet

## 安装
### npm
```
$ npm install --save @pythnetwork/pyth-evm-js
```
### Yarn
```
$ yarn add @pythnetwork/pyth-evm-js
```

## 快速入门
Pyth 将价格存储在链下，以最大限度地降低 gas 费用，这使我们能够提供更广泛的产品选择和更快的更新时间。有关此方法的详细信息，请参阅按需更新。为了在链上使用 Pyth 价格，必须从链下价格服务中获取它们。该 `EvmPriceServiceConnection` 类可用于与这些服务交互，从而提供了一种直接在代码中获取这些价格的方法。以下示例包装了现有的 RPC 提供程序，并演示如何获取 Pyth 价格并将其提交到网络
```
const connection = new EvmPriceServiceConnection(
  "https://xc-testnet.pyth.network"
); // See Price Service endpoints section below for other endpoints

const priceIds = [
  // You can find the ids of prices at https://pyth.network/developers/price-feed-ids#pyth-evm-testnet
  "0xf9c0172ba10dfa4d19088d94f5bf61d3b54d5bd7483a322a982e1373ee8ea31b", // BTC/USD price id in testnet
  "0xca80ba6dc32e08d06f1aa886011eed1d77c77be9eb761cc10d72b7d0a2fd57a6", // ETH/USD price id in testnet
];

// In order to use Pyth prices in your protocol you need to submit the price update data to Pyth contract in your target
// chain. `getPriceFeedsUpdateData` creates the update data which can be submitted to your contract. Then your contract should
// call the Pyth Contract with this data.
const priceUpdateData = await connection.getPriceFeedsUpdateData(priceIds);

// If the user is paying the price update fee, you need to fetch it from the Pyth contract.
// Please refer to https://docs.pyth.network/documentation/pythnet-price-feeds/on-demand#fees for more information.
//
// `pythContract` below is a web3.js contract; if you wish to use ethers, you need to change it accordingly.
// You can find the Pyth interface ABI in @pythnetwork/pyth-sdk-solidity npm package.
const updateFee = await pythContract.methods
  .getUpdateFee(priceUpdateData)
  .call();
// Calling someContract method
// `someContract` below is a web3.js contract; if you wish to use ethers, you need to change it accordingly.
await someContract.methods
  .doSomething(someArg, otherArg, priceUpdateData)
  .send({ value: updateFee });
```

`SomeContract` 类似于如下合约

```
pragma solidity ^0.8.0;

import "@pythnetwork/pyth-sdk-solidity/IPyth.sol";
import "@pythnetwork/pyth-sdk-solidity/PythStructs.sol";

contract SomeContract {
  IPyth pyth;

  constructor(address pythContract) {
    pyth = IPyth(pythContract);
  }

  function doSomething(
    uint someArg,
    string memory otherArg,
    bytes[] calldata priceUpdateData
  ) public payable {
    // Update the prices to be set to the latest values
    uint fee = pyth.getUpdateFee(priceUpdateData);
    pyth.updatePriceFeeds{ value: fee }(priceUpdateData);

    // Doing other things that uses prices
    bytes32 priceId = 0xf9c0172ba10dfa4d19088d94f5bf61d3b54d5bd7483a322a982e1373ee8ea31b;
    PythStructs.Price price = pyth.getPrice(priceId);
  }
}
```

### 链下价格

许多应用程序还需要在链下显示 Pyth 价格，例如，在其前端应用程序中。提供了 `EvmPriceServiceConnection` 两种不同的方法来获取当前的 Pyth 价格。下面的代码块假定 `connection` 和 `priceIds` 对象已初始化，如上所示。第一种方法是单次查询：

```
// `getLatestPriceFeeds` returns a `PriceFeed` for each price id. It contains all information about a price and has
// utility functions to get the current and exponentially-weighted moving average price, and other functionality.
const priceFeeds = await connection.getLatestPriceFeeds(priceIds);
// Get the price if it is not older than 60 seconds from the current time.
console.log(priceFeeds[0].getPriceNoOlderThan(60)); // Price { conf: '1234', expo: -8, price: '12345678' }
// Get the exponentially-weighted moving average price if it is not older than 60 seconds from the current time.
console.log(priceFeeds[1].getEmaPriceNoOlderThan(60));
```

该对象还支持流式 websocket 连接，允许您订阅给定源的每个新价格更新。如果您想在前端显示不断更新的实时价格，此方法很有用：

```
// Subscribe to the price feeds given by `priceId`. The callback will be invoked every time the requested feed
// gets a price update.
connection.subscribePriceFeedUpdates(priceIds, (priceFeed) => {
  console.log(
    `Received update for ${priceFeed.id}: ${priceFeed.getPriceNoOlderThan(60)}`
  );
});

// When using the subscription, make sure to close the websocket upon termination to finish the process gracefully.
setTimeout(() => {
  connection.closeWebSocket();
}, 60000);
```

### 例子
#### Evm价格服务客户端
此示例使用 HTTP 请求 API 和流式 websocket API 获取 `PriceFeed` 更新。您可以使用 运行 `npm run example-client` 它。在测试网网络中打印BTC和ETH价格馈送的完整命令如下所示：

```
npm run example-client -- --endpoint https://xc-testnet.pyth.network --price-ids 0xf9c0172ba10dfa4d19088d94f5bf61d3b54d5bd7483a322a982e1373ee8ea31b 0xca80ba6dc32e08d06f1aa886011eed1d77c77be9eb761cc10d72b7d0a2fd57a6
```

#### EvmRelay
此示例说明如何更新 EVM 网络上的价格。它执行以下操作
1. 获取更新数据以更新给定的价格馈送。
2. 使用更新数据调用 pyth 协定。
3. 将其提交到网络，如果成功，则打印 txhash。
您可以使用 运行 `npm run example-relay` 此示例。