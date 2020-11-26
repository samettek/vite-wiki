---
sidebarDepth: 4
---

# Contract

:::tip 维护者
[viteLiz](https://github.com/viteLiz)
:::

## 创建合约步骤

创建合约本质上是发起一笔类型为创建合约的交易，并指定创建合约的代码和参数。具体步骤如下：

1. 调用`contract_getCreateContractToAddress`接口生成新合约地址。
2. 根据ABI定义对创建合约的参数进行编码。这一步可以使用`vitejs`的`abi.encodeParameters`方法（推荐），也可以调用`contract_getCreateContractParams`接口。
3. 调用`contract_getCreateContractData`接口生成交易数据。
4. 调用`tx_sendRawTx`接口发起创建合约交易，其中`toAddress`为第1步生成的合约地址；`data`为第3步生成的交易数据；`blockType`为1，表示该交易为创建合约交易；`amount`和`tokenId`为调用合约构造函数时的转账金额和代币id；`fee`字段值为创建合约费用，预主网中固定为10 vite。

注意：`vitejs`的`builtinTxBlock.createContract`接口实现了以上逻辑。

## 调用合约步骤

调用合约本质上是向合约账户发起一笔转账交易，并指定调用的接口和参数。具体步骤如下：

1. 根据ABI定义对调用合约的方法名和参数进行编码，生成交易数据。这一步可以使用`vitejs`的`abi.encodeFunctionCall`方法（推荐），也可以调用`contract_getCallContractData`接口。
2. 调用`tx_sendRawTx`接口发起调用合约交易，其中`toAddress`为被调用的合约地址；`data`为第1步生成的交易数据；`blockType`为2，表示该交易为转账交易或者调用合约交易；`amount`和`tokenId`为调用合约时的转账金额和代币id；`fee`字段值填0。

注意：`vitejs`的`builtinTxBlock.callContract`接口实现了以上逻辑。

## 离线读取合约状态

Vite链上部署的智能合约可以通过`getter`方法来离线读取合约状态。在编译合约时会生成`getter`方法的ABI定义和离线读取的代码。

1. 根据ABI定义对合约离线读取接口的方法名和参数进行编码。这一步可以使用`vitejs`的`abi.encodeFunctionCall`方法（推荐），也可以调用`contract_getCallOffChainData`接口。
2. 调用`contract_callOffChainMethod`方法，指定世界状态，获取合约状态。

## 调用内置合约

调用内置合约和调用普通合约类似，也是向内置合约发起一笔转账交易，并指定调用的接口和参数。Vite提供了[抵押获取配额](./pledge.html)、[铸币](./mintage.html)、[共识信息](./consensus.html)3个内置合约。

调用内置合约时，先调用相应的`getData`接口，例如铸币时，调用`mintage_getMintData`接口，然后通过`tx_sendRawTx`发送交易。

`vitejs`的`builtinTxBlock`模块封装了大部分内置合约的调用接口。

## contract_getCreateContractToAddress
创建合约时生成新的合约地址

- **Parameters**: 

  * `Address`: 交易的发起方
  * `uint64`: 当前块高度
  * `Hash`: 交易发起方账户链上上一个块的哈希

- **Returns**: 
	- `Address` 新的合约地址

- **Example**:

::: demo

```json tab:Request
{  
   "jsonrpc":"2.0",
   "id":1,
   "method":"contract_getCreateContractToAddress",
   "params":[
      "vite_a5a7f08011c2f0e40ccd41b5b79afbfb818d565f566002d3c6", 
      "2", 
      "3a56babeb0a8140b12ac55e91d2e05c41f908ebe99767b0e4aa5cd7af22d6de7"]
}
```

```json tab:Response
{  
   "jsonrpc":"2.0",
   "id":1,
   "result": "vite_22f4f195b6b0f899ea263241a377dbcb86befb8075f93eeac8"
}
```
:::

## contract_getCreateContractParams
对创建合约的ABI和参数进行编码

- **Parameters**: 

  * `string`: abi
  * `[]string`: 创建合约参数。简单类型直接转换为string，复合类型为json格式的string

- **Returns**: 
	- `[]byte` Data

- **Example**:

::: demo

```json tab:Request
{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "contract_getCreateContractParams",
    "params": [
        "[{\"constant\":false,\"inputs\":[{\"name\":\"voter\",\"type\":\"address\"}],\"name\":\"authorization\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"proposal\",\"type\":\"uint256\"}],\"name\":\"vote\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"inputs\":[{\"name\":\"proposalNames\",\"type\":\"uint256[]\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"constructor\"}]",
        ["[\"0x1111111111111111111111111111111111111111111111111111111111111111\",\"0x2222222222222222222222222222222222222222222222222222222222222222\"]"]
    ]
}
```
:::

## contract_getCreateContractData
获取创建合约交易请求数据

- **Parameters**: 

  * `Object`:
    * `gid`:`Gid`: 合约所属的委托共识组id，公共委托共识组id为"00000000000000000002"
    * `confirmTime`:`uint8`: 发给合约账户的request块被多少个快照块确认之后出response块，取值范围0-75，取0表示不需要等待request被快照块确认。如果合约代码中使用了随机数、时间戳、快照块高度等指令，要求这个字段值大于0。注意当confirmTime大于0时，合约的每个响应交易都会消耗额外的配额。
    * `seedCount`:`uint8`: 发给合约账户的request块被多少个包含随机数的快照块确认之后出response块，取值范围0-75，取0表示不需要等待request被包含随机数的快照块确认。如果合约代码中使用了随机数指令，要求这个字段值大于0。注意confirmTime必须大于或等于seedCount。(SEED硬分叉后支持，硬分叉前创建的合约在硬分叉后seedCount默认设置为confirmTime)
    * `quotaRatio`:`uint8`: 合约方法调用配额翻倍数*10，取值范围为10-100，例如，取值为15时表示调用合约时收取1.5倍的配额。
    * `hexCode`:`string`: 十六进制合约代码
    * `params`:`[]byte`: 编码后的参数，`contract_getCreateContractParams`接口的返回值

- **Returns**: 
	- `[]byte` Data

- **Example**:

::: demo

```json tab:Request
{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "contract_getCreateContractData",
    "params": [{
        "gid":"00000000000000000002",
        "confirmTime":2,
        "seedCount":1,
        "quotaRatio":10,
        "hexCode":"608060405234801561001057600080fd5b506101ca806100206000396000f3fe608060405260043610610041576000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff16806380ae0ea114610046575b600080fd5b6100bd6004803603602081101561005c57600080fd5b810190808035906020019064010000000081111561007957600080fd5b82018360208201111561008b57600080fd5b803590602001918460208302840111640100000000831117156100ad57600080fd5b90919293919293905050506100bf565b005b60006002838390508115156100d057fe5b061415156100dd57600080fd5b600080905060008090505b8383905081101561018a576000848483818110151561010357fe5b9050602002013590506000858560018501818110151561011f57fe5b905060200201359050808401935080841015151561013c57600080fd5b600081111561017d578173ffffffffffffffffffffffffffffffffffffffff164669ffffffffffffffffffff168260405160405180820390838587f1505050505b50506002810190506100e8565b50348114151561019957600080fd5b50505056fea165627a7a723058203cef4a3f93b33e64e99e0f88f586121282084394f6d4b70f1030ca8c360b74620029", 
        "params":""
    }]
}
```

:::

## contract_getCallContractData
获取调用合约交易请求数据

- **Parameters**: 

  * `string`: abi
  * `string`: 方法名称
  * `[]string`: 方法参数。简单类型直接转换为string，复合类型为json格式的string

- **Returns**: 
	- `[]byte` Data

- **Example**:


::: demo


```json tab:Request
{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "contract_getCallContractData",
    "params": [
        "[{\"constant\":false,\"inputs\":[{\"name\":\"voter\",\"type\":\"address\"}],\"name\":\"authorization\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"proposal\",\"type\":\"uint256\"}],\"name\":\"vote\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"inputs\":[{\"name\":\"proposalNames\",\"type\":\"uint256[]\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"constructor\"}]",
        "vote",
        ["0x1111111111111111111111111111111111111111111111111111111111111111"]
    ]
}
```

:::


## contract_getContractInfo
查询合约信息

- **Parameters**: 

  * `string`: 合约账户地址
  
- **Returns**: 
	`ContractInfo`
    1. `code`: `[]byte`  合约代码
    2. `gid`: `Gid`  合约所属委托共识组id
    3. `confirmTime`: `uint8` 发给合约账户的request块被多少个快照块确认之后出response块
    4. `seedCount`: `uint8` 发给合约账户的request块被多少个包含随机数种子的快照块确认之后出response块

- **Example**:

::: demo
```json tab:Request
{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "contract_getContractInfo",
    "params": ["vite_22f4f195b6b0f899ea263241a377dbcb86befb8075f93eeac8"]
}
```
:::

## contract_getCallOffChainData
按ABI定义对getter方法的入参进行编码。返回值可作为`contract_callOffChainMethod`方法入参中的data参数。

- **Parameters**: 

  * `string` 合约ABI
  * `string` getter方法名称
  * `[]string` getter方法参数列表
  
- **Returns**: 
	`[]byte` 按ABI定义编码后的getter方法入参。

- **Example**:

::: demo
```json tab:Request
{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "contract_getCallOffChainData",
    "params": [
      "[{\"constant\":true,\"inputs\":[],\"name\":\"getTokenList\",\"outputs\":[{\"name\":\"\",\"type\":\"tokenId[]\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"offchain\"}]",
      "getTokenList",
      []
    ]
}
```
:::

## contract_callOffChainMethod
离线查询合约状态。合约代码中的getter方法可以通过离线查询的方式来调用。

- **Parameters**: 

  * `Object`:
    * `selfAddr`:`Address` 合约账户地址
    * `offchainCode`:`string` 用于离线查询的合约代码。编译代码时指定`--bin`参数后得到的`OffChain Binary`代码。十六进制格式代码。
    * `offChainCodeBytes`:`[]byte` 用于离线查询的合约代码。编译代码时指定`--bin`参数后得到的`OffChain Binary`代码。base64格式代码。注意offchainCode和offChainCodeBytes只需要填一个。
    * `data`:`[]byte` 按ABI定义编码后的调用参数，`contract_getCallOffChainData`接口的返回值
    
- **Returns**: 
	`[]byte` 按ABI定义编码后的getter方法返回值。可以使用vitejs的abi decode方法反解析。

- **Example**:

::: demo
```json tab:Request
{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "contract_callOffChainMethod",
    "params": [{
      "selfAddr":"vite_22f4f195b6b0f899ea263241a377dbcb86befb8075f93eeac8",
      "offChainCodeBytes":"YIBgQFJgBDYQYQBQV2AANXwBAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAJAEY/////8WgGO+RoE6FGEAVFeAY/EnHggUYQCxV2EAUFZbW1sAW2EAjWAEgDYDYCCBEBVhAGtXYABgAP1bgQGQgIA1af////////////8WkGAgAZCSkZBQUFBhARFWW2BAUYCEgVJgIAGDgVJgIAGCgVJgIAGTUFBQUGBAUYCRA5DzW2EAuWEB0VZbYEBRgIBgIAGCgQOCUoOBgVGBUmAgAZFQgFGQYCABkGAgAoCDg2AAW4OBEBVhAP1XgIIBUYGEAVJbYCCBAZBQYQDhVltQUFBQkFABklBQUGBAUYCRA5DzW2AAYABgAGACYABQYACFaf////////////8Waf////////////8WgVJgIAGQgVJgIAFgACFgAFBgAAFgAFBUYAJgAFBgAIZp/////////////xZp/////////////xaBUmAgAZCBUmAgAWAAIWAAUGABAWAAUFRgAmAAUGAAh2n/////////////Fmn/////////////FoFSYCABkIFSYCABYAAhYABQYAIBYABQVJJQklCSUGEBylZbkZOQklBWW2BgYAFgAFCAVIBgIAJgIAFgQFGQgQFgQFKAkpGQgYFSYCABgoBUgBVhAlpXYCACggGRkGAAUmAgYAAhkGAAkFuCgpBUkGEBAAqQBGn/////////////Fmn/////////////FoFSYCABkGAKAZBgIIJgCQEEkoMBkmABA4ICkVCAhBFhAhFXkFBbUFBQUFCQUGECZlZbkFb+oWVienpyMFgg9JX2H2l/JeRsqoaMCbNbV1qzMePGCBeYgOGTK1hIq6oAKQ==",
      "data":"f1271e08"
    }]
}
```
:::
