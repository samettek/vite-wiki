# ABI

## 安装

:::demo
```bash tab:npm
npm install @vite/vitejs-abi --save
```

```bash tab:yarn
yarn add @vite/vitejs-abi
```
:::

## 引入

```javascript import
import { abi } from '@vite/vitejs';
// Or
import * as abi from '@vite/vitejs-abi';
```

## 参数类型说明
合约方法（包括构造方法、异步调用、离线读取）可以包含多个参数，其中离线读取接口还可以包含多个返回值，目前支持以下参数类型：


| 参数类型 | 名称 | 示例 | 编码前示例 | 编码后示例 |
|:------------:|:-----------:|:-----------:|:-----------:|:-----------:|
| `uint<M>` | 无符号整数，其中 0 < M <= 256，M % 8 == 0 | uint256 | '2345675643' | '000000000000000000000000000000000000000000000000000000008bd02b7b' |
| `int<M>` | 有符号整数，其中 0 < M <= 256，M % 8 == 0 | int8 | '2' | '0000000000000000000000000000000000000000000000000000000000000002' |
| `uint` | 相当于uint256 | uint | '2345675643' | '000000000000000000000000000000000000000000000000000000008bd02b7b' |
| `int` | 相当于int256 | int | '2' | '0000000000000000000000000000000000000000000000000000000000000002' |
| `tokenId` | 代币id | tokenId | 'tti_5649544520544f4b454e6e40' | '000000000000000000000000000000000000000000005649544520544f4b454e' |
| `address` | 账户地址 | address | 'vite_010000000000000000000000000000000000000063bef3da00' | '0000000000000000000000010000000000000000000000000000000000000000' |
| `gid` | 委托共识组id | gid | '01000000000000000000' | '0000000000000000000000000000000000000000000001000000000000000000' |
| `bool` | 布尔 | bool | true | '0000000000000000000000000000000000000000000000000000000000000001' |
| `bytes<M>` | 定长字节数组，其中 0 < M <= 32 | bytes32 | '0x0100000000000000000000000000000000000000000000000000000000000000' | '0100000000000000000000000000000000000000000000000000000000000000' |
| `bytes` | 不定长字节数组 | bytes | '0xdf3234' | '00000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000003df32340000000000000000000000000000000000000000000000000000000000' | 
| `string` | 不定长字符串 | string | 'foobar' | '0000000000000000000000000000000000000000000000000000000000000006666f6f6261720000000000000000000000000000000000000000000000000000' |
| `<type>[M]` | type类型的定长数组，其中 M >= 0，type取值范围：`uint<M>`、`int<M>`、`uint`、`int`、`tokenId`、`address`、`gid`、`bool`、`string` | uint8[2] | ['1','2'] | '00000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000002' |
| `<type>[]` | type类型的不定长数组，type取值范围：`uint<M>`、`int<M>`、`uint`、`int`、`tokenId`、`address`、`gid`、`bool`、`string` | uint256[] | ['1','2'] | '000000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000002' |

- **Example jsonInterface**

```json ::Demo
{
    "type": "event",
    "name": "methodName",
    "inputs": [
        { "name": "input1", "type": "address" }
    ]
}
```

## Methods

### encodeLogSignature

- **Parameters**
    * `jsonInterface | Array<jsonInterface>`
    * `methodName?` 当第一个参数为数组时, 此参数必填(用于识别abi)

- **Return**
    * `hexString`

- **Example**
```js ::Demo
let encodeLogSignatureResult1 = abi.encodeLogSignature({
    'type': 'event',
    'name': 'balance',
    'inputs': [{'name':'in','type':'uint256'}]
});
// 8a3390b86e28f274e3a88354b3b83cf0f8780a1f0975f629966bd2a2d38eb188

let encodeLogSignatureResult22 = abi.encodeLogSignature([
    {'type':'event','name':'heck','inputs':[{'name':'t','type':'address'}]},
    {'type':'event','name':'check','inputs':[{'name':'t','type':'address'},{'name':'b','type':'uint256'}]},
    {'type':'event','name':'eck','inputs':[]},
], 'check');
// 17c53855485cba60b5dea781a996394bb9d3b44bc8932b3adf79ac70e908b220
```    

### encodeFunctionSignature

- **Parameters**
    * `jsonInterface | Array<jsonInterface>`
    * `methodName?` 当第一个参数为数组时, 此参数必填(用于识别abi)

- **Return**
    * `hexString`

- **Example**
```js ::Demo
let encodeMethodResult1 = abi.encodeFunctionSignature({
    'type': 'function',
    'name': 'singleParam',
    'inputs': [{'name':'param1','type':'address'}]
}); 
// 053f71a4
```  

### encodeFunctionCall

- **Parameters**
    * `jsonInterface | Array<jsonInterface>`
    * `params`
    * `methodName?` 当第一个参数为数组时, 此参数必填(用于识别abi)

- **Return**
    * `hexString`

- **Example**
```js ::Demo
let result = abi.encodeFunctionCall({
    name: 'myMethod',
    type: 'function',
    inputs: [{
        type: 'uint256',
        name: 'myNumber'
    },{
        type: 'string',
        name: 'myString'
    }]
}, ['2345675643', 'Hello!%']);
// 96173f6c000000000000000000000000000000000000000000000000000000008bd02b7b0000000000000000000000000000000000000000000000000000000000000040000000000000000000000000000000000000000000000000000000000000000748656c6c6f212500000000000000000000000000000000000000000000000000

let result1 = abi.encodeFunctionCall([{
    name: 'myMethod',
    type: 'function',
    inputs: [{
        type: 'uint256',
        name: 'myNumber'
    },{
        type: 'string',
        name: 'myString'
    }]
}, {
    name: 'myethod',
    type: 'function',
    inputs: [{
        type: 'uint256',
        name: 'myNumber'
    },{
        type: 'string',
        name: 'myString'
    }]
}], ['2345675643', 'Hello!%'], 'myMethod');
// 96173f6c000000000000000000000000000000000000000000000000000000008bd02b7b0000000000000000000000000000000000000000000000000000000000000040000000000000000000000000000000000000000000000000000000000000000748656c6c6f212500000000000000000000000000000000000000000000000000
```  

### encodeParameter

- **Parameters**
    * `type`
    * `params` 当第一个参数为数组类型时, 第二个参数应传数组(二者类型应一致)

- **Return**
    * `hexString`

- **Example**
```js ::Demo
let _r = abi.encodeParameter('uint256', '2345675643');
// 000000000000000000000000000000000000000000000000000000008bd02b7b

let encodeParameterResult4 = abi.encodeParameter('uint16[]', [1,2]);
// 000000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000002
```  

### decodeParameter

- **Parameters**
    * `type`
    * `hexString`

- **Return**
    * `decodeResult`

- **Example**
```js ::Demo
let _r = abi.decodeParameter('uint256', '000000000000000000000000000000000000000000000000000000008bd02b7b');
// 2345675643

let encodeParameterResult2 = abi.decodeParameter('uint8[]', '000000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000002');
// ['1','2']
```  

### encodeParameters

- **Parameters**
    * `jsonInterface | Array<type-string> | Array<jsonInterface>`
    * `params<Array | json-string>`
    * `methodName?` 当第一个参数为数组时, 此参数必填(用于识别abi, 取出对应types)

- **Return**
    * `hexString`

- **Example**
```js ::Demo
let encodeParametersResult1 = abi.encodeParameters({'type':'constructor','inputs':[
    {'type':'uint8[]'}, {'type': 'bytes'}
]}, [['34','43'], '324567ff']);

// Or json-string, eg
// let encodeParametersResult1 = abi.encodeParameters({'type':'constructor','inputs':[
//     {'type':'uint8[]'}, {'type': 'bytes'}
// ]}, JSON.stringfy([['34','43'], '324567ff']));

// 000000000000000000000000000000000000000000000000000000000000004000000000000000000000000000000000000000000000000000000000000000a000000000000000000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000000000022000000000000000000000000000000000000000000000000000000000000002b0000000000000000000000000000000000000000000000000000000000000004324567ff00000000000000000000000000000000000000000000000000000000

let encodeParametersResult4 = abi.encodeParameters(['tokenId','address'], ['tti_01000000000000000000fb5e', 'vite_010000000000000000000000000000000000000063bef3da00']);
// 00000000000000000000000000000000000000000000010000000000000000000000000000000000000000010000000000000000000000000000000000000000

let encodeParametersResult12 = abi.encodeParameters([
    {'type':'constructor', 'name': 'myMethods', 'inputs':[{'type':'uint8[]'}, {'type': 'bytes'}]},
    {'type':'constructor', 'name': 'myMetod', 'inputs':[{'type': 'bytes'}]},
    {'type':'constructor', 'name': 'myMethowed', 'inputs':[{'type':'uint8[]'}, {'type': 'bytes'}]},
    {'type':'constructor', 'name': 'myMethossssd', 'inputs':[{'type': 'bytes'}]}
], [['34','43'], '324567ff'], 'myMethowed');
// 000000000000000000000000000000000000000000000000000000000000004000000000000000000000000000000000000000000000000000000000000000a000000000000000000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000000000022000000000000000000000000000000000000000000000000000000000000002b0000000000000000000000000000000000000000000000000000000000000004324567ff00000000000000000000000000000000000000000000000000000000

```  

### decodeParameters

- **Parameters**
    * `jsonInterface | Array<type-string> | Array<jsonInterface>`
    * `hexString`
    * `methodName?` 当第一个参数为数组时, 此参数必填(用于识别abi, 取出对应types)

- **Return**
    * `decodeResult`

- **Example**
```js ::Demo
let decodeParametersResult1 = abi.decodeParameters({'type':'constructor','inputs':[
    {'type':'uint8[]'}, {'type': 'bytes'}
]}, '000000000000000000000000000000000000000000000000000000000000004000000000000000000000000000000000000000000000000000000000000000a000000000000000000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000000000022000000000000000000000000000000000000000000000000000000000000002b0000000000000000000000000000000000000000000000000000000000000004324567ff00000000000000000000000000000000000000000000000000000000');
// [['34','43'], '324567ff']

let decodeParametersResult5 = abi.decodeParameters(['string', 'tokenId','address'], '000000000000000000000000000000000000000000000000000000000000006000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000f343832393438326e73646b6a736b640000000000000000000000000000000000');
// ['4829482nsdkjskd', 'tti_01000000000000000000fb5e', 'vite_00010000000000000000000000000000000000005cce05dbde']

let decodeParametersResult22 = abi.decodeParameters([
    {'type':'function','name':'singl','inputs':[{'name':'param1','type':'address'}]},
    {'type':'function','name':'singleParam','inputs':[
        {'name':'param1','type':'address'},
        {'name':'param1','type':'uint8[]'}
    ]}
], '00000000000000000000000001000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000040000000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000002', 'singleParam');
// ['vite_00010000000000000000000000000000000000005cce05dbde', [1,2]]
```  

### decodeLog

- **Parameters**
    * `jsonInterface.inputs | jsonInterface | Array<jsonInterface>`
    * `hexString`
    * `Array<hexString>`
    * `methodName?` 当第一个参数为jsonInterface数组时, 此参数必填(用于识别abi, 取出对应inputs)

- **Return**
    * `decodeResult`

- **Example**
```js ::Demo
let decodeResult2 = abi.decodeLog(
    [
        {'indexed':true,'name':'from','type':'address'},
        {'indexed':true,'name':'to','type':'address'},
        {'indexed':false,'name':'value','type':'uint256'}
    ], 
    '00000000000000000000000000000000000000000000000000000000000f4240',
    ['0000000000000000000000000100000000000000000000000000000000000000', '0000000000000000000000000200000000000000000000000000000000000000']
);
// {
//     '0': 'vite_00010000000000000000000000000000000000005cce05dbde',
//     '1': 'vite_0002000000000000000000000000000000000000fe64322db1',
//     '2': '1000000',
//     from: 'vite_00010000000000000000000000000000000000005cce05dbde',
//     to: 'vite_0002000000000000000000000000000000000000fe64322db1',
//     value: '1000000'
// }

let decodeResult222 = abi.decodeLog([
    { 
        'type':'constructor',
        'name': '89xxx',
        'inputs':[{type:'string',name:'myString'}]
    },
    { 'name': '232', 'inputs':[] },
    { 
        'type':'constructor',
        'name': 'xxxxx',
        'inputs':[
            {type:'string',name:'myString'},
            {type:'uint256',name:'myNumber',indexed: true},
            {type: 'uint8',name: 'mySmallNumber',indexed: true}
        ]
    }
], 
'0000000000000000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000000000000748656c6c6f252100000000000000000000000000000000000000000000000000',
['000000000000000000000000000000000000000000000000000000000000f310', '0000000000000000000000000000000000000000000000000000000000000010'], 'xxxxx');
// {
//     '0': 'Hello%!',
//     '1': '62224',
//     '2': '16',
//     myString: 'Hello%!',
//     myNumber: '62224',
//     mySmallNumber: '16'
// }

let decodeResult1 = abi.decodeLog({'type':'constructor','inputs':[
    {type:'string',name:'myString'},
    {type:'uint256',name:'myNumber',indexed: true},
    {type: 'uint8',name: 'mySmallNumber',indexed: true}
]}, 
'0000000000000000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000000000000748656c6c6f252100000000000000000000000000000000000000000000000000',
['000000000000000000000000000000000000000000000000000000000000f310', '0000000000000000000000000000000000000000000000000000000000000010']);
// {
//     '0': 'Hello%!',
//     '1': '62224',
//     '2': '16',
//     myString: 'Hello%!',
//     myNumber: '62224',
//     mySmallNumber: '16'
// }
```  
