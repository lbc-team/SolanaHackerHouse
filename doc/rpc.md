## RPC

https://docs.solana.com/api/http

### 示例

```js
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "getBalance",
  "params": [
    "83astBRguLMdt2h5U1Tpdq5tjFoJ6noeGwaY3mDLVcri"
  ]
}
```

对应的请求结果为：

```js
{
  "jsonrpc": "2.0",
  "result": {

  },
  "id": 1
}
```

在请求查询的时候，对查询的结果有三种状态选择：

- 'finalized' - 节点将查询由超过集群中超多数确认为达到最大封锁期的最新区块，表示集群已将此区块确认为已完成。
- 'confirmed' - 节点将查询由集群的超多数投票的最新区块。
- 'processed' - 节点将查询最新的区块。注意，该区块可能被集群跳过。

### 获取集群节点信息

```
curl https://api.devnet.solana.com -X POST -H "Content-Type: application/json" -d '
    {
      "jsonrpc": "2.0",
      "id": 1,
      "method": "getClusterNodes"
    }
  '
```

结果：

```js
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": [{
      "featureSet": 3712769919,
      "gossip": "57.128.73.26:25000",
      "pubkey": "FDQHfbqgSUk94XKFKWu6E8qidL7bwGEXDPzAoTVTXEDm",
      "pubsub": null,
      "rpc": null,
      "shredVersion": 38642,
      "tpu": "57.128.73.26:25003",
      "tpuQuic": "57.128.73.26:25009",
      "version": "1.16.8"
    },
    {
      "featureSet": 1879391783,
      "gossip": "34.133.16.61:8021",
      "pubkey": "6ZuobS4qns8od4DuSknAEuD7fuPwPrnheT87YqNhACR3",
      "pubsub": null,
      "rpc": null,
      "shredVersion": 38642,
      "tpu": null,
      "tpuQuic": null,
      "version": "1.14.18"
    },
    {
      "featureSet": 3712769919,
      "gossip": "3.95.133.231:8000",
      "pubkey": "3fgo2TkMaEu8rMLABpA7gg7KGp5XGTVdWYifeYqzsjkW",
      "pubsub": null,
      "rpc": null,
      "shredVersion": 38642,
      "tpu": "3.95.133.231:8003",
      "tpuQuic": "3.95.133.231:8009",
      "version": "1.16.8"
    }

  ]
}
```

### 获取当前区块高度

```
curl https://api.devnet.solana.com -X POST -H "Content-Type: application/json" -d '
    {
      "jsonrpc":"2.0","id":0,
      "method":"getBlockHeight"
    }
    '
```

结果：

```js
{"jsonrpc":"2.0","result":234889717,"id":0}
```

### 获取最近的 BlockHash

```
curl https://api.devnet.solana.com -X POST -H "Content-Type: application/json" -d '
    {
        "id":1,
        "jsonrpc":"2.0",
        "method":"getLatestBlockhash",
        "params":[
        {
            "commitment":"processed"
        }
        ]
    }
  '
```

结果：

```js
{
  "jsonrpc": "2.0",
  "id": 1
  "result": {
    "context": {
      "apiVersion": "1.16.11",
      "slot": 246574000
    },
    "value": {
      "blockhash": "7pbKBsJi5JxEWiRRxawXJQzEPU5JJRJ2ZzTBtqHZ8FMN",
      "lastValidBlockHeight": 234890201
    }
  }
}
```

### 获取指定高度 block 的信息

```
curl https://api.devnet.solana.com -X POST -H "Content-Type: application/json" -d '
    {
        "jsonrpc": "2.0","id":0,
        "method":"getBlock",
        "params": [
            246574000,
            {
                "encoding": "jsonParsed",
                "maxSupportedTransactionVersion":0,
                "transactionDetails":"full",
                "rewards":false
            }
        ]
    }
  '
```

结果：

```js
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "blockHeight": 234889802,
    "blockTime": 1695650622,
    "blockhash": "C53WVY6bAeHTknx6NszarZ5akQBgyvKWnoXvn7vnDaSV",
    "parentSlot": 246573999,
    "previousBlockhash": "yb9Zzg2sEDZLod6g6LpoX4sC9oah8gxBRMkMeTaE8do",
    "transactions": [{
      "meta": {
        "computeUnitsConsumed": 0,
        "err": null,
        "fee": 5000,
        "innerInstructions": [],
        "logMessages": [
          "Program Vote111111111111111111111111111111111111111 invoke [1]",
          "Program Vote111111111111111111111111111111111111111 success"
        ],
        "postBalances": [
          5692625905,
          50883432957,
          1
        ],
        "postTokenBalances": [],
        "preBalances": [
          5692630905,
          50883432957,
          1
        ],
        "preTokenBalances": [],
        "rewards": null,
        "status": {
          "Ok": null
        }
      },
      "transaction": {
        "message": {
          "accountKeys": [{
              "pubkey": "Gp9R3ts3j9Akhmvyky8WCrUYRVdUhzTyct4M4WXz937d",
              "signer": true,
              "source": "transaction",
              "writable": true
            },
            {
              "pubkey": "5iic7eCs3tGKQvscTaY3Lb8mr6HvogpZKoxgxazxdiCA",
              "signer": false,
              "source": "transaction",
              "writable": true
            },
            {
              "pubkey": "Vote111111111111111111111111111111111111111",
              "signer": false,
              "source": "transaction",
              "writable": false
            }
          ],
          "instructions": [{
            "parsed": {
              "info": {
                "voteAccount": "5iic7eCs3tGKQvscTaY3Lb8mr6HvogpZKoxgxazxdiCA",
                "voteAuthority": "Gp9R3ts3j9Akhmvyky8WCrUYRVdUhzTyct4M4WXz937d",
                "voteStateUpdate": {
                  "hash": "7rhvjZo1z5tqQkAkEhKdLke8axz7fDAY8ECfcJAAzJqo",
                  "lockouts": [{
                      "confirmation_count": 31,
                      "slot": 246573968
                    },
                    {
                      "confirmation_count": 30,
                      "slot": 246573969
                    },
                    {
                      "confirmation_count": 29,
                      "slot": 246573970
                    },
                    {
                      "confirmation_count": 28,
                      "slot": 246573971
                    },
                    {
                      "confirmation_count": 27,
                      "slot": 246573972
                    },
                    {
                      "confirmation_count": 26,
                      "slot": 246573973
                    },
                    {
                      "confirmation_count": 25,
                      "slot": 246573974
                    },
                    {
                      "confirmation_count": 24,
                      "slot": 246573975
                    },
                    {
                      "confirmation_count": 23,
                      "slot": 246573976
                    },
                    {
                      "confirmation_count": 22,
                      "slot": 246573977
                    },
                    {
                      "confirmation_count": 21,
                      "slot": 246573978
                    },
                    {
                      "confirmation_count": 20,
                      "slot": 246573979
                    },
                    {
                      "confirmation_count": 19,
                      "slot": 246573980
                    },
                    {
                      "confirmation_count": 18,
                      "slot": 246573981
                    },
                    {
                      "confirmation_count": 17,
                      "slot": 246573982
                    },
                    {
                      "confirmation_count": 16,
                      "slot": 246573983
                    },
                    {
                      "confirmation_count": 15,
                      "slot": 246573984
                    },
                    {
                      "confirmation_count": 14,
                      "slot": 246573985
                    },
                    {
                      "confirmation_count": 13,
                      "slot": 246573986
                    },
                    {
                      "confirmation_count": 12,
                      "slot": 246573987
                    },
                    {
                      "confirmation_count": 11,
                      "slot": 246573988
                    },
                    {
                      "confirmation_count": 10,
                      "slot": 246573989
                    },
                    {
                      "confirmation_count": 9,
                      "slot": 246573990
                    },
                    {
                      "confirmation_count": 8,
                      "slot": 246573991
                    },
                    {
                      "confirmation_count": 7,
                      "slot": 246573992
                    },
                    {
                      "confirmation_count": 6,
                      "slot": 246573993
                    },
                    {
                      "confirmation_count": 5,
                      "slot": 246573994
                    },
                    {
                      "confirmation_count": 4,
                      "slot": 246573995
                    },
                    {
                      "confirmation_count": 3,
                      "slot": 246573996
                    },
                    {
                      "confirmation_count": 2,
                      "slot": 246573997
                    },
                    {
                      "confirmation_count": 1,
                      "slot": 246573998
                    }
                  ],
                  "root": 246573967,
                  "timestamp": 1695650622
                }
              },
              "type": "compactupdatevotestate"
            },
            "program": "vote",
            "programId": "Vote111111111111111111111111111111111111111",
            "stackHeight": null
          }],
          "recentBlockhash": "7PbNoLFAnbYWauxiCFB5DeN55fRUkm9JGz3xtSKxEvUr"
        },
        "signatures": [
          "67GTNnjvRpFcajBhPZHb6dQvBXDAgDhRwy8ifqJRftX7rq8bHSbWHk8y8MSfihBeTmtFyhMWqhqrrPTDknsmwmMS"
        ]
      },
      "version": "legacy"
    }
    ...
  ]

  }
}
```

### 获取指定 block 的确认状态

```
curl https://api.devnet.solana.com -X POST -H "Content-Type: application/json" -d '
    {
        "jsonrpc": "2.0", "id": 0,
        "method": "getBlockCommitment",
        "params":[174302734]
    }
  '
```

结果：

```js
{"jsonrpc":"2.0","result":{"commitment":null,"totalStake":156171505106792315},"id":0}
```

### 一次性获取多个 block 的信息

```
curl https://api.devnet.solana.com -X POST -H "Content-Type: application/json" -d '
    {
        "jsonrpc": "2.0", "id": 0,
        "method": "getBlocks",
        "params": [
            174302734, 174302735
        ]
    }
  '
```

结果：

```js
{"jsonrpc":"2.0","result":[174302734,174302735],"id":0}
```

### 分页获取 block

```
curl https://api.devnet.solana.com -X POST -H "Content-Type: application/json" -d '
  {
    "jsonrpc": "2.0",
    "id":0,
    "method":"getBlocksWithLimit",
    "params":[174302734, 3]
  }
'
```

结果：

```js
{"jsonrpc":"2.0","result":[174302734,174302735,174302736],"id":0}
```

### 获取当前 Epoch 信息

```
curl https://api.devnet.solana.com -X POST -H "Content-Type: application/json" -d '
    {"jsonrpc":"2.0","id":0, "method":"getEpochInfo"}
    '
```

结果：

```js
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "absoluteSlot": 246575942,
    "blockHeight": 234891740,
    "epoch": 570,
    "slotIndex": 335942,
    "slotsInEpoch": 432000,
    "transactionCount": 12064372695
  },
}
```

### getEpochSchedule

获取 Epoch 的调度信息

```
curl https://api.devnet.solana.com -X POST -H "Content-Type: application/json" -d '
    {
        "jsonrpc":"2.0","id":0,
        "method":"getEpochSchedule"
    }
  '
```

结果：

```js
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "firstNormalEpoch": 0,
    "firstNormalSlot": 0,
    "leaderScheduleSlotOffset": 432000,
    "slotsPerEpoch": 432000,
    "warmup": false
  }
}
```

### 获取最新 Slot

```
curl https://api.devnet.solana.com -X POST -H "Content-Type: application/json" -d '
    {"jsonrpc":"2.0","id":0, "method":"getSlot"}
  '
```

结果：

```js
{"jsonrpc":"2.0","result":246576515,"id":0}
```

### 获取 Account 信息

通过 getAccountInfo RPC 请求来查看

```
curl https://api.devnet.solana.com -X POST -H "Content-Type: application/json" -d '
    {
        "jsonrpc": "2.0",
        "id": 1,
        "method": "getAccountInfo",
        "params": [
            "5pWae6RxD3zrYzBmPTMYo1LZ5vef3vfWH6iV3s8n6ZRG",
            {
                "encoding": "base58",
                "commitment": "finalized"
            }
        ]
    }
  '
```

结果：

```js
{
  "jsonrpc": "2.0",
  "result": {
    "context": {
      "apiVersion": "1.16.11",
      "slot": 246576668
    },
    "value": {
      "data": ["", "base58"],
      "executable": false,
      "lamports": 672674901240,
      "owner": "11111111111111111111111111111111",
      "rentEpoch": 0,
      "space": 0
    }
  },
  "id": 1
}
```

### 获取账号余额

```
curl https://api.devnet.solana.com -X POST -H "Content-Type: application/json" -d '
    {
        "jsonrpc": "2.0", "id": 1,
        "method": "getBalance",
        "params": [
            "5pWae6RxD3zrYzBmPTMYo1LZ5vef3vfWH6iV3s8n6ZRG"
        ]
    }
  '
```

结果：

```js
{
  "jsonrpc": "2.0",
  "result": {
    "context": {
      "apiVersion": "1.16.11",
      "slot": 246576885
    },
    "value": 672674901240
  },
  "id": 1
}
```

### 获取某个合约管理的所有 Account

```
curl  https://api.devnet.solana.com  -X POST -H "Content-Type: application/json" -d '
        {
            "jsonrpc": "2.0",
            "id": 1,
            "method": "getProgramAccounts",
            "params": [
            "namesLPneVptA9Z5rqUDD9tMTWEJwofgaYwp8cawRkX",
            {
                "encoding": "jsonParsed",
                "filters": [
                {
                    "dataSize": 128
                }
                ]
            }
            ]
        }
    '
```

结果：

```js
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": [{
    "account": {
      "data": [
        "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAGwk7Y137iow53XrTOM962Y2TVISoKMGL9mi9Y8u6DZQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA=",
        "base64"
      ],
      "executable": false,
      "lamports": 1781761,
      "owner": "namesLPneVptA9Z5rqUDD9tMTWEJwofgaYwp8cawRkX",
      "rentEpoch": 371,
      "space": 128
    },
    "pubkey": "Hhs9G3t3sUPMMFygrK9xmerVYk2dmaMieZAucfrzxc8v"
  }]
}
```

### getTokenAccountsByOwner

查询某个 Token 下，所有 owner 为某人的 Token 账号，或者 delegate 为某人的所有账号。

```
curl  https://api.devnet.solana.com -X POST -H "Content-Type: application/json" -d '
        {
            "jsonrpc": "2.0",
            "id": 1,
            "method": "getTokenAccountsByOwner",
            "params": [
            "Czorr4y9oFvE3VdfCLVFuKDYxaNUG1iyQomR7kMZUuzi",
            {
                "mint": "7vtXvye2ECB1T5Se8E1KebNfmV7t4VkaULDjf2v1xpA9"
            },
            {
                "encoding": "jsonParsed"
            }
            ]
        }
    '
```

结果：

```js
{
  "jsonrpc": "2.0",
  "result": {
    "context": {
      "apiVersion": "1.16.11",
      "slot": 246578586
    },
    "value": [{
      "account": {
        "data": {
          "parsed": {
            "info": {
              "isNative": false,
              "mint": "7vtXvye2ECB1T5Se8E1KebNfmV7t4VkaULDjf2v1xpA9",
              "owner": "Czorr4y9oFvE3VdfCLVFuKDYxaNUG1iyQomR7kMZUuzi",
              "state": "initialized",
              "tokenAmount": {
                "amount": "94000000000",
                "decimals": 9,
                "uiAmount": 94.0,
                "uiAmountString": "94"
              }
            },
            "type": "account"
          },
          "program": "spl-token",
          "space": 165
        },
        "executable": false,
        "lamports": 2039280,
        "owner": "TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA",
        "rentEpoch": 0,
        "space": 165
      },
      "pubkey": "EZhhUANUMKsRhRMArczio1kLc9axefTUAh5xofGX35AK"
    }]
  },
  "id": 1
}
```

### getTokenAccountsByDelegate

```
curl https://api.devnet.solana.com -X POST -H "Content-Type: application/json" -d '
    {
        "jsonrpc": "2.0",
        "id": 1,
        "method": "getTokenAccountsByDelegate",
        "params": [
        "Czorr4y9oFvE3VdfCLVFuKDYxaNUG1iyQomR7kMZUuzi",
        {
            "mint": "7vtXvye2ECB1T5Se8E1KebNfmV7t4VkaULDjf2v1xpA9"
        },
        {
            "encoding": "jsonParsed"
        }
        ]
    }
    '
```

结果：

```js
{
  "jsonrpc": "2.0",
  "result": {
    "context": {
      "apiVersion": "1.16.11",
      "slot": 246578813
    },
    "value": []
  },
  "id": 1
}
```

### 获取某个 Token Account 账号的余额

```
curl  https://api.devnet.solana.com  -X POST -H "Content-Type: application/json" -d '
        {
            "jsonrpc": "2.0", "id": 1,
            "method": "getTokenAccountBalance",
            "params": [
                "EZhhUANUMKsRhRMArczio1kLc9axefTUAh5xofGX35AK"
            ]
        }
    '
```

结果：

```js
{
  "jsonrpc": "2.0",
  "result": {
    "context": {
      "apiVersion": "1.16.11",
      "slot": 246578969
    },
    "value": {
      "amount": "94000000000",
      "decimals": 9,
      "uiAmount": 94.0,
      "uiAmountString": "94"
    }
  },
  "id": 1
}
```

### 获取交易手续费

```
curl https://api.devnet.solana.com -X POST -H "Content-Type: application/json" -d '
    {
        "id":1,
        "jsonrpc":"2.0",
        "method":"getFeeForMessage",
        "params":[
            "AQABAgIAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAEBAQAA",
            {
                "commitment":"processed"
            }
        ]
    }
    '
```

结果：

```js
{
  "jsonrpc": "2.0",
  "result": {
    "context": {
      "apiVersion": "1.16.11",
      "slot": 246579128
    },
    "value": null
  },
  "id": 1
}
```

### 获取交易详细信息

```
curl  https://api.devnet.solana.com  -X POST -H "Content-Type: application/json" -d '
        {
            "jsonrpc": "2.0",
            "id": 1,
            "method": "getTransaction",
            "params": [
                "2o9qCEhwKi8w7hTFQJTLwMBZPFH8qM3iNd9rprtdY6XShyrpsqkWt4Df3Zgsxv6y4nbRe4SDgU8KMvuMfs7HxVhp",
                "jsonParsed"
            ]
        }
    '
```

结果：

```js
{
  "jsonrpc": "2.0",
  "result": {
    "blockTime": 1674954447,
    "meta": {
      "computeUnitsConsumed": 12481,
      "err": null,
      "fee": 5000,
      "innerInstructions": [],
      "logMessages": ["Program gSbePebfvPy7tRqimPoVecS2UsBvYv46ynrzWocc92s invoke [1]", "Program gSbePebfvPy7tRqimPoVecS2UsBvYv46ynrzWocc92s consumed 2633 of 600000 compute units", "Program gSbePebfvPy7tRqimPoVecS2UsBvYv46ynrzWocc92s success", "Program gSbePebfvPy7tRqimPoVecS2UsBvYv46ynrzWocc92s invoke [1]", "Program gSbePebfvPy7tRqimPoVecS2UsBvYv46ynrzWocc92s consumed 5562 of 597367 compute units", "Program gSbePebfvPy7tRqimPoVecS2UsBvYv46ynrzWocc92s success", "Program gSbePebfvPy7tRqimPoVecS2UsBvYv46ynrzWocc92s invoke [1]", "Program gSbePebfvPy7tRqimPoVecS2UsBvYv46ynrzWocc92s consumed 4286 of 591805 compute units", "Program gSbePebfvPy7tRqimPoVecS2UsBvYv46ynrzWocc92s success"],
      "postBalances": [420164575000, 23942400, 23942400, 23942400, 1169280, 1141440],
      "postTokenBalances": [],
      "preBalances": [420164580000, 23942400, 23942400, 23942400, 1169280, 1141440],
      "preTokenBalances": [],
      "rewards": [],
      "status": {
        "Ok": null
      }
    },
    "slot": 192074782,
    "transaction": {
      "message": {
        "accountKeys": [{
          "pubkey": "vir55LvSEGcY55ny876GycLmFCxMXTkoRg7RxDvKiw5",
          "signer": true,
          "source": "transaction",
          "writable": true
        }, {
          "pubkey": "8PugCXTAHLM9kfLSQWe2njE5pzAgUdpPk3Nx5zSm7BD3",
          "signer": false,
          "source": "transaction",
          "writable": true
        }, {
          "pubkey": "EfnLcrwxCgwALc5vXr4cwPZMVcmotZAuqmHa8afG8zJe",
          "signer": false,
          "source": "transaction",
          "writable": true
        }, {
          "pubkey": "6Ukmvns6Uyf3nRVj3ErDBgx7BiZRNJrLyXe1nGQ7CUHA",
          "signer": false,
          "source": "transaction",
          "writable": true
        }, {
          "pubkey": "SysvarC1ock11111111111111111111111111111111",
          "signer": false,
          "source": "transaction",
          "writable": false
        }, {
          "pubkey": "gSbePebfvPy7tRqimPoVecS2UsBvYv46ynrzWocc92s",
          "signer": false,
          "source": "transaction",
          "writable": false
        }],
        "instructions": [{
          "accounts": ["vir55LvSEGcY55ny876GycLmFCxMXTkoRg7RxDvKiw5", "8PugCXTAHLM9kfLSQWe2njE5pzAgUdpPk3Nx5zSm7BD3", "SysvarC1ock11111111111111111111111111111111"],
          "data": "6mJFQCt94hG4CKNYKgVcwiF4v7AWo54Dz3XinKUG6Qm1DDhhmspAST",
          "programId": "gSbePebfvPy7tRqimPoVecS2UsBvYv46ynrzWocc92s",
          "stackHeight": null
        }, {
          "accounts": ["vir55LvSEGcY55ny876GycLmFCxMXTkoRg7RxDvKiw5", "EfnLcrwxCgwALc5vXr4cwPZMVcmotZAuqmHa8afG8zJe", "SysvarC1ock11111111111111111111111111111111"],
          "data": "6mJFQCt94hG4CKNYKgVcwigC7XswHjekyj7J1dQmjsHsoqHjydqXoV",
          "programId": "gSbePebfvPy7tRqimPoVecS2UsBvYv46ynrzWocc92s",
          "stackHeight": null
        }, {
          "accounts": ["vir55LvSEGcY55ny876GycLmFCxMXTkoRg7RxDvKiw5", "6Ukmvns6Uyf3nRVj3ErDBgx7BiZRNJrLyXe1nGQ7CUHA", "SysvarC1ock11111111111111111111111111111111"],
          "data": "6mJFQCt94hG4CKNYKgVcwcojsn834cy7vrPD6ksi4ri42uvkGeVMkb",
          "programId": "gSbePebfvPy7tRqimPoVecS2UsBvYv46ynrzWocc92s",
          "stackHeight": null
        }],
        "recentBlockhash": "sS5jHAvxaXfowtGCvg4dWc9QjzeZ1dJS5GonshyDsEq"
      },
      "signatures": ["2o9qCEhwKi8w7hTFQJTLwMBZPFH8qM3iNd9rprtdY6XShyrpsqkWt4Df3Zgsxv6y4nbRe4SDgU8KMvuMfs7HxVhp"]
    }
  },
  "id": 1
}
```
