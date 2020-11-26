# ARISENJS Signature Provider for Ledger

## Overview
A SignatureProvider for communicating with [arisenjs](https://github.com/ARISEN/arisenjs) from a Ledger device.

When plugged into `arisenjs`, this signature provider enables applications to route signing requests to a Ledger device. Full instructions for `arisenjs` can be found [here](https://github.com/ARISEN/arisenjsv1).

## Installation

```bash
# Using yarn
yarn add arisenjs-ledger-signature-provider
```

## Usage

#### Example
```javascript
const { SignatureProvider } from 'arisenjs-ledger-signature-provider'

const signatureProvider = new SignatureProvider()

signatureProvider.getAvailableKeys()
  .then((result) => console.info('Keys: ', result))
  .catch((error) => console.info('Error: ', error))

const chainId = '000000000'
const serializedTransaction = {} // A transaction as a Uint8Array. View `serializeTransaction` in https://github.com/ARISEN/arisenjs/blob/develop/src/arisenjs-api.ts

signatureProvider.sign({ chainId, serializedTransaction })
  .then((result) => console.info('TransactionId: ', result))
  .catch((error) => console.info('Error: ', error))
```

#### Example with arisenjs
```javascript
const { Api, JsonRpc } from 'arisenjs'
const { SignatureProvider } from 'arisenjs-ledger-signature-provider'

const rpcEndpoint = 'https://localhost:3000'
const signatureProvider = new SignatureProvider()
const rpc = new JsonRpc(rpcEndpoint)
const api = new Api({ signatureProvider, rpc })

// arisenjs will call both `getAvailableKeys` and `sign` from the SignatureProvider
api.transact(...)
.then((result) => console.info('TransactionId: ', result))
.catch((error) => console.info('Error: ', error))
```

## Contribution
Check out the [Contributing](./CONTRIBUTING.md) guide

## License
[MIT licensed](./LICENSE)
