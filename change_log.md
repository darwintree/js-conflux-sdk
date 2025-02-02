# change log

## v1.7.2
* Add `balance` key in the result of `estimateGasAndCollateralAdvance` as the balance of `options.from`.

## v1.7.1

* Add method `checkBalanceAgainstTransaction`, and `estimateGasAndCollateralAdvance` to better estimate gas and check balance.

## v1.6.15

* Add `blockNumber` to block related methods `cfx_getBlockByHash`, `cfx_getBlockByEpochNumber`, `cfx_getBlockByHashWithPivotAssumption` which need `Conflux-rust v1.1.5` or above.
* Add one new RPC method `cfx_getBlockByBlockNubmer`

## v1.6.10
* `format.bytes` now only support hex string, will not accept non hex utf-8 string
* Add cli `cfxjs` which can random generate a `0x1 prefix ethereum` address
* `Conflux` add a new method `getEpochReceiptsByPivotBlockHash`

## v1.6.9
* Support `keepAlive` option in `Conflux` initialization.
* Add one util method `tracesInTree` to return a tree structure traces.
* Fix contract method override bug.
* Add a address utility method `shortenCfxAddress`.

## v1.6.3
* Support `retry` option in `Conflux` initialization.
* Add pending transaction status enum `CONST.PENDING_TX_STATUS` currently have two value: `FUTURE_NONCE` `NOT_ENOUGH_CASH`

## v1.6.2
* Optimize the address convert performance.

## v1.6.1
* `Conflux` add method `getAccountPendingTransactions` to get one account's pending transaction.
* Split API documents into several files, which is easy to read.

## v1.6.0
This version is corresponding to conflux-rust v1.1.3, check it's [changelog](https://github.com/Conflux-Chain/conflux-rust/blob/master/changelogs/CHANGELOG-1.1.x.md#113) for detailed info.

* `format.address` will respect `networkId`, `verbose` flag even if the first parameter is an CIP37 address.
* Add support for a standard token contract through `Conflux.CRC20`
* `cfx_getLogs` filter option add one more field `offset`
* Add one RPC method `cfx_getAccountPendingInfo` to get account's transaction pending info
* `epochs` pubsub now accept one parameter `subscription_epoch` the supported values are `latest_mined` \(default\) and `latest_state`
* Include `blockHash`, `epochHash`, `epochNumber`, `transactionHash`, and `transactionPosition` for trace RPCs
* When ABI encoding `bytes-N` type, if the data's length is not enough, will auto pad \(right\) to `N`

## v1.5.13
* `getStatus` method rethurn three new fields `latestState`, `latestConfirmed`, `latestCheckpoint`
* add two `trace` related rpc `traceTransaction`, `traceFilter`
* add one debug rpc `getEpochReceipts`
* add two provider wrapper `wrapEthereum`, `wrapConflux` to work with metamask

Notice: this is an update corresponding `conflux-rust v1.1.2`

## v1.5.10
* `Conflux`'s option can pass `networkId` now, and add a new method `updateNetworkId` to sync networkId from RPC.
* `format.address` will return new CIP37 addresses, if you pass a hex address, `networkId` should also be passed as second parameter
* add new method `format.hexAddress` to format hex address
* Wallet's constructor add a parameter `networkId`
* PrivateKeyAccount `constructor`, `decrypt`, `random` need one more parameter `networkId`
* `Transaction`, `Message` `sign` method need one more parameter `networkId`
* Conflux's get methods will return new address, and same to contract method returned address.
* `getSupplyInfo` response add new field `totalCirculating`
* `getStatus` response add new field `networkId`

## v1.1.7
* Add RPC method `traceBlock`  to `Conflux` which can used to get block's execution trace

## v1.1.6
* export `Contract`

  ```text
  // nodejs
  const { Contract } = require('js-conflux-sdk');
  ```

```text
import { Contract } from 'js-conflux-sdk'
```

## v1.1.5
* add `stateMutability` for method from abi

```text
console.log(contract.symbol.stateMutability) // "view"
console.log(contract.transfer.stateMutability) // "nonpayable"
```

* rename EventLog.params to EventLog.arguments

  \`\`\`

  await conflux.contract.Transfer\(null, null, null\).getLogs\({

  fromEpoch: 2868400,

  toEpoch: 2868500,

  }\)

/ _\[ { data: '0x0000000000000000000000000000000000000000000000000001184b321b4e44', topics: \[ '0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef', '0x0000000000000000000000001dc05200485776b79f195a1e617dbccb6826f1c4', '0x000000000000000000000000882c4ddb1d3210b5ae778360729c04cd3242df70' \], ... arguments: NamedTuple\(from,to,value\)\(3\) \[ '0x1dc05200485776b79f195a1e617dbccb6826f1c4', '0x882c4ddb1d3210b5ae778360729c04cd3242df70', 308186218974788n \] } \]_ /

```text
* add `subscribeLogs` for EventLog
```

subscription = await contract.Transfer\(null, null, null\).subscribeLogs\(\);

subscription.on\('data', data =&gt; { console.log\(data\); }\);

```text
* contract decode constructor data with out bytecode 

## v1.1.4

* add `conflux.getSupplyInfo`

## v1.1.3

* WebsocketProvider with Websocket options
```

new Conflux\({ url: 'ws://127.0.0.1', clientConfig: { maxReceivedFrameSize: 10_1000_1000, // 10 MB } }\)

```text
## v1.1.2

* add `conflux.getVoteList`

* add `conflux.getDepositList`

* update `conflux.getTransactionReceipt`

## v1.1.1

fix: update request id avoid repeat
```

// old conflux.provider.requestId\(\); // "16055917399420726"

// new conflux.provider.requestId\(\); // "175d4b91862001f4f81eb443"

```text
## v1.1.0

fix: use native websocket for front-end

* use BigInt for nodejs, JSBI for browser
```

// for nodejs

// old conflux.getBalance\(ADDRESS\); // JSBI\(1\) \[ -1153374696, sign: false \]

// new conflux.getBalance\(ADDRESS\); // 3141592600n

```text
## v1.0.1

fix: EventCoder, FunctionCoder, valueCoder decode return string but not JSBI

## v1.0.0

* add `defaultGasRatio` and `defaultStorageRatio`
```

conflux = new Conflux\({ defaultGasRatio: 1.1, defaultStorageRatio: 1.1, ... }\)

```text
* add `BaseAccount` and `PrivateKeyAccount`

Account `signTransaction` and `signMessage` to be `async`

* add wallet

wallet use for create and manage `Account` by address
```

account = conflux.wallet.addRandom\(\) console.log\(conflux.wallet.has\(account.address\)\); // true

account = conflux.wallet.addPrivateKey\(PRIVATE\_KEY\) console.log\(conflux.wallet.has\(account.address\)\); // true

account = conflux.wallet.addKeystore\(keystore, password\) console.log\(conflux.wallet.has\(account.address\)\); // true

```text
wallet use for sendTransaction
```

// old account = conflux.Account\(PRIVATE\_KEY\);

conflux.sendTransaction\({ from: account.address, // address will call `cfx_sendTranscion` ... }\)

conflux.sendTransaction\({ from: account, // must be instance of `Account` to sign by sdk and call `cfx_sendRawTransaction` ... }\)

```text

```

// new conflux.sendTransaction\({ from: address, // if address not in `conflux.wallet`, call `cfx_sendTranscion` ... }\)

account = conflux.wallet.addPrivate\(PRIVATE\_KEY\);

conflux.sendTransaction\({ from: account.address, // if account in `conflux.wallet`, sign by account and call `cfx_sendRawTransaction` ... }\)

conflux.sendTransaction\({ from: account, // same as `from: account.address`, but some user think input account instance with privateKey is unsafe ... }\)

```text
* add Subscription
```

await conflux.subscribe\(name, ...args\); // =&gt; id await conflux.subscribeEpochs\(\); // =&gt; Subscription with event 'data' await conflux.subscribeNewHeads\(\); // =&gt; Subscription with event 'data' await conflux.subscribeLogs\(\); // =&gt; Subscription with event 'data', 'revert' await conflux.unsubscribe\(id\); // =&gt; boolean await conflux.unsubscribe\(subscription\); // =&gt; boolean

```text
* add internal contract
```

contract = conflux.InternalContract\('AdminControl'\); console.log\(contract\);

contract = conflux.InternalContract\('SponsorWhitelistControl'\); console.log\(contract\);

contract = conflux.InternalContract\('Staking'\); console.log\(contract\);

```text
* add checksum address
```

// old conflux.getBalance\('0x1B716c51381e76900EBAA7999A488511A4E1fD0a'\); // ok conflux.getBalance\('0x1B716c51381e76900EBAA7999A488511A4E1fD0A'\); // ok

// new conflux.getBalance\('0x1B716c51381e76900EBAA7999A488511A4E1fD0a'\); // ok conflux.getBalance\('0x1B716c51381e76900EBAA7999A488511A4E1fD0A'\); // Error\('address checksum error'\)

```text
* `providerFactory` only accept first argument as override options
```

// old provider = providerFactory\('[http://localhost:12537](http://localhost:12537)'\)

// new provider = providerFactory\({ url: '[http://localhost:12537](http://localhost:12537)' }\)

```text
* add batch request
```

provider = providerFactory\({ url: '[http://localhost:12537](http://localhost:12537)' }\)

array = await provider.batch\(\[ { method: 'cfx\_epochNumber' }, { method: 'cfx\_getBalance', params: \['0x0123456789012345678901234567890123456789'\] }, \]\) / _\[ '0x1381', '0x0', \]_ /

```text
* add WebSocketProvider
```

provider = providerFactory\({ url: 'ws://localhost:12535' }\)

provider.close\(\); // user need to close before process ternimal

```text
* BaseProvider instanceof EventEmitter
```

const EventEmitter = require\('events'\);

// old console.log\(new BaseProvider\(\) instanceof EventEmitter\); // false console.log\(new HttpProvider\(\) instanceof EventEmitter\); // false

// new console.log\(new BaseProvider\({}\) instanceof EventEmitter\); // true console.log\(new HttpProvider\({}\) instanceof EventEmitter\); // true console.log\(new WebSocketProvider\({}\) instanceof EventEmitter\); // true

```text
* add CONST
```

const { CONST } = require\('js-conflux-sdk'\);

console.log\(CONST.EPOCH\_NUMBER\)

/ _{ LATEST\_MINED: 'latest\_mined', LATEST\_STATE: 'latest\_state', LATEST\_CONFIRMED: 'latest\_confirmed', LATEST\_CHECKPOINT: 'latest\_checkpoint', EARLIEST: 'earliest' }_ /

```text
* export `format` and `sign` without `util`
```

// old const { util: {format, sign} } = require\('js-conflux-sdk'\);

// new const { format, sign } = require\('js-conflux-sdk'\);

```text
* add `Drip` to replace unit
```

// old const { util } = require\('js-conflux-sdk'\);

const balance = await conflux.getBalance\(ADDRESS\); console.log\(util.unit.fromDripToCFX\(balance\)\)

// new const { Drip } = require\('js-conflux-sdk'\);

const balance = await conflux.getBalance\(ADDRESS\); console.log\(Drip\(balance\).toCFX\(\)\)

```text
for input, use `Drip.fromXXX` to get drip number string
```

// old const { util } = require\('js-conflux-sdk'\);

const tx = { to: ADDRESS, value: util.unit.fromCFXToDrip\(0.1\), ... }

// new const { Drip } = require\('js-conflux-sdk'\);

const tx = { to: ADDRESS, value: Drip.fromCFX\(0.1\), ... }

```text
* include all method from conflux JSON_RPC document

[JSON_RPC](https://developer.conflux-chain.org/docs/conflux-doc/docs/json_rpc) 

* friendly example code

example will guide user to use SDK step by step

* charming code organization

split abi coder with types

split contract method, event and override

## v0.13.4

* rename `send_transaction` to `cfx_sendTransaction`

## v0.13.3

* Account.encrypt returned address drop '0x' prefix

## v0.13.2

* use scrypt-js

## v0.13.1

* RPC returned all number as hex

* fix `sendTransaction`, `call`, `estimateGasAndCollateral` shallow copy `options`

## v0.13.0

* `Account.decrypt` required keystoreV3 object as input, and put `password` as second parameter
```

// old Account.decrypt\('password', {salt:..., iv:..., cipher:..., mac:...}\)

// new Account.decrypt\({ version: 3, id: '0bb47ee0-aac3-a006-2717-03877afa15f0', address: '0x1cad0b19bb29d4674531d6f115237e16afce377c', crypto: { ciphertext: 'a8ec41d2440311ce897bacb6f7942f3235113fa17c4ae6732e032336038a8f73', cipherparams: { iv: '85b5e092c1c32129e3d27df8c581514d' }, cipher: 'aes-128-ctr', kdf: 'scrypt', kdfparams: { dklen: 32, salt: 'b662f09bdf6751ac599219732609dceac430bc0629a7906eaa1451555f051ebc', n: 8192, r: 8, p: 1 }, mac: 'cc89df7ef6c27d284526a65cabf8e5042cdf1ec1aa4ee36dcf65b965fa34843d' } }, 'password'\)

```text
* `Account.prototype.encrypt` returned keystoreV3 format object
```

const account = new Account\('0x0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef'\);

// old account.encrypt\('password'\) / _{ algorithm: 'aes-128-ctr', N: 8192, r: 8, p: 1, dkLen: 32, salt: '0xb662f09bdf6751ac599219732609dceac430bc0629a7906eaa1451555f051ebc', iv: '0x85b5e092c1c32129e3d27df8c581514d', cipher: '0xa8ec41d2440311ce897bacb6f7942f3235113fa17c4ae6732e032336038a8f73', mac: '0xcc89df7ef6c27d284526a65cabf8e5042cdf1ec1aa4ee36dcf65b965fa34843d' }_ /

// new account.encrypt\('password'\) / _{ version: 3, id: '0bb47ee0-aac3-a006-2717-03877afa15f0', address: '0x1cad0b19bb29d4674531d6f115237e16afce377c', crypto: { ciphertext: 'a8ec41d2440311ce897bacb6f7942f3235113fa17c4ae6732e032336038a8f73', cipherparams: { iv: '85b5e092c1c32129e3d27df8c581514d' }, cipher: 'aes-128-ctr', kdf: 'scrypt', kdfparams: { dklen: 32, salt: 'b662f09bdf6751ac599219732609dceac430bc0629a7906eaa1451555f051ebc', n: 8192, r: 8, p: 1 }, mac: 'cc89df7ef6c27d284526a65cabf8e5042cdf1ec1aa4ee36dcf65b965fa34843d' } }_ /

```text
* epochNumber accept `earliest`, `latest_checkpoint`, `latest_confirmed` label

## v0.12.0

* add `getAdmin`
```

await cfx.getAdmin\('0x89996a8aefb2228593aae723d47f9517eef1341d'\) // "0x1be45681ac6c53d5a40475f7526bac1fe7590fb8"

```text
* sendTransaction accept privateKey as `from`
```

cfx.sendTransaction\({ from: PRIVATE\_KEY, // accept Account instance or privateKey to: ADDRESS, // accept Account instance or address ..., }\)

```text
* create Account accept address
```

new Account\(PRIVATE\_KEY\); // {privateKey:'0x...', publicKey: '0x...', address: '0x...'} new Account\(PUBLIC\_KEY\); // {publicKey: '0x...', address: '0x...'} new Account\(ADDRESS\); // {address: '0x...'}

```text
## v0.11.0

* defaultGasPrice, only use for sendTransaction
```

cfx = new Conflux\({ url: '[http://testnet-jsonrpc.conflux-chain.org:12537](http://testnet-jsonrpc.conflux-chain.org:12537)', defaultGasPrice: 100, }\)

// old cfx.call\({ address: '0x...', data: '0x...', }\); // =&gt; cfx\_call{defaultGasPrice:'0x64',address:'0x...',data:'0x...'}

// new cfx.call\({ address: '0x...', data: '0x...', }\); // =&gt; cfx\_call{address:'0x...',data:'0x...'}

```text
* remove defaultEpoch, defaultChainId, defaultGas, defaultStorageLimit
```

// old cfx = new Conflux\({ url: '[http://testnet-jsonrpc.conflux-chain.org:12537](http://testnet-jsonrpc.conflux-chain.org:12537)', defaultEpoch: 'latest\_state', defaultChainId: 1, defaultGasPrice: 100, defaultGas: 10, defaultStorageLimit: 1, }\)

// new cfx = new Conflux\({ url: '[http://testnet-jsonrpc.conflux-chain.org:12537](http://testnet-jsonrpc.conflux-chain.org:12537)', defaultGasPrice: 100, }\)

// user could `epochNumber` and `chainId` manual on each method.

```text
## v0.10.3

* fix broken sourcemap

## v0.10.2

* fix: include crypto into browserify build
```

// old ConfluxJSSDK.util.sign.randomPrivateKey\(\) // TypeError randomBytes is not a function

```text
## v0.10.1

* add format.bytes
```

format.bytes\('abcd'\); //  format.bytes\(\[0, 1, 2, 3\]\); // 

```text
* add contract method & event type or signature indexes
```

// solidity function override\(bytes memory str\) public function override\(string memory str\) public

```text

```

contract.override\('str'\); // Error: can not determine override

contract\['override\(string\)'\]\('str'\); // specify override method by type contract\['0x227ffd52'\]\('str'\); // specify override method by signature

```text
## v0.10.0-alpha

* add `getStatus`
```

cfx.getStatus\(\)

```text
* remove `getRiskCoefficient` and replace with `getConfirmationRiskByHash`
```

// old cfx.getRiskCoefficient\(epochNumber\)

// new cfx.getConfirmationRiskByHash\(blockHash\)

```text
* remove `getAccount` cause it's internal RPC.

* use `require` replace `import` to gen code.

## v0.9.2

* add defaultStorageLimit and defaultChainId for Conflux
```

// old const cfx = new Conflux\({ url: '[http://localhost:8000](http://localhost:8000)', defaultGasPrice: 100, defaultGas: 100000, }\)

// new const cfx = new Conflux\({ url: '[http://localhost:8000](http://localhost:8000)', defaultGasPrice: 100, defaultGas: 100000, defaultStorageLimit: 4096, defaultChainId: 0, }\)

```text
## v0.9.1

* abi implicitly converting string to number

solidity method: `function add(uint,uint) public returns (uint);`
```

// old await contract.add\(1, '2'\); // error! can not accept string

// new version await contract.add\(1, '2'\); // good, converting string to number

```text
## v0.9.0-beta

* format nonce as JSBI.BigInt
```

nonce = await cfx.getNextNonce\(...\)

// old 100000

// new JSBI.BigInt\(100000\)

```text
* format transaction fields
```

tx = await cfx.getTransactionByHash\(txHash\) // old { storageLimit: "0x64", chainId: "0x0", epochHeight: "0x400", ... }

// new { storageLimit: JSBI.BigInt\(100\), // JSBI chainId: 0, epochHeight: 1024, ... }

```text
* unit return string
```

// old unit.fromCFXToGDrip\(123\) =&gt; JSBI.BigInt\(123000000000\) unit.fromCFXToGDrip\('0.1234567891'\) =&gt; Error\('Cannot convert JSBI.BigInt'\)

// new unit.fromCFXToGDrip\(123\) =&gt; "123000000000" unit.fromCFXToGDrip\('0.1234567891'\) =&gt; "123456789.1"

```text
* contract fields "code" rename to "bytecode"
```

// old cfx.Contract\({code, abi, address}\)

// new cfx.Contract\({bytecode, abi, address}\)

```text
* abi decodeData and decodeLog return object
```

result = contract.abi.decodeData\('0x....'\)

// old \["Tom", JSBI.BigInt\(18\)\]

// new { name: 'func' fullName: 'func\(string name, uint age\)', type: 'func\(string,uint\)', signature: '0x812600df', array: \["Tom", JSBI.BigInt\(18\)\], object: { name: "Tom", age: JSBI.BigInt\(18\), } }

\`\`\`

