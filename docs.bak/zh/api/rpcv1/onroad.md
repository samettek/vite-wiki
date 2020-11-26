---
sidebarDepth: 4
---

# Onroad
:::tip 维护者
[vite-crzn](https://github.com/vite-crzn)
:::

## 在途模块

对在途概念的定义，实际是用来描述账户发起交易的状态，具体是指账户发起的暂未被指定接收账户接收的交易，我们也称之为交易未闭合(Open)。BlockType常表现为1,2,3,6, 依次分别对应着 ”发起合约创建交易“、”发起转账或合约调用交易“、”发起提取出块奖励交易“、以及”发起退款交易“。

常与未确认交易混淆，未确认交易是指那些未被快照的交易。账本(Ledger模块)记录着所有发起和接受交易，而在途和未确认仅用来描述交易的不同状态，所有在途交易都是发送交易，而未确认交易既可为发送交易也可以是接受交易。


## onroad_getOnroadBlocksByAddress <Badge text="public"/>

获取账户的在途交易列表

- **Parameters**:

  * `Address`: 账户地址
  * `uint64`: 页码
  * `uint64`: 每页大小，个数上限为256

- **Return**:

  * `[]AccountBlock` 具体参考Ledger模块设计

- **Example**:


::: demo


```json tab:Request
{
    "jsonrpc": "2.0",
    "id": 2,
    "method": "onroad_getOnroadBlocksByAddress",
    "params": [
        "vite_00000000000000000000000000000000000000042d7ef71894",
        0, 
        1
    ]
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": [
        {
            "blockType": 2,
            "hash": "6301891cee55aa123be4ac4762d2d19cf3e960b84d343b848f41dc7a2c775030",
            "prevHash": "a7c0ded4733b0b8e9d6a15c98d53020db18cc3be1005aeb288cbdae4de7aee23",
            "accountAddress": "vite_360232b0378111b122685a15e612143dc9a89cfa7e803f4b5a",
            "publicKey": "P8UiTllDO/9PSMg8DrTt6g5MQuppfgTN7HF9A+UNUgA=",
            "toAddress": "vite_00000000000000000000000000000000000000042d7ef71894",
            "tokenId": "tti_5649544520544f4b454e6e40",
            "fromBlockHash": "0000000000000000000000000000000000000000000000000000000000000000",
            "data": "/cF/JQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAnMxAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA",
            "logHash": null,
            "nonce": null,
            "sendBlockList": [],
            "signature": "1jS6qK9qArQGu0M850tJ05bQHoWLj/gNDVf7qzhA5AEXRoIvLloxPVAKtbzwkrb0nRXRYP3Y/X2OggIEeHPYCA==",
            "fromAddress": "vite_360232b0378111b122685a15e612143dc9a89cfa7e803f4b5a",
            "height": "5318",
            "quota": "62000",
            "amount": "0",
            "fee": "0",
            "difficulty": null,
            "timestamp": 1555592008,
            "confirmedTimes": "3",
            "confirmedHash": "edf77dd2eb904c56002c87b3cb965c0d33c129cf9ef6f02adc1f08faf63d2acc",
            "tokenInfo": {
                "tokenName": "Vite Token",
                "tokenSymbol": "VITE",
                "totalSupply": "1000000000000000000000000000",
                "decimals": 18,
                "owner": "vite_ab24ef68b84e642c0ddca06beec81c9acb1977bbd7da27a87a",
                "tokenId": "tti_5649544520544f4b454e6e40",
                "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
                "ownerBurnOnly": false,
                "isReIssuable": true,
                "index": 0
            },
            "receiveBlockHeight": "",
            "receiveBlockHash": null
        }
    ]
}
```
:::

## onroad_getOnroadInfoByAddress <Badge text="public"/>

获取某个账户的在途资金信息

- **Parameters**:

  *  `Address`- 账户地址

- **Return**:

  * ``[]Object``:  `Object` 具体为下：
    * `accountAddress`: `Address` 账户地址
    * `totalNumber`: `string` 在途交易总数
    * `tokenBalanceInfoMap`: `Map[tokenId]Object` 具体代币的在途交易
        * `tokenInfo`: `Object` 代币信息
            * `tokenName`: `string` 代币名称
            * `tokenSymbol`: `string` 代币简称
            * `tokenId`: `TokenId` 代币id
            * `totalSupply`: `*string` 总发行量
            * `decimals`: `uint8` 小数位数
            * `owner`: `Address` 所有者
            * `maxSupply`: `*string` 最大发行量
            * `ownerBurnOnly`: `bool` 是否仅支持所有者销毁
            * `isReIssuable`: `bool` 是否可增发
            * `index`: `uint16` 索引
        * `totalAmount`: `*string` 总在途金额
        * `number`: `string` 在途数量


- **Example**:


::: demo


```json tab:Request
{
    "jsonrpc": "2.0",
    "id": 2,
    "method": "onroad_getAccountOnroadInfo",
    "params": [
        "vite_00000000000000000000000000000000000000042d7ef71894"
    ]
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": {
        "accountAddress": "vite_00000000000000000000000000000000000000042d7ef71894",
        "totalNumber": "5",
        "tokenBalanceInfoMap": {
            "tti_5649544520544f4b454e6e40": {
                "tokenInfo": {
                    "tokenName": "Vite Token",
                    "tokenSymbol": "VITE",
                    "totalSupply": "1000000000000000000000000000",
                    "decimals": 18,
                    "owner": "vite_ab24ef68b84e642c0ddca06beec81c9acb1977bbd7da27a87a",
                    "tokenId": "tti_5649544520544f4b454e6e40",
                    "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
                    "ownerBurnOnly": false,
                    "isReIssuable": true,
                    "index": 0
                },
                "totalAmount": "0",
                "number": "5"
            }
        }
    }
}
```

:::

## onroad_getOnroadBlocksInBatch <Badge text="private" type="error"/>

批量获取账户的在途交易列表

- **Parameters**:

`[]Object`: 批量查询上限为10个 
  * `Address`: 账户地址
  * `uint64`: 页码
  * `uint64`: 每页大小，个数上限为256个

- **Return**:

  * `map[Address][]AccountBlock`

- **Example**:


::: demo


```json tab:Request
{
    "jsonrpc": "2.0",
    "id": 2,
    "method": "onroad_getOnroadBlocksInBatch",
    "params": [
        [
    	    {
    		"addr": "vite_00000000000000000000000000000000000000042d7ef71894", 
    		"pageNum": 0 ,
    		"pageCount": 1
    	},
    	    	{
    		"addr": "vite_00000000000000000000000000000000000000042d7ef71894", 
    		"pageNum": 0 ,
    		"pageCount": 1
    	}
    	]]    
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": {
        "vite_00000000000000000000000000000000000000042d7ef71894": [
            {
                "blockType": 2,
                "hash": "3c21c7f27517c23b9749545a24c94077c8c1a01c0b4a51215bdc4ffde96de2a3",
                "prevHash": "6d0df63200792e1734ba52fdd4d1100e087d6d8c643e6a2bd050158ff558faaa",
                "accountAddress": "vite_360232b0378111b122685a15e612143dc9a89cfa7e803f4b5a",
                "publicKey": "P8UiTllDO/9PSMg8DrTt6g5MQuppfgTN7HF9A+UNUgA=",
                "toAddress": "vite_00000000000000000000000000000000000000042d7ef71894",
                "tokenId": "tti_5649544520544f4b454e6e40",
                "fromBlockHash": "0000000000000000000000000000000000000000000000000000000000000000",
                "data": "/cF/JQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAnMxAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA",
                "logHash": null,
                "nonce": null,
                "sendBlockList": [],
                "signature": "9rdpoB/e/VmXmwI779y3Uuz5lkXG9cO7hkOjO/gxi1Nq1Mp1JQUcaliRP9LDcFU/2CV8GMVX6VmSw3Ph7H/fDA==",
                "fromAddress": "vite_360232b0378111b122685a15e612143dc9a89cfa7e803f4b5a",
                "height": "83",
                "quota": "62000",
                "amount": "0",
                "fee": "0",
                "difficulty": null,
                "timestamp": 1555578070,
                "confirmedTimes": "3",
                "confirmedHash": "ce4694f7769dc839b7dde62b179cb0d96566cc7c64cb0bd61e62f2e167a31376",
                "tokenInfo": {
                    "tokenName": "Vite Token",
                    "tokenSymbol": "VITE",
                    "totalSupply": "1000000000000000000000000000",
                    "decimals": 18,
                    "owner": "vite_ab24ef68b84e642c0ddca06beec81c9acb1977bbd7da27a87a",
                    "tokenId": "tti_5649544520544f4b454e6e40",
                    "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
                    "ownerBurnOnly": false,
                    "isReIssuable": true,
                    "index": 0
                },
                "receiveBlockHeight": "",
                "receiveBlockHash": null
            }
        ]
    }
}
```
:::

## onroad_getOnroadInfoInBatch <Badge text="private" type="error"/>


批量获取多个账户的在途资金信息

- **Parameters**:
  * `[]Address`- 账户地址列表，上限为10个地址

- **Return**:

  * ``[]Object``:  `Object` 具体如下：
    * `accountAddress`: `Address` 账户地址
    * `totalNumber`: `string` 在途交易总数
    * `tokenBalanceInfoMap`: `Map[tokenId]Object` 具体代币的在途交易
        * `tokenInfo`: `Object` 代币信息
            * `tokenName`: `string` 代币名称
            * `tokenSymbol`: `string` 代币简称
            * `tokenId`: `TokenId` 代币id
            * `totalSupply`: `*string` 总发行量
            * `decimals`: `uint8` 小数位数
            * `owner`: `Address` 所有者
            * `pledgeAmount`: `*string` 抵押金额
            * `withdrawHeight`: `string` 抵押到期高度
            * `maxSupply`: `*string` 最大发行量
            * `ownerBurnOnly`: `bool` 是否仅支持所有者销毁
            * `isReIssuable`: `bool` 是否可增发
            * `index`: `uint16` 索引
        * `totalAmount`: `*string` 总在途金额
        * `number`: `string` 在途数量

- **Example**:
::: demo

```json tab:Request
{
    "jsonrpc": "2.0",
    "id": 2,
    "method": "onroad_getOnroadInfoInBatch",
    "params": [
        [
            "vite_00000000000000000000000000000000000000042d7ef71894",
            "vite_00000000000000000000000000000000000000042d7ef71894"
        ]
    ]
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": [
        {
            "accountAddress": "vite_00000000000000000000000000000000000000042d7ef71894",
            "totalNumber": "11",
            "tokenBalanceInfoMap": {
                "tti_5649544520544f4b454e6e40": {
                    "tokenInfo": {
                        "tokenName": "Vite Token",
                        "tokenSymbol": "VITE",
                        "totalSupply": "1000000000000000000000000000",
                        "decimals": 18,
                        "owner": "vite_ab24ef68b84e642c0ddca06beec81c9acb1977bbd7da27a87a",
                        "tokenId": "tti_5649544520544f4b454e6e40",
                        "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
                        "ownerBurnOnly": false,
                        "isReIssuable": true,
                        "index": 0
                    },
                    "totalAmount": "0",
                    "number": "11"
                }
            }
        }
    ]
}
```
:::