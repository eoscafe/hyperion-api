# Hyperion HTTP API Javascript library

## Installation

Using Yarn:

    yarn add @jafri/hyperion

or using NPM:

    npm install --save @jafri/hyperion

## Quick Start

**CommonJS**

```js
const { JsonRpc } = require("@jafri/hyperion")
const fetch = require("isomorphic-fetch")

const endpoint = "https://br.eosrio.io"
const rpc = new JsonRpc(endpoint, { fetch })
```

**TypeScript**

```ts
import { JsonRpc } from "@jafri/hyperion"
import fetch from "isomorphic-fetch"

const endpoint = "https://br.eosrio.io"
const rpc = new JsonRpc(endpoint, { fetch })
```

## ENV Variables

```bash
HYPERION_ENDPOINT=<Enter Hyperion Endpoint>  # "https://br.eosrio.io"
```

## Supported Endpoints

    /v2/history/alive
    /v2/history/get_abi_snapshot
    /v2/history/get_actions
    /v2/history/get_creator
    /v2/history/get_key_accounts
    /v2/history/get_tokens
    /v2/history/get_transacted_accounts
    /v2/history/get_transaction
    /v2/history/get_transfers

## API

<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

#### Table of Contents

-   [JsonRpc](#jsonrpc)
    -   [Parameters](#parameters)
    -   [Examples](#examples)
    -   [alive](#alive)
        -   [Examples](#examples-1)
    -   [get_abi_snapshot](#get_abi_snapshot)
        -   [Parameters](#parameters-1)
        -   [Examples](#examples-2)
    -   [get_actions](#get_actions)
        -   [Parameters](#parameters-2)
        -   [Examples](#examples-3)
    -   [get_creator](#get_creator)
        -   [Parameters](#parameters-3)
        -   [Examples](#examples-4)
    -   [get_key_accounts](#get_key_accounts)
        -   [Parameters](#parameters-4)
        -   [Examples](#examples-5)
    -   [get_tokens](#get_tokens)
        -   [Parameters](#parameters-5)
        -   [Examples](#examples-6)
    -   [get_transacted_accounts](#get_transacted_accounts)
        -   [Parameters](#parameters-6)
        -   [Examples](#examples-7)
    -   [get_transaction](#get_transaction)
        -   [Parameters](#parameters-7)
        -   [Examples](#examples-8)
    -   [get_transfers](#get_transfers)
        -   [Parameters](#parameters-8)
        -   [Examples](#examples-9)
-   [JsonRpc](#jsonrpc-1)
    -   [alive](#alive-1)
        -   [Examples](#examples-10)
    -   [get_abi_snapshot](#get_abi_snapshot-1)
        -   [Parameters](#parameters-9)
        -   [Examples](#examples-11)
    -   [get_actions](#get_actions-1)
        -   [Parameters](#parameters-10)
        -   [Examples](#examples-12)
    -   [get_creator](#get_creator-1)
        -   [Parameters](#parameters-11)
        -   [Examples](#examples-13)
    -   [get_key_accounts](#get_key_accounts-1)
        -   [Parameters](#parameters-12)
        -   [Examples](#examples-14)
    -   [get_tokens](#get_tokens-1)
        -   [Parameters](#parameters-13)
        -   [Examples](#examples-15)
    -   [get_transacted_accounts](#get_transacted_accounts-1)
        -   [Parameters](#parameters-14)
        -   [Examples](#examples-16)
    -   [get_transaction](#get_transaction-1)
        -   [Parameters](#parameters-15)
        -   [Examples](#examples-17)
    -   [get_transfers](#get_transfers-1)
        -   [Parameters](#parameters-16)
        -   [Examples](#examples-18)
-   [Error](#error)
-   [Error](#error-1)

### JsonRpc

JsonRpc

#### Parameters

-   `endpoint` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** hyperion endpoint

#### Examples

```javascript
const endpoint = "https://br.eosrio.io"
const rpc = new JsonRpc(endpoint, { fetch })
```

#### alive

[GET /v2/history/alive](https://br.eosrio.io/v2/history/docs/index.html#/v2/get_v2_history_alive)

simple server healthcheck

##### Examples

```javascript
const response = await rpc.alive();
console.log(response);
// => {"status": "OK"}
```

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;Alive>** alive

#### get_abi_snapshot

[GET /v2/history/get_abi_snapshot](https://br.eosrio.io/v2/history/docs/index.html#/v2/get_v2_history_get_abi_snapshot)

fetch contract abi at specific block

##### Parameters

-   `contract` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** contract account
-   `block`  
-   `number` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** target block

##### Examples

```javascript
const response = await rpc.get_abi_snapshot("eosio", 200);
console.log(response.version);
// => "eosio::abi/1.0"

for (const table of response.tables) {
    console.log(table);
    // => { name: 'producers', index_type: 'i64', key_names: [ 'owner' ], key_types: [ 'uint64' ], type: 'producer_info' }
}
```

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;GetAbiSnapshot>** abi snapshot

#### get_actions

[GET /v2/history/get_actions](https://br.eosrio.io/v2/history/docs/index.html#/v2/get_v2_history_get_actions)

get actions based on notified account

##### Parameters

-   `account` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** notified account
-   `options` **[object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** Optional parameters (optional, default `{}`)
    -   `options.filter` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** code::name filter
    -   `options.skip` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)?** skip [n] actions (pagination)
    -   `options.limit` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)?** limit of [n] actions per page
    -   `options.sort` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** sort direction
    -   `options.after` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** filter after specified date (ISO8601)
    -   `options.before` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** filter before specified date (ISO8601)

##### Examples

```javascript
const response = await rpc.get_actions("eoscafeblock", {
    filter: "eosio.token:*",
    skip: 100,
    limit: 100,
});

for (const action of response.actions) {
    console.log(action);
    // => { act: { account: 'eosio.token', name: 'transfer', ... } }
}
```

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;GetActions>** get actions

#### get_creator

[GET /v2/history/get_creator](https://br.eosrio.io/v2/history/docs/index.html#/v2/get_v2_history_get_creator)

get account creator

##### Parameters

-   `account` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** created account

##### Examples

```javascript
const response = await rpc.get_creator("eosnationftw");
console.log(response);
// => { account: 'eosnationftw', creator: 'gyztcmrvgqge', timestamp: '2018-06-10T13:06:43.500', ... }
```

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;GetAccountCreator>** get creator

#### get_key_accounts

[GET/v2/history/get_key_accounts](https://br.eosrio.io/v2/history/docs/index.html#/v2/get_v2_history_get_key_accounts)

get account by public key

##### Parameters

-   `public_key` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** Contract account targeted by the action.

##### Examples

```javascript
const response = await rpc.get_key_accounts("EOS5Mto3Km6BCVxowb6LkkFaT9oaUwLVgswgcxvY4Qgc4rhHry4Tv");
console.log(response.account_names);
// => [ 'eoscafeblock' ]
```

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;GetKeyAccounts>** key accounts

#### get_tokens

[GET /v2/history/get_tokens](https://br.eosrio.io/v2/history/docs/index.html#/v2/get_v2_history_get_tokens)

get tokens

##### Parameters

-   `account` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** account

##### Examples

```javascript
const response = await rpc.get_tokens("eosnationftw");
for (const token of response.tokens) {
    console.log(token);
    // => { symbol: 'ZOS', precision: 4, amount: 140, contract: 'zosdiscounts' }
}
```

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;GetTokens>** get tokens

#### get_transacted_accounts

[GET /v2/history/get_transacted_accounts](https://br.eosrio.io/v2/history/docs/index.html#/v2/get_v2_history_get_transacted_accounts)

get all account that interacted with the source account provided

##### Parameters

-   `account` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** source account
-   `direction` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** search direction (in, out or both)
-   `options` **[object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** Optional parameters (optional, default `{}`)
    -   `options.symbol` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** token symbol
    -   `options.contract` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** token contract
    -   `options.min` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)?** minimum value
    -   `options.max` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)?** maximum value
    -   `options.limit` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)?** query limit

##### Examples

```javascript
const response = await rpc.get_transacted_accounts("eoscafeblock", "in");
console.log(response);
// => { query_time: 268, account: 'eoscafeblock', total_in: 1092369.1827, inputs: [ ... ] }
```

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;GetTransactedAccounts>** transacted accounts

#### get_transaction

[GET /v2/history/get_transaction](https://br.eosrio.io/v2/history/docs/index.html#/v2/get_v2_history_get_transaction)

get all actions belonging to the same transaction

##### Parameters

-   `id` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** transaction id

##### Examples

```javascript
const response = await rpc.get_transaction("42dacd5722001b734be46a2140917e06cd21d42425f927f506c07b4388b07f62");
for (const action of response.actions) {
    console.log(action);
    // => { act: { account: 'eosio', name: 'buyrambytes', ... }}
}
```

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;GetTransaction>** transaction

#### get_transfers

[GET /v2/history/get_transfers](https://br.eosrio.io/v2/history/docs/index.html#/v2/get_v2_history_get_transfers)

get token transfers utilizing the eosio.token standard

##### Parameters

-   `options` **[object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** Optional parameters (optional, default `{}`)
    -   `options.from` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** source account
    -   `options.to` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** destination account
    -   `options.symbol` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** token symbol
    -   `options.contract` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** token contract
    -   `options.after` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** filter after specified date (ISO8601)
    -   `options.before` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** filter before specified date (ISO8601)

##### Examples

```javascript
const response = await rpc.get_transfers({to: "eosnewyorkio"});
for (const action of response.actions) {
    console.log(action.act.data);
    // => { from: 'eosio.bpay', to: 'eosnewyorkio', amount: 326.524, symbol: 'EOS', memo: 'producer block pay' }
}
```

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;GetTransfers>** transfers

### JsonRpc

#### alive

[GET /v2/history/alive](https://br.eosrio.io/v2/history/docs/index.html#/v2/get_v2_history_alive)

simple server healthcheck

##### Examples

```javascript
const response = await rpc.alive();
console.log(response);
// => {"status": "OK"}
```

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;Alive>** alive

#### get_abi_snapshot

[GET /v2/history/get_abi_snapshot](https://br.eosrio.io/v2/history/docs/index.html#/v2/get_v2_history_get_abi_snapshot)

fetch contract abi at specific block

##### Parameters

-   `contract` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** contract account
-   `block`  
-   `number` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** target block

##### Examples

```javascript
const response = await rpc.get_abi_snapshot("eosio", 200);
console.log(response.version);
// => "eosio::abi/1.0"

for (const table of response.tables) {
    console.log(table);
    // => { name: 'producers', index_type: 'i64', key_names: [ 'owner' ], key_types: [ 'uint64' ], type: 'producer_info' }
}
```

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;GetAbiSnapshot>** abi snapshot

#### get_actions

[GET /v2/history/get_actions](https://br.eosrio.io/v2/history/docs/index.html#/v2/get_v2_history_get_actions)

get actions based on notified account

##### Parameters

-   `account` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** notified account
-   `options` **[object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** Optional parameters (optional, default `{}`)
    -   `options.filter` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** code::name filter
    -   `options.skip` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)?** skip [n] actions (pagination)
    -   `options.limit` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)?** limit of [n] actions per page
    -   `options.sort` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** sort direction
    -   `options.after` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** filter after specified date (ISO8601)
    -   `options.before` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** filter before specified date (ISO8601)

##### Examples

```javascript
const response = await rpc.get_actions("eoscafeblock", {
    filter: "eosio.token:*",
    skip: 100,
    limit: 100,
});

for (const action of response.actions) {
    console.log(action);
    // => { act: { account: 'eosio.token', name: 'transfer', ... } }
}
```

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;GetActions>** get actions

#### get_creator

[GET /v2/history/get_creator](https://br.eosrio.io/v2/history/docs/index.html#/v2/get_v2_history_get_creator)

get account creator

##### Parameters

-   `account` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** created account

##### Examples

```javascript
const response = await rpc.get_creator("eosnationftw");
console.log(response);
// => { account: 'eosnationftw', creator: 'gyztcmrvgqge', timestamp: '2018-06-10T13:06:43.500', ... }
```

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;GetAccountCreator>** get creator

#### get_key_accounts

[GET/v2/history/get_key_accounts](https://br.eosrio.io/v2/history/docs/index.html#/v2/get_v2_history_get_key_accounts)

get account by public key

##### Parameters

-   `public_key` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** Contract account targeted by the action.

##### Examples

```javascript
const response = await rpc.get_key_accounts("EOS5Mto3Km6BCVxowb6LkkFaT9oaUwLVgswgcxvY4Qgc4rhHry4Tv");
console.log(response.account_names);
// => [ 'eoscafeblock' ]
```

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;GetKeyAccounts>** key accounts

#### get_tokens

[GET /v2/history/get_tokens](https://br.eosrio.io/v2/history/docs/index.html#/v2/get_v2_history_get_tokens)

get tokens

##### Parameters

-   `account` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** account

##### Examples

```javascript
const response = await rpc.get_tokens("eosnationftw");
for (const token of response.tokens) {
    console.log(token);
    // => { symbol: 'ZOS', precision: 4, amount: 140, contract: 'zosdiscounts' }
}
```

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;GetTokens>** get tokens

#### get_transacted_accounts

[GET /v2/history/get_transacted_accounts](https://br.eosrio.io/v2/history/docs/index.html#/v2/get_v2_history_get_transacted_accounts)

get all account that interacted with the source account provided

##### Parameters

-   `account` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** source account
-   `direction` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** search direction (in, out or both)
-   `options` **[object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** Optional parameters (optional, default `{}`)
    -   `options.symbol` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** token symbol
    -   `options.contract` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** token contract
    -   `options.min` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)?** minimum value
    -   `options.max` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)?** maximum value
    -   `options.limit` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)?** query limit

##### Examples

```javascript
const response = await rpc.get_transacted_accounts("eoscafeblock", "in");
console.log(response);
// => { query_time: 268, account: 'eoscafeblock', total_in: 1092369.1827, inputs: [ ... ] }
```

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;GetTransactedAccounts>** transacted accounts

#### get_transaction

[GET /v2/history/get_transaction](https://br.eosrio.io/v2/history/docs/index.html#/v2/get_v2_history_get_transaction)

get all actions belonging to the same transaction

##### Parameters

-   `id` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** transaction id

##### Examples

```javascript
const response = await rpc.get_transaction("42dacd5722001b734be46a2140917e06cd21d42425f927f506c07b4388b07f62");
for (const action of response.actions) {
    console.log(action);
    // => { act: { account: 'eosio', name: 'buyrambytes', ... }}
}
```

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;GetTransaction>** transaction

#### get_transfers

[GET /v2/history/get_transfers](https://br.eosrio.io/v2/history/docs/index.html#/v2/get_v2_history_get_transfers)

get token transfers utilizing the eosio.token standard

##### Parameters

-   `options` **[object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** Optional parameters (optional, default `{}`)
    -   `options.from` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** source account
    -   `options.to` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** destination account
    -   `options.symbol` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** token symbol
    -   `options.contract` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** token contract
    -   `options.after` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** filter after specified date (ISO8601)
    -   `options.before` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** filter before specified date (ISO8601)

##### Examples

```javascript
const response = await rpc.get_transfers({to: "eosnewyorkio"});
for (const action of response.actions) {
    console.log(action.act.data);
    // => { from: 'eosio.bpay', to: 'eosnewyorkio', amount: 326.524, symbol: 'EOS', memo: 'producer block pay' }
}
```

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;GetTransfers>** transfers

### Error

### Error
