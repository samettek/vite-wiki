---
sidebarDepth: 4
---

# Subscribe
:::tip 维护者
[viteLiz](https://github.com/viteLiz)
:::

事件订阅相关接口。Vite提供两种事件订阅模式：轮询模式和长连接模式。

轮询模式先创建`filter`，然后通过`filterId`轮询`subscribe_getFilterChanges`接口，获取新事件。轮询模式如果超过5分钟没有请求则自动关闭这个`filterId`，也可以通过`subscribe_uninstallFilter`接口主动取消订阅。

长连接模式先注册一个`subscription`，然后当产生新事件时`subscription`会通过回调的方式返回新事件。长连接断开时自动取消订阅。

当前支持5种类型的事件：新快照（即新快照块）事件、新交易（即新账户块）事件、单个账户的新交易（即新账户块）事件、单个账户的新在途事件、新日志（即新账户块中的日志）事件。每一种类型的事件都包含相应的回滚事件，回滚时，事件消息中的removed字段为true。

## 使用说明

### 长连接模式订阅日志

先注册一个`subscription`，例如订阅`vite_f48f811a1800d9bde268e3d2eacdc4b4f8b9110e017bd7a76f`地址的日志事件。
```bash
// method填subscribe_subscribe，params的第一个参数为方法名，第二个参数开始为方法参数。
{"jsonrpc": "2.0","id": 1,"method": "subscribe_subscribe","params": ["newLogs", {"addrRange":{"vite_f48f811a1800d9bde268e3d2eacdc4b4f8b9110e017bd7a76f":{"fromHeight":"0","toHeight":"0"}}}]}
// 注册成功后返回订阅id 0x4b97e0674a5ebef942dbb07709c4a608。
{"jsonrpc": "2.0","id": 1,"result": "0x4b97e0674a5ebef942dbb07709c4a608"}
```
订阅成功后，产生新事件时自动回调。
```bash
// 返回值中的subscription为订阅id，result为事件内容
{"jsonrpc":"2.0","method":"subscribe_subscription","params":{"subscription":"0x4b97e0674a5ebef942dbb07709c4a608","result":[{"log":{"topics":["aa65281f5df4b4bd3c71f2ba25905b907205fce0809a816ef8e04b4d496a85bb","000000000000000000000000bb6ad02107a4422d6a324fd2e3707ad53cfed935"],"data":"AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAo="},"accountBlockHash":"23ea04b0dea4b9d0aa4d1f84b246b298a30faba753fa48303ad2deb29cd27f40","addr":"vite_f48f811a1800d9bde268e3d2eacdc4b4f8b9110e017bd7a76f","removed":false}]}}
```
长连接模式订阅无需取消订阅，断开连接时会自动取消。

### 轮询模式订阅日志

先创建一个`filter`。
```bash
// method和其他RPC接口一样，填"模块名_方法名"，params填方法参数。
{
	"jsonrpc": "2.0",
	"id": 1,
	"method": "subscribe_newLogsFilter",
	"params": [{
      "addrRange":{
        "vite_f48f811a1800d9bde268e3d2eacdc4b4f8b9110e017bd7a76f":{"fromHeight":"0","toHeight":"0"}
      }
		}]
}
// 订阅成功后返回filterId
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": "0x61d780619649fb0872e1f94a40cec713"
}
```
按一定的时间间隔用`filterId`轮询新事件。
```bash
// params填filterId
{
	"jsonrpc": "2.0",
	"id": 2,
	"method": "subscribe_getFilterChanges",
	"params": ["0x61d780619649fb0872e1f94a40cec713"]
}
// 根据订阅类型，返回对应格式的数据，返回的数据是上一次查询之后发生的新事件
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": {
        "result": [
            {
                "log": {
                    "topics": [
                        "96a65b1cd08da045d0318cafda7b8c8436092851d5a4b7e75054c005a296e3fb",
                        "0000000000000000000000ab24ef68b84e642c0ddca06beec81c9acb1977bb00"
                    ],
                    "data": "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAHsAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAN4Lazp2QAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAF"
                },
                "accountBlockHash": "802b82821ec52bdadb8b79a53363bf2f90645caef95a83c34af20c640a6c320b",
                "accountHeight": "10",
                "addr": "vite_f48f811a1800d9bde268e3d2eacdc4b4f8b9110e017bd7a76f",
                "removed": false
            }
        ],
        "subscription": "0x61d780619649fb0872e1f94a40cec713"
    }
}
```
轮询模式需要手动取消订阅
```bash
{
	"jsonrpc": "2.0",
	"id": 17,
	"method": "subscribe_uninstallFilter",
	"params": ["0x61d780619649fb0872e1f94a40cec713"]
}
```

### 补全数据

如果由于断开连接导致订阅不连续，可以通过`ledger_getSnapshotBlocks`（按高度范围查询快照块）、`ledger_getBlocksByHeight`（按高度范围查询账户块）、`onroad_getOnroadBlocksByAddress`（查询在途交易列表）、`subscribe_getLogs`（按账户地址、索引信息查询日志）一次性获取一段时间内的所有事件。

例如，在重新订阅快照事件时，应该先通过`subscribe_newSnapshotBlocksFilter`或者`subscribe_newSnapshotBlocks`订阅事件，然后通过`ledger_getSnapshotChainHeight`接口获取最新的快照块高度，然后通过`ledger_getSnapshotBlocks`补全断开连接时缺失的快照块。

注意：
 * gvite最低版本2.1.4，建议使用最新版本的gvite。
 * 需要在node_config.json的PublicModules中配置"subscribe"，并且配置"SubscribeEnabled":true，才能使用事件订阅接口。

## subscribe_newSnapshotBlocksFilter
轮询接口，创建一个新快照事件的filter，创建成功后可以通过subscribe_getFilterChanges轮询新事件。

- **Returns**:  
	- `string` filterId

::: demo
```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 1,
	"method": "subscribe_newSnapshotBlocksFilter",
	"params": []
}
```
```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": "0xf90906914486a9c22d620e50022b38d5"
}
```
:::

## subscribe_newAccountBlocksFilter
轮询接口，创建一个所有账户新交易事件的filter，创建成功后可以通过subscribe_getFilterChanges轮询新事件。

- **Returns**:  
	- `string` filterId

::: demo
```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 1,
	"method": "subscribe_newAccountBlocksFilter",
	"params": []
}
```
```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": "0xf90906914486a9c22d620e50022b38d5"
}
```
:::

## subscribe_newAccountBlocksByAddrFilter
轮询接口，创建单个账户新交易事件的filter，创建成功后可以通过subscribe_getFilterChanges轮询新事件。

- **Parameters**:
  * `Address`: 订阅的账户地址

- **Returns**:  
	- `string` filterId

::: demo
```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 1,
	"method": "subscribe_newAccountBlocksByAddrFilter",
	"params": ["vite_ab24ef68b84e642c0ddca06beec81c9acb1977bbd7da27a87a"]
}
```
```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": "0x4f18a08c6e6801aeb7a8cfbad0ca90af"
}
```
:::

## subscribe_newOnroadBlocksByAddrFilter
轮询接口，创建单个账户在途交易事件的filter，创建成功后可以通过subscribe_getFilterChanges轮询新事件。新事件包括新在途交易、在途交易被接收和在途交易被回滚。

- **Parameters**:
  * `Address`: 订阅的账户地址

- **Returns**:  
	- `string` filterId

::: demo
```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 1,
	"method": "subscribe_newOnroadBlocksByAddrFilter",
	"params": ["vite_ab24ef68b84e642c0ddca06beec81c9acb1977bbd7da27a87a"]
}
```
```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": "0x64e1eb3d26517a0d736b3d85ae9ce299"
}
```
:::

## subscribe_newLogsFilter
轮询接口，创建一个指定参数的新日志事件filter，创建成功后可以通过subscribe_getFilterChanges轮询新事件。

- **Parameters**:

  * `FilterParam`
    1. `addrRange`: `map[Address]Range` 只查询指定的账户地址和账户高度的日志，可以同时指定多个账户地址和高度范围，必须至少指定一个账户地址
    2. `topics`: `[][]Hash` 订阅的topics的前缀组合，使用方法见示例。
    
`Range`
  1. `fromHeight`: `uint64` 起始高度，为0表示从最新的高度开始查询
  2. `toHeight`: `uint64` 结束高度，为0表示不设置结束高度

```
topics取值示例：
 [] 匹配所有日志
 [[A]] 匹配topics中第一个元素为A的日志
 [[],[B]] 匹配topics中第二个元素为B的日志
 [[A],[B]] 匹配topics中第一个元素为A且第二个元素为B的日志
 [[A,B],[C,D]] 匹配topics中第一个元素为A或B，且第二个元素为C或D的日志
```
::: demo
```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 1,
	"method": "subscribe_newLogsFilter",
	"params": [{
		"addrRange":{
			"vite_bb6ad02107a4422d6a324fd2e3707ad53cfed9359378a78792":{
				"fromHeight":"0",
				"toHeight":"0"
			}
		}
	}]
}
```
```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": "0x8f34ddeb22b87fdfd2acb6c9f5a2b50d"
}
```
:::

## subscribe_uninstallFilter
轮询接口，轮询模式取消订阅。

- **Parameters**:
  * `string`: filterId

- **Returns**:  
	- `bool` 取消结果，true 取消成功，false 取消失败。

::: demo
```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 1,
	"method": "subscribe_uninstallFilter",
	"params": ["0x8f34ddeb22b87fdfd2acb6c9f5a2b50d"]
}
```
```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": true
}
```
:::

## subscribe_getFilterChanges
轮询接口，轮询新事件。返回值类型取决于订阅事件类型。如果上一次轮询后未产生新事件，则返回空数组。

- **Parameters**:
  * `string`: filterId

- **subscribe_newSnapshotBlocksFilter返回值**: 
  * `subscription`: `string` filterId
  * `result`: `Array<SnapshotBlocksMsg>`
    1. `hash`: `Hash` 快照块哈希
    2. `heightStr`: `uint64` 快照块高度
    3. `removed`: `bool` 是否回滚。true表示回滚，false表示新交易。
  
::: demo
```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 1,
	"method": "subscribe_getFilterChanges",
	"params": ["0xf90906914486a9c22d620e50022b38d5"]
}
```
```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
      "result": [
          {
              "hash": "5d47f2e0a532923f7ee53e7b465381f197a669e86155d541b3b7f3d63f07a0e2",
              "heightStr": "124",
              "removed": false
          },
          {
              "hash": "78b19cb84ac293d4af3f36e741938929f6d3311362e1265e87bbaa74e5fcef09",
              "heightStr": "125",
              "removed": false
          },
          {
              "hash": "94437996b3e70afd5d8593e2020ae56f63dbbc538df1ead1633340393bd52c1a",
              "heightStr": "126",
              "removed": false
          }
      ],
      "subscription": "0xf90906914486a9c22d620e50022b38d5"
    }
}
```
:::  

- **subscribe_newAccountBlocksFilter返回值**: 
  * `subscription`: `string` filterId
  * `result`: `Array<AccountBlocksMsg>`
    1. `hash`: `Hash` 账户块哈希
    2. `removed`: `bool` 是否回滚。true表示回滚，false表示新交易。
  
::: demo
```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 1,
	"method": "subscribe_getFilterChanges",
	"params": ["0xf90906914486a9c22d620e50022b38d5"]
}
```
```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
      "result": [
          {
              "Hash": "9cc9ba996a4192e35ddbfe3ba448611fc06f6342463e21d3300e58e9772b348f",
              "Removed": false
          },
          {
              "Hash": "8b9f8067ef09aa09c8f9d652f0d9ac5e99d083722089a6d91323cffd8b2dcf08",
              "Removed": false
          }
      ],
      "subscription": "0xf90906914486a9c22d620e50022b38d5"
    }
}
```
:::

- **subscribe_newAccountBlocksByAddrFilter返回值**: 
  * `subscription`: `string` filterId
  * `result`: `Array<AccountBlocksWithHeightMsg>`
    1. `hash`: `Hash` 账户块哈希
    2. `heightStr`: `uint64` 账户块高度
    3. `removed`: `bool` 是否回滚。true表示回滚，false表示新交易。
  
::: demo
```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 1,
	"method": "subscribe_getFilterChanges",
	"params": ["0x4f18a08c6e6801aeb7a8cfbad0ca90af"]
}
```
```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
      "result": [
          {
              "hash": "72ec861cb2f6c32a48632407f3aa1b05d5ad450ef75fa7660dd39d7be6d3ab68",
              "heightStr": "15",
              "removed": false
          },
          {
              "hash": "9d0df2fbc311ceb232e851a758e88fcc0a9f16d7a4240c2aa486f26f1b36d8f2",
              "heightStr": "16",
              "removed": false
          },
          {
              "hash": "18914060ba6fe9474b4c724dfe3ff5999d9cb90b5128222ade210d11fe3216f0",
              "heightStr": "17",
              "removed": false
          }
      ],
      "subscription": "0x4f18a08c6e6801aeb7a8cfbad0ca90af"
    }
}
```
:::

- **subscribe_newOnroadBlocksByAddrFilter返回值**: 
  * `subscription`: `string` filterId
  * `result`: `Array<OnroadMsg>`
    1. `hash`: `Hash` 账户块哈希
    2. `closed`: `bool` 在途交易是否被接收。
    3. `removed`: `bool` 是否回滚。removed为true时表示在途交易被回滚；removed为false，closed为false时表示为新在途交易；removed为false，closed为true时表示在途交易被接收。
  
::: demo
```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 1,
	"method": "subscribe_getFilterChanges",
	"params": ["0x64e1eb3d26517a0d736b3d85ae9ce299"]
}
```
```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
      "result": [
          {
              "hash": "72ec861cb2f6c32a48632407f3aa1b05d5ad450ef75fa7660dd39d7be6d3ab68",
              "closed": false,
              "removed": false
          },
          {
              "hash": "72ec861cb2f6c32a48632407f3aa1b05d5ad450ef75fa7660dd39d7be6d3ab68",
              "closed": true,
              "removed": false
          },
          {
              "hash": "18914060ba6fe9474b4c724dfe3ff5999d9cb90b5128222ade210d11fe3216f0",
              "closed": false,
              "removed": true
          }
      ],
      "subscription": "0x64e1eb3d26517a0d736b3d85ae9ce299"
    }
}
```
:::

- **subscribe_newLogsFilter返回值**: 
  * `subscription`: `string` filterId
  * `result`: `Array<LogsMsg>`
    1. `accountBlockHash`: `Hash` 账户块哈希
    2. `accountHeight`: `uint64` 账户块高度
    3. `addr`: `Address` 账户地址
    4. `log`: `VmLog` 日志信息
    5. `removed`: `bool` 是否回滚。true表示回滚；false表示新日志。

::: demo
```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 1,
	"method": "subscribe_getFilterChanges",
	"params": ["0x8f34ddeb22b87fdfd2acb6c9f5a2b50d"]
}
```
```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
      "result": [
          {
              "log": {
                  "topics": [
                      "aa65281f5df4b4bd3c71f2ba25905b907205fce0809a816ef8e04b4d496a85bb",
                      "000000000000000000000000bb6ad02107a4422d6a324fd2e3707ad53cfed935"
                  ],
                  "data": "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAo="
              },
              "accountBlockHash": "de8cd1dc188fd4bf44c0cb90958ffbcccab5766840d56f7b35443a1a1c5c9d3e",
              "accountHeight": "10",
              "addr": "vite_78926f48bccef67a3b9cc64fdfe864f2a708ebce1d0bbe9aef",
              "removed": false
          }
      ],
      "subscription": "0x8f34ddeb22b87fdfd2acb6c9f5a2b50d"
    }
}
```
:::

## subscribe_newSnapshotBlocks
长连接接口，创建一个新快照事件的长连接。

- **Returns**:  
	- `string` 订阅id
	
- **Callback**:  
`Object`
  1. `subscription`: `string`  订阅id
  2. `result`: `Array<SnapshotBlocksMsg>` 事件信息

::: demo
```json tab:Request
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "subscribe_subscribe",
  "params": ["newSnapshotBlocks"]
}
```
```json tab:Response
{
  "jsonrpc":"2.0",
  "id":1,
  "result":"0xa809145803ebb2a52229aefcbd52a99d"
}
```
```json tab:Callback
{
  "jsonrpc":"2.0",
  "method":"subscribe_subscription",
  "params":{
    "subscription":"0xa809145803ebb2a52229aefcbd52a99d",
    "result":[{"hash":"22c38acb79e2de0de3c5a09618054b93ac7c7e82f41f9e15d754e58694eefe16","heightStr":"250","removed":false}]
  }
}
```
:::

## subscribe_newAccountBlocks
长连接接口，创建一个所有账户新交易事件的subscription。

- **Returns**:  
	- `string` 订阅id
	
- **Callback**:  
`Object`
  1. `subscription`: `string`  订阅id
  2. `result`: `Array<AccountBlocksMsg>` 事件信息

::: demo
```json tab:Request
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "subscribe_subscribe",
  "params": ["newAccountBlocks"]
}
```
```json tab:Response
{
  "jsonrpc":"2.0",
  "id":1,
  "result":"0xa809145803ebb2a52229aefcbd52a99d"
}
```
```json tab:Callback
{
  "jsonrpc":"2.0",
  "method":"subscribe_subscription",
  "params":{
    "subscription":"0xa809145803ebb2a52229aefcbd52a99d",
    "result":[{
      "hash":"20009ee78d5f77122d215c3021f839b4024e4f2701e57bdb574e0cae1ae44e6c",
      "removed":false
    }]
  }
}
```
:::

## subscribe_newAccountBlocksByAddr
长连接接口，创建单个账户新交易事件的subscription。

- **Parameters**:

  * `address` 订阅的账户地址

- **Returns**:  
	- `string` 订阅id
	
- **Callback**:  
`Object`
  1. `subscription`: `string`  订阅id
  2. `result`: `Array<AccountBlocksWithHeightMsg>` 事件信息

::: demo
```json tab:Request
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "subscribe_subscribe",
  "params": ["newAccountBlocksByAddr", "vite_ab24ef68b84e642c0ddca06beec81c9acb1977bbd7da27a87a"]
}
```
```json tab:Response
{
  "jsonrpc":"2.0",
  "id":1,
  "result":"0xa809145803ebb2a52229aefcbd52a99d"
}
```
```json tab:Callback
{
  "jsonrpc":"2.0",
  "method":"subscribe_subscription",
  "params":{
    "subscription":"0xa809145803ebb2a52229aefcbd52a99d",
    "result":[{
      "hash":"20009ee78d5f77122d215c3021f839b4024e4f2701e57bdb574e0cae1ae44e6c",
      "heightStr":"1",
      "removed":false
    }]
  }
}
```
:::

## subscribe_newOnroadBlocksByAddr
长连接接口，创建单个账户在途交易事件的subscription。

- **Parameters**:

  * `address` 订阅的账户地址

- **Returns**:  
	- `string` 订阅id
	
- **Callback**:  
`Object`
  1. `subscription`: `string`  订阅id
  2. `result`: `Array<OnroadMsg>` 事件信息

::: demo
```json tab:Request
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "subscribe_subscribe",
  "params": ["newOnroadBlocksByAddr", "vite_ab24ef68b84e642c0ddca06beec81c9acb1977bbd7da27a87a"]
}
```
```json tab:Response
{
  "jsonrpc":"2.0",
  "id":1,
  "result":"0xa809145803ebb2a52229aefcbd52a99d"
}
```
```json tab:Callback
{
  "jsonrpc":"2.0",
  "method":"subscribe_subscription",
  "params":{
    "subscription":"0xa809145803ebb2a52229aefcbd52a99d",
    "result":[{
      "hash":"20009ee78d5f77122d215c3021f839b4024e4f2701e57bdb574e0cae1ae44e6c",
      "closed":false,
      "removed":false
    }]
  }
}
```
:::

## subscribe_newLogs
长连接接口，创建一个新日志事件的subscription。

- **Parameters**:

  * `FilterParam` 订阅参数，同subscribe_newLogsFilter

- **Returns**:  
	- `string` 订阅id
	
- **Callback**:  
`Object`
  1. `subscription`: `string`  订阅id
  2. `result`: `Array<LogsMsg>` 事件信息

::: demo
```json tab:Request
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "subscribe_subscribe",
  "params": [
    "newLogs",
    {
      "addrRange":{
        "vite_f48f811a1800d9bde268e3d2eacdc4b4f8b9110e017bd7a76f":{
          "fromHeight":"0",
          "toHeight":"0"
        }
      }
    }
  ]
}
```
```json tab:Response
{
  "jsonrpc":"2.0",
  "id":1,
  "result":"0x4b97e0674a5ebef942dbb07709c4a608"
}
```
```json tab:Callback
{
  "jsonrpc":"2.0",
  "method":"subscribe_subscription",
  "params":{
    "subscription":"0x4b97e0674a5ebef942dbb07709c4a608",
    "result":[
      {
        "log":{
          "topics":[
            "aa65281f5df4b4bd3c71f2ba25905b907205fce0809a816ef8e04b4d496a85bb",
            "000000000000000000000000bb6ad02107a4422d6a324fd2e3707ad53cfed935"
          ],
          "data":"AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAo="
        },
        "accountBlockHash":"23ea04b0dea4b9d0aa4d1f84b246b298a30faba753fa48303ad2deb29cd27f40",
        "accountHeight": "10",
        "addr":"vite_f48f811a1800d9bde268e3d2eacdc4b4f8b9110e017bd7a76f",
        "removed":false
      }
    ]
  }
}
```
:::

## subscribe_getLogs
查询历史日志。返回值按账户块高度从低到高排序。

- **Parameters**: 和`subscribe_newLogsFilter`参数类似，注意`fromHeight`和`toHeight`都填0时会查询整个账户链，可能会导致返回数据过多，最好指定明确的查询高度范围。

  * `FilterParam`
    1. `addrRange`: `map[Address]Range` 只查询指定的账户地址和账户高度的日志，可以同时指定多个账户地址和高度范围，必须至少指定一个账户地址
    2. `topics`: `[][]Hash` 订阅的topics的前缀组合，使用方法见`subscribe_newLogsFilter`方法参数。
    
`Range`
  1. `fromHeight`: `uint64` 起始高度，为0表示从账户链上第一个块开始查询
  2. `toHeight`: `uint64` 结束高度，为0表示查询到账户链上最新的块

- **Returns**:  
	- `Array<LogsMsg>` 日志信息
	
::: demo
```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 17,
	"method": "subscribe_getLogs",
	"params": [{
		"addrRange":{
			"vite_8810e12ec2d4d61e7568cac25ebd5dd44735d36a405b94f1fa":{
				"fromHeight":"1",
				"toHeight":"10"
			}
		}
	}]
}
```
```json tab:Response
{
  "jsonrpc":"2.0",
  "id":1,
  "result": [
    {
      "log": {
        "topics": [
          "28e6ea56797f4a1b22a1d1986cb6c22e80099ba8e4fd14d42accfaedfe5f6640"
        ],
        "data": "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAGQQurTFV9WklB2DRvsX8wLCgyoVomYHSCebb9Br/hQ+RAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABwYLIcJLnbQjGl+qeU7YWlTWwfsoF6mescP5xz2fDTEg="
      },
      "accountBlockHash": "e4917f357a4588ec1752797ee5516939f46078f5356b14422d4a9dfe45f88bf5",
      "accountHeight": "10",
      "addr": "vite_8810e12ec2d4d61e7568cac25ebd5dd44735d36a405b94f1fa",
      "removed": false
    }
  ]
}
```
:::
