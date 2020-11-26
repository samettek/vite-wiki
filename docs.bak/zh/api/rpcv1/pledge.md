---
sidebarDepth: 4
---

# Pledge
:::tip 维护者
[viteLiz](https://github.com/viteLiz)
:::

## 合约信息说明
抵押合约，合约账户地址： `vite_0000000000000000000000000000000000000003f6af7459b9`

ABI：

```json
[
  // 抵押获取配额
  {"type":"function","name":"Pledge", "inputs":[{"name":"beneficial","type":"address"}]},
  // 取消抵押
  {"type":"function","name":"CancelPledge","inputs":[{"name":"beneficial","type":"address"},{"name":"amount","type":"uint256"}]},
  // 代理抵押
  {"type":"function","name":"AgentPledge", "inputs":[{"name":"pledgeAddress","type":"address"},{"name":"beneficial","type":"address"},{"name":"bid","type":"uint8"}]},
  // 代理抵押回调
  {"type":"function","name":"AgentPledgeCallback","inputs":[{"name":"pledgeAddress","type":"address"},{"name":"beneficial","type":"address"},{"name":"amount","type":"uint256"},{"name":"bid","type":"uint8"},{"name":"success","type":"bool"}]},
  // 取消代理抵押
  {"type":"function","name":"AgentCancelPledge","inputs":[{"name":"pledgeAddress","type":"address"},{"name":"beneficial","type":"address"},{"name":"amount","type":"uint256"},{"name":"bid","type":"uint8"}]},
  // 取消代理抵押回调
  {"type":"function","name":"AgentCancelPledgeCallback","inputs":[{"name":"pledgeAddress","type":"address"},{"name":"beneficial","type":"address"},{"name":"amount","type":"uint256"},{"name":"bid","type":"uint8"},{"name":"success","type":"bool"}]}		
]
```

其中，代理抵押和去掉代理抵押的响应交易会产生回调请求交易，通知本次代理抵押或者取消代理抵押交易是否成功。

## pledge_getPledgeData
获取抵押交易请求数据，也可以通过对ABI中的`Pledge`方法编码获取交易请求数据。

- **Parameters**: 

  * `Address`: 抵押受益账户

- **Returns**: 
	- `[]byte` Data

- **Example**:


::: demo


```json tab:Request
{  
   "jsonrpc":"2.0",
   "id":1,
   "method":"pledge_getPledgeData",
   "params":["vite_a5a7f08011c2f0e40ccd41b5b79afbfb818d565f566002d3c6"]
}
```

:::

## pledge_getCancelPledgeData
获取撤销抵押交易请求数据，也可以通过对ABI中的`CancelPledge`方法编码获取交易请求数据。

- **Parameters**: 

  * `Address`: 抵押受益账户
  * `big.int`: 撤销金额

- **Returns**: 
	- `[]byte` Data

- **Example**:


::: demo


```json tab:Request
{  
   "jsonrpc":"2.0",
   "id":1,
   "method":"pledge_getCancelPledgeData",
   "params":[
      "vite_a5a7f08011c2f0e40ccd41b5b79afbfb818d565f566002d3c6",
      "10"
    ]
}
```

:::

## pledge_getAgentPledgeData
获取代理抵押交易请求数据，也可以通过对ABI中的`AgentPledge`方法编码获取交易请求数据。

- **Parameters**: 

`Object`
  1. `pledgeAddr`:`Address`  实际抵押地址
  2. `beneficialAddr`:`Address`  抵押受益地址
  3. `bid`:`uint8`  业务id，来自同一个代理地址相同业务id的多笔抵押金额会合并，抵押到期时间也会顺延
  4. `stakeHeight`:`uint64`  抵押高度，范围为259200~31536000，例如259200表示抵押之后等待259200个快照块之后可以取回抵押。

- **Returns**: 
	- `[]byte` Data

- **Example**:

::: demo

```json tab:Request
{  
   "jsonrpc":"2.0",
   "id":1,
   "method":"pledge_getAgentPledgeData",
   "params":[
      {
      	"pledgeAddr":"vite_56fd05b23ff26cd7b0a40957fb77bde60c9fd6ebc35f809c23",
      	"beneficialAddr":"vite_a5a7f08011c2f0e40ccd41b5b79afbfb818d565f566002d3c6",
      	"bid":1,
      	"stakeHeight":"259200"
      }
   ]
}
```

:::

## pledge_getAgentCancelPledgeData
获取代理撤销抵押交易请求数据，也可以通过对ABI中的`AgentCancelPledge`方法编码获取交易请求数据。

- **Parameters**: 

`Object`
  1. `pledgeAddr`:`Address`  实际抵押地址
  2. `beneficialAddr`:`Address`  抵押受益地址
  3. `bid`:`uint8`  业务id
  4. `amount`:`big.Int`  撤销金额

- **Returns**: 
	- `[]byte` Data

- **Example**:


::: demo


```json tab:Request
{  
   "jsonrpc":"2.0",
   "id":1,
   "method":"pledge_getAgentCancelPledgeData",
   "params":[
      {
      	"pledgeAddr":"vite_56fd05b23ff26cd7b0a40957fb77bde60c9fd6ebc35f809c23",
      	"beneficialAddr":"vite_a5a7f08011c2f0e40ccd41b5b79afbfb818d565f566002d3c6",
      	"amount":"200000000000000000000",
      	"bid":1
      }
    ]
}
```

:::

## pledge_getPledgeQuota
获取账户当前配额和最大能发起的交易数

- **Parameters**: 

  * `Address`: 账户地址

- **Returns**: 

`Object`
  1. `current`: `uint64`  当前可用配额
  2. `quotaPerSnapshotBlock`: `uint64` 抵押vite后，每增长一个快照块获得的配额
  3. `currentUt`: `float`: 当前可用配额，单位：ut，精确到小数点后4位
  4. `utpe`: `float`: 当前抵押可以获得的最高配额，单位：ut，精确到小数点后4位
  5. `pledgeAmount`: `big.Int`: 抵押的vite金额
  

- **Example**:


::: demo


```json tab:Request
{  
   "jsonrpc":"2.0",
   "id":1,
   "method":"pledge_getPledgeQuota",
   "params": ["vite_a5a7f08011c2f0e40ccd41b5b79afbfb818d565f566002d3c6"]
}
```

```json tab:Response
{  
   "jsonrpc":"2.0",
   "id":1,
   "result": {
      "current": "1575000",
      "quotaPerSnapshotBlock": "21000",
      "currentUt": "75",
      "utpe": "75",
      "pledgeAmount": "134000000000000000000"
   }
}
```
:::

## pledge_getPledgeList
获取本账户的抵押金额列表，按到期快照块高度倒序排序

- **Parameters**: 

  * `Address`: 抵押账户地址
  * `int`: 页码，从0开始
  * `int`: 每页条数

- **Returns**: 

`Object`
  1. `totalPledgeAmount`: `big.Int`  本账户抵押的总金额
  2. `totalCount`: `int`  抵押信息总数
  3. `pledgeInfoList`: `Array<PledgeInfo>` 抵押信息列表
     * `amount`: `big.int`  抵押金额
     * `withdrawHeight`: `uint64`  到期快照块高度
     * `beneficialAddr`: `Address`  受益地址
     * `withdrawTime`: `int64`  预计到期时间
     * `agent`: `bool`  是否代理抵押，true-代理抵押 false-普通抵押
     * `agentAddress`: `Address`  代理地址，普通抵押时，代理地址为0
     * `bid`: `uint8`  业务id，普通抵押时，业务id为0
    

- **Example**:


::: demo


```json tab:Request
{  
   "jsonrpc":"2.0",
   "id":1,
   "method":"pledge_getPledgeList",
   "params":["vite_a5a7f08011c2f0e40ccd41b5b79afbfb818d565f566002d3c6", 0, 50]
}
```

```json tab:Response
{  
   "jsonrpc":"2.0",
   "id":1,
   "result":  {
      "totalPledgeAmount": "5000000000000000000000",
      "totalCount": 1,
      "pledgeInfoList": [
        {
          "amount":10000000000000000000,
          "withdrawHeight":259200,
          "beneficialAddr":"vite_a5a7f08011c2f0e40ccd41b5b79afbfb818d565f566002d3c6",
          "withdrawTime":1540213336,
          "agent":false,
          "agentAddress":"vite_0000000000000000000000000000000000000000a4f3a0cb58",
          "bid":0
        }
      ]
   }
}
```
:::

## pledge_getAgentPledgeInfo
获取代理抵押信息

- **Parameters**: 

`Object`
  1. `pledgeAddr`:`Address`  实际抵押地址
  2. `agentAddr`:`Address`  代理抵押地址
  3. `beneficialAddr`:`Address`  抵押受益地址
  4. `bid`:`uint8`  业务id，来自同一个代理地址相同业务id的多笔抵押金额会合并，抵押到期时间也会顺延

- **Returns**: 

`Object`
  1.`amount`: `big.int`  抵押金额
  2.`withdrawHeight`: `uint64`  到期快照块高度
  3.`beneficialAddr`: `Address`  受益地址
  4.`withdrawTime`: `int64`  预计到期时间
  5.`agent`: `bool`  是否代理抵押，true-代理抵押 false-普通抵押
  6.`agentAddress`: `Address`  代理地址，普通抵押时，代理地址为0
  7.`bid`: `uint8`  业务id，普通抵押时，业务id为0
    

- **Example**:


::: demo


```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 1,
	"method": "pledge_getAgentPledgeInfo",
	"params": [
		{
			"pledgeAddr":"vite_56fd05b23ff26cd7b0a40957fb77bde60c9fd6ebc35f809c23", 
			"agentAddr":"vite_ab24ef68b84e642c0ddca06beec81c9acb1977bbd7da27a87a",
			"beneficialAddr":"vite_a5a7f08011c2f0e40ccd41b5b79afbfb818d565f566002d3c6",
			"bid":1
		}
	]
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "amount": "1000000000000000000000",
        "withdrawHeight": "259992",
        "beneficialAddr": "vite_a5a7f08011c2f0e40ccd41b5b79afbfb818d565f566002d3c6",
        "withdrawTime": 1561098331,
        "agent": true,
        "agentAddress": "vite_ab24ef68b84e642c0ddca06beec81c9acb1977bbd7da27a87a",
        "bid": 1
    }
}
```
:::

