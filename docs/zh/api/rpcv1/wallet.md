---
sidebarDepth: 4
---

# Wallet
:::tip 维护者
[TiantaoZhu](https://github.com/TiantaoZhu)
:::

## wallet_listEntropyFilesInStandardDir
返回所有在标准EntropyStore目录下的地址

- **Parameters**: `none`

- **Returns**: 
	- `Array[string]` EntropyStore绝对路径

- **Example**:


::: demo


```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 4,
	"method": "wallet_listEntropyFilesInStandardDir",
	"params": []
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 4,
    "result": [
        "/Users/xxx/Library/GVite/testdata/wallet/vite_15391ac8b09d4e8ad78bfe5f9f9ab9682fe689572f6f53655e",
        "/Users/xxx/Library/GVite/testdata/wallet/vite_5b013ec4f3c235da12e47b525713e2f5edd0b04df965fafc22",
        "/Users/xxx/Library/GVite/testdata/wallet/vite_67de981eff372d4a757541b05f0e8a269eee11c2f6c9fbdae6",
        "/Users/xxx/Library/GVite/testdata/wallet/vite_f24bb4eceadc65020de5de6a4aeb22c52edd6cb72ee2279a97"
    ]
}

```
:::

## wallet_listAllEntropyFiles 
列出已经在钱包管理的所有EntropyStore

- **Parameters**: `none`

- **Returns**: 
	- `Array[string]` EntropyStore绝对路径


- **Example**:

::: demo
```json tab:Request
{
    "jsonrpc": "2.0",
    "id": 2,
    "method": "wallet_listAllEntropyFiles",
    "params": []
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 4,
    "result": [
        "/Users/xxx/Library/GVite/testdata/wallet/vite_15391ac8b09d4e8ad78bfe5f9f9ab9682fe689572f6f53655e",
        "/Users/xxx/Library/GVite/testdata/wallet/vite_5b013ec4f3c235da12e47b525713e2f5edd0b04df965fafc22",
        "/Users/xxx/Library/GVite/testdata/wallet/vite_67de981eff372d4a757541b05f0e8a269eee11c2f6c9fbdae6"
    ]
}
```
:::

## wallet_extractMnemonic
 获得某个EntropyStore的助记词

- **Parameters**: 
	- `string` : EntropyStore的绝对路径，如果EntropyStore文件在标准钱包目录下，只要传文件名就可以，标准的文件名是用0号地址命名
	- `string` : 密码 

- **Returns**: 
	- `string`: Mnemonic

- **Example**: 

::: demo
```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 4,
	"method": "wallet_extractMnemonic",
	"params": [
		"vite_15391ac8b09d4e8ad78bfe5f9f9ab9682fe689572f6f53655e",
		"123456"]
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 4,
    "result": "goddess crush pattern cluster level combine survey give seminar uniform invite beach"
}
```
:::

## wallet_unlock
解锁某个EntropyStore

- **Parameters**: 
	- `string` : EntropyStore的绝对路径，如果EntropyStore文件在标准钱包目录下，只要传文件名就可以，标准的文件名是用0号地址命名
	- `string` : 密码 

- **Returns**: 
	- `null`

- **Example**: 

::: demo
```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 4,
	"method": "wallet_unlock",
	"params": [
		"vite_15391ac8b09d4e8ad78bfe5f9f9ab9682fe689572f6f53655e",
		"123456"]
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 4,
    "result": null
}
```
:::

## wallet_lock
加锁账户

- **Parameters**: 
	- `string` : EntropyStore的绝对路径，如果EntropyStore文件在标准钱包目录下，只要传文件名就可以，标准的文件名是用0号地址命名


- **Returns**:
	- `null`

- **Example**:

::: demo
```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 4,
	"method": "wallet_lock",
	"params": [
		"vite_15391ac8b09d4e8ad78bfe5f9f9ab9682fe689572f6f53655e"]
}
```

```json tab:Response Success
{
    "jsonrpc": "2.0",
    "id": 4,
    "result": null
}
```

:::


### wallet_listEntropyStoreAddresses
列出该EntropyStore下指定范围内的地址

- **Parameters**: 
	- `string`: 地址或者文件名
	- `uint32`:左边界（包含）
	- `uint32`:右边届（不包含）

- **Returns**: 
	- `Array[string]`: 地址

- **Example**:

::: demo

```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 4,
	"method": "wallet_listEntropyStoreAddresses",
	"params": [
		"/Users/xxx/Library/GVite/testdata/wallet/vite_15391ac8b09d4e8ad78bfe5f9f9ab9682fe689572f6f53655e",
		0,
		10
	]
}
```
```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 4,
    "result": [
        "vite_15391ac8b09d4e8ad78bfe5f9f9ab9682fe689572f6f53655e",
        "vite_659fbce2a908bdab3b7c46348f249c90c812e36b9ceac67aa0",
        "vite_cc373442a471a8dd4b2240d5a74f8e4037177a8795d30bdfd7",
        "vite_1beb02f13af1b16a317c927d470ca3118ba738e22da3f8bf6e",
        "vite_d1c10321319de24bcbd865e7f4127f5873bf9c251f0a4abb00",
        "vite_acf35393ba47b8216ebbc5252e8884d518971a57c11b5866e1",
        "vite_87df61f0feddb6121fecf7d5ba8d7e56443d53ead06da90a06",
        "vite_8de52abce25c65116b08d84966d67e3dd7860848b52f388d23",
        "vite_ed346025dc7196ed000caa429306bbed1bda42010597d63676",
        "vite_783baa0caccff4d365f09873660208ee727bfc5d9710b267e5"]
}
```
:::


## wallet_newMnemonicAndEntropyStore
创建助记词和EntropyStore

- **Parameters**: 
	- `string`: 密码

- **Returns**: 
	- `Object`:
		- `mnemonic : string` : 助记词
		- `primaryAddr : string` : 地址
		- `filename : string`: 文件地址  

- **Example**:

::: demo
```json tab:Request
{
    "jsonrpc": "2.0",
    "id": 2,
    "method": "wallet_newMnemonicAndEntropyStore",
    "params": [
        "123456"
    ]
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": {
        "mnemonic": "pear lonely piece base local lift material damp animal siege error throw ride flag version dumb parent clever upper toe lumber great wild vivid",
        "primaryAddr": "vite_f646dc1f32b0ea88289bbfe4e4138d26edc9f9eac33a9e5292",
        "filename": "/Users/xxx/Library/GVite/testdata/wallet/vite_f646dc1f32b0ea88289bbfe4e4138d26edc9f9eac33a9e5292"
    }
}
```
:::

## wallet_deriveByIndex
派生地址

- **Parameters**: 
	- `string` : 文件地址或者初始地址
	- `uint32`: 派生index

- **Returns**: 
	- `Object`:
		-  `bip44Path : string` : bip44形式的地址编号
		-  `address : string` : 地址
		-  `privateKey : []byte`: 地址对应的私钥 Base64 

- **Example**:

::: demo
```json tab:Request
{
    "jsonrpc": "2.0",
    "id": 2,
    "method": "wallet_deriveForIndexPath",
    "params": [
    	"vite_15391ac8b09d4e8ad78bfe5f9f9ab9682fe689572f6f53655e",
        0
    ]
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": {
        "bip44Path": "m/44'/666666'/1'",
        "address": "vite_8431a5acb599da19529c3e8bd099087a9d550fb29039dada28",
        "privateKey": "SKxAWibv4u85xMdRByCaveOwjw0bhempG9/zi59TjJUESNFMNvoE+wP/X/Zz+Tc3ObdZVO53UQT5BS8xATefbg=="
    }
}
```

:::

## wallet_deriveByFullPath
派生地址

- **Parameters**: 
	- `string` : 文件地址或者初始地址,支持更多级的地址
	- `string`: bip44形式的地址编号

- **Returns**: 
	- `Object`:
		-  `bip44Path : string` : bip44形式的地址编号
		-  `address : string` : 地址
		-  `privateKey : []byte`: 地址对应的私钥 Base64 

- **Example**:

::: demo
```json tab:Request
{
    "jsonrpc": "2.0",
    "id": 2,
    "method": "wallet_deriveByFullPath",
    "params": [
    	"vite_b1c00ae7dfd5b935550a6e2507da38886abad2351ae78d4d9a",
        "m/44'/666666'/2'/4'"
    ]
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": {
        "bip44Path": "m/44'/666666'/2'/4'",
        "address": "vite_a5efba49303b46c42c7e89b6cf5facd897d3a444fdb37af64e",
        "privateKey": "HSe4vB20dKTHYz+xzlAJ+wDhQQTJnJfemLTjbkPBb6ql/LS+lob/77NOdRfky3VWjai4g81mGR8L+goQDgEKoA=="
    }
}
```

:::

## wallet_recoverEntropyStoreFromMnemonic
助记词恢复EntropyStore

- **Parameters**: 
	- `string` : 助记词
	- `string`: 新的EntropyStore密码

- **Returns**: 
- `Object`:
	- `mnemonic : string` : 助记词
	- `primaryAddr : string` : 地址
	- `filename : string`: 文件地址  

- **Example**:

::: demo

```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 4,
	"method": "wallet_recoverEntropyStoreFromMnemonic",
	"params": [
	"utility client point estate auction region jump hat sick blast tomorrow pottery detect mixture clog able person matrix blast volume decide april congress resource",
		"123456"
	]
}

```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 4,
    "result": {
        "mnemonic": "utility client point estate auction region jump hat sick blast tomorrow pottery detect mixture clog able person matrix blast volume decide april congress resource",
        "primaryAddr": "vite_981bca7a348de85bd431b842d4b6c17044335f71e5f3da59c0",
        "filename": "/Users/xxx/Library/GVite/testdata/wallet/vite_981bca7a348de85bd431b842d4b6c17044335f71e5f3da59c0"
    }
}

```

:::
## wallet_globalCheckAddrUnlocked
全局检查地址是否解锁

- **Parameters**: `string` : `address`

- **Returns**: `bool` 是否解锁

- **Example**:

::: demo

```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 4,
	"method": "wallet_globalCheckAddrUnlocked",
	"params": [
	"vite_3fd41bb6ba4f15d5e74214a16153ff2f5abce67f73dc0dc07b"
	]
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 4,
    "result": false
}
```


:::
## wallet_isAddrUnlocked
检查某个EntropyStore下的地址是否解锁， 必须确保EntropyStore已经解锁

- **Parameters**: 
	- `string`: `Primry address` 或者 `EntropyStore abs filepath`
	- `string`:`address`： 具体的地址

- **Returns**: `bool` 是否解锁

- **Example**:

::: demo

```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 4,
	"method": "wallet_isAddrUnlocked",
	"params": [
		"vite_15391ac8b09d4e8ad78bfe5f9f9ab9682fe689572f6f53655e",
		"vite_3fd41bb6ba4f15d5e74214a16153ff2f5abce67f73dc0dc07b"
	]
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 4,
    "result": true
}
```


:::
## wallet_isUnlocked
检查EntropyStore是否解锁

- **Parameters**:  `string`: `Primry address` 或者 `EntropyStore abs filepath`

- **Returns**: `bool` 是否解锁

- **Example**:

::: demo

```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 4,
	"method": "wallet_isUnlocked",
	"params": [
		"vite_15391ac8b09d4e8ad78bfe5f9f9ab9682fe689572f6f53655e"
	]
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 4,
    "result": true
}
```

:::
## wallet_findAddr
在某个EntropyStore解锁的情况下 ，搜索某个地址

- **Parameters**:  
	- `string`: `Primry address` 或者 `EntropyStore abs filepath`
	- `string`:`address`： 具体的地址

- **Returns**:
	- `Object` 
		- `entropyStoreFile : string` : 该EntropyStore的完整路径
		- `index : uint32 `: 该地址在该Entropy下的序号
- **Example**: 

::: demo

```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 4,
	"method": "wallet_findAddr",
	"params": [
		"vite_15391ac8b09d4e8ad78bfe5f9f9ab9682fe689572f6f53655e",
		"vite_3fd41bb6ba4f15d5e74214a16153ff2f5abce67f73dc0dc07b"
	]
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 4,
    "result": {
        "entropyStoreFile": "/Users/xxx/Library/GVite/testdata/wallet/vite_15391ac8b09d4e8ad78bfe5f9f9ab9682fe689572f6f53655e",
        "index": 84
    }
}
```


:::

### wallet_globalFindAddr
全局搜索某个地址

- **Parameters**:  
	 * `string`:`address`： 具体的地址

- **Returns**:
	- `Object` 
		- `entropyStoreFile : string` : 该EntropyStore的完整路径
		- `index : uint32 `: 该地址在该Entropy下的序号
- **Example**: 

::: demo

```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 4,
	"method": "wallet_globalFindAddr",
	"params": [
	"vite_3fd41bb6ba4f15d5e74214a16153ff2f5abce67f73dc0dc07b"
	]
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 4,
    "result": {
        "entropyStoreFile": "/Users/xxx/Library/GVite/testdata/wallet/vite_15391ac8b09d4e8ad78bfe5f9f9ab9682fe689572f6f53655e",
        "index": 84
    }
}
```

:::
## wallet_createTxWithPassphrase
发送交易

- **Parameters**:  
	-  `Object`:
		- `entropystoreFile : string` :  `Primry address` 或者 `EntropyStore abs filepath`，可不填
		- `selfAddr : string address` : 自己的地址，必填
		- `toAddr : string address` : 转给谁，必填
		- `tokenTypeId : string tokentypeid` : 哪个币，必填
		- `passphrase : string` : 密码，必填
		- `amount : string bigint` : 转多少钱，必填
		- `data : string base64` : 转账留言，可不填
		- `difficulty : string bigint` : pow难度，可不填

- **Returns**: `none`


:::

### wallet_addEntropyStore
增加某个EntropyStore文件，可以用于应用非标准目录下托管的EntropyStore文件

- **Parameters**:  
	- `string`: `Primry address` 或者 `EntropyStore abs filepath`

- **Returns**: `none`
