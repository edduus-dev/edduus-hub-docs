This is sub-document of Edduus Hub documentation. For the reference, please refer to the [parent document](README.md).

# Hub-Js Documentation

## Installation

Using npm:

```bash
npm i git+ssh://github.com/edduus-dev/hub-js.git
```

## Usage

### Import library

```javascript
const hub = require('@edduus/hub-js')
```

### Generate mnemonic

```javascript
let mnemonic = hub.generateMnemonic()
```

### Derive account

```javascript
let dummyMnemonic =
  'human salon off check jealous delay mechanic intact gravity hunt dust giggle diamond drift south napkin mouse evoke sample athlete wreck silver summer device'
let account = hub.deriveAccount(dummyMnemonic)
```

### Construct Transaction

```javascript
let tx = hub.constructTransaction(
  account.address, // sender
  'cosmos14fxm9fhxwms84w06ekqqy45rva7trwn7wc3u4q', // receiver
  10, // amount
  10, // fee
  200000, // gas price
  'send with Edduuss', // memo
  6, // account number
  2 // account sequence
)
```

### Sign Transaction

```javascript
let signedTx = hub.signTransaction(tx, account.privateKey)
```

## Examples

### Construct transaction, and send with curl

Note: It is assumed your Edduus Hub REST client is running on `http://localhost:1317`

```javascript
const hub = require('@edduus/hub-js')
let util = require('util')

let account = hub.deriveAccount(
  'human salon off check jealous delay mechanic intact gravity hunt dust giggle diamond drift south napkin mouse evoke sample athlete wreck silver summer device'
)

let tx = hub.constructTransaction(
  account.address,
  'cosmos14fxm9fhxwms84w06ekqqy45rva7trwn7wc3u4q',
  10,
  10,
  200000,
  'send with Edduuss',
  6,
  2
)
let signedTx = hub.signTransaction(tx, account.privateKey)

console.log(
  util.inspect(JSON.stringify(signedTx), { showHidden: false, depth: null })
)
```

Now, you can use REST client to broadcast signed transaction

```bash
curl -XPOST -s http://localhost:1317/txs --data-binary '{"tx":{"msg":[{"type":"cosmos-sdk/MsgSend","value":{"amount":[{"amount":"10","denom":"edtoken"}],"from_address":"cosmos1quyw6ew2mvj9y5q47fd8v9s6agd4pp4tq4jt24","to_address":"cosmos14fxm9fhxwms84w06ekqqy45rva7trwn7wc3u4q"}}],"fee":{"amount":[{"amount":"10","denom":"edtoken"}],"gas":"200000"},"signatures":[{"signature":"Urd6i5OoMbAG3N0JdGrmh0O7tqnt3sNfUHzHQ+clnURANDYusBArTttHZKRgYxJxk1ZXRmNdqlmHkJcVFdqH/Q==","pub_key":{"type":"tendermint/PubKeySecp256k1","value":"AvvIBNLbDXF2eD+0AfC4Oc2XAggPMpIaUPjuar8btqP7"}}],"memo":"send with Edduuss"},"mode":"sync"}'
```

## Development

### Run tests

```bash
npm run test
```
