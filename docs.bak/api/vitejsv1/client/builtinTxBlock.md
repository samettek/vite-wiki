# BuiltinTxBlock

Gvite-RPC [ledger_getLatestBlock](../../rpcv1/ledger.md)

```javascript
// For example
// ...
accountBlock.prevHash = latestBlock ? latestBlock.hash : Default_Hash;
accountBlock.height = latestBlock ? latestBlock.height + 1 : 1;
```

## How to invoke

:::warning Notice
You can leave out those optional parameters in Methods of `client.builtinTxBlock` as below when `requestType` equals to `async`. Default`requestType = async`
:::

```javascript
// ...

const block = myclient.builtinTxBlock.getAccountBlock(/** ... */);
```

## Common

### getAccountBlock
[Same as accountBlock.getAccountBlock](../tool/accountBlock.md)

### asyncAccountBlock
Get accountBlock asynchronously

- **Parameters** 
    * `__namedParameters: Object`
        - `blockType: BlockType`
        - `accountAddress: Address`
        - `fromBlockHash?: Hex`
        - `data?: Base64`
        - `message?: string`
        - `toAddress?: Address`
        - `tokenId?: TokenId`
        - `amount?: BigInt`
        - `fee?: BigInt`
        - `prevHash?: Hex`
        - `height?: Uint64`
        - `nonce?: Base64`

- **Return**:
    * Promise<`AccountBlock`>

### pow
Get the AccountBlock after running PoW successfully. *Gvite-RPC [pow_getPowNonce](../../rpcv1/pow.md)*

- **Parameters** 
    * `__namedParameters: Object`
        - `blockType: BlockType`
        - `accountAddress: Address`
        - `fromBlockHash?: Hex`
        - `data?: Base64`
        - `message?: string`
        - `toAddress?: Address`
        - `tokenId?: TokenId`
        - `amount?: BigInt`
        - `fee?: BigInt`
        - `prevHash?: Hex`
        - `height?: Uint64`
    * `difficulty` PoW-Difficulty

- **Return**:
    * Promise<`AccountBlock`>

### autoPow
Automatically run PoW to get the accountBlock, when there is no quota. *Gvite-RPC [tx_calcPoWDifficulty](../../rpcv1/tx.md) + [pow_getPowNonce](../../rpcv1/pow.md)*

- **Parameters** 
    * `__namedParameters: Object`
        - `blockType: BlockType`
        - `accountAddress: Address`
        - `fromBlockHash?: Hex`
        - `data?: Base64`
        - `message?: string`
        - `toAddress?: Address`
        - `tokenId?: TokenId`
        - `amount?: BigInt`
        - `fee?: BigInt`
        - `prevHash?: Hex`
        - `height?: Uint64`
    * `usePledgeQuota : Boolean` Whether to use quotas preferentially

- **Return**:
    * Promise<`{ accountBlock, difficulty, quota }`>

### getSendTxBlock
[Same as accountBlock.getSendTxBlock](../tool/accountBlock.md)

### asyncSendTx
Get accountBlock of sending transaction

- **Parameters** 
    * `__namedParameters: object`
        - `accountAddress: Address`
        - `toAddress: Address`
        - `tokenId: TokenId`
        - `amount: BigInt`
        - `message?: string`
        - `prevHash?: Hex`
        - `height?: Uint64`
        
- **Return**:
    * Promise<`AccountBlock`>

### getReceiveTxBlock
[Same as accountBlock.getReceiveTxBlock](../tool/accountBlock.md)

### asyncReceiveTx
Get accountBlock of receiving transaction

- **Parameters** 
    * `__namedParameters: object`
        - `accountAddress: Address`
        - `fromBlockHash: Hex`
        - `prevHash?: Hex`
        - `height?: Uint64`

- **Return**:
    * Promise<`AccountBlock`>

## Contract

### createContract
Get accountBlock of creating contract. *Gvite-RPC [contract_getCreateContractToAddress](../../rpcv1/contract.md)*

- **Parameters** 
    * `__namedParameters: object`
        - `accountAddress: Address`
        - `tokenId: TokenId` Default: Vite_TokenId
        - `amount: BigInt` Default: '0'
        - `fee: BigInt,` Default: '10000000000000000000'
        - `hexCode: Hex`
        - `abi: string`
        - `confirmTime: Uint8` Default: '0'
        - `quotaRatio: Uint8` Default: '10'
        - `seedCount: Uint8` Default: '0'
        - `params?: stirng`
        - `height?: Uint64`
        - `prevHash?: Hex`
    * `requestType?: string<'async' | 'sync'>` Default: async. Options (sync or async) when reformatting accountBlock

- **Return**:
    * Promise<`AccountBlock`>

### callContract
Get accountBlock of calling contract

- **Parameters** 
    * `__namedParameters: object`
        - `accountAddress: Address`
        - `toAddress: Address`
        - `abi: string`
        - `tokenId: TokenId` Default Vite_TokenId
        - `amount: BigInt`
        - `methodName: stirng`
        - `fee?: BigInt`
        - `params?: stirng`
        - `height?: Uint64`
        - `prevHash?: Hex`
    - `requestType?: string<'async' | 'sync'>` Default: async. Options (sync or async) when reformatting accountBlock

- **Return**:
    * Promise<`AccountBlock`>

## SBP

### SBPreg
Get accountBlock of SBP registration. *this.callContract [constant.Register_Abi](../constant/constant.md)*

- **Parameters** 
    * `__namedParameters: object`
        - `accountAddress: Address`
        - `nodeName: string`
        - `toAddress: Address`
        - `tokenId: TokenId`
        - `amount: BigInt`
        - `Gid?: string`
        - `prevHash?: Hex`
        - `height?: Uint64`
    * `requestType: string<'async' | 'sync'>` Default: async. Options (sync or async) when reformatting accountBlock.

- **Return**:
    * Promise<`AccountBlock`>

### updateReg
Get accountBlock of updating SBP registration. *this.callContract [constant.UpdateRegistration_Abi](../constant/constant.md)*

- **Parameters** 
    * `__namedParameters: object`
        - `accountAddress: Address`
        - `nodeName: string`
        - `toAddress: Address`
        - `tokenId: TokenId`
        - `Gid?: string`
        - `prevHash?: Hex`
        - `height?: Uint64`
    * `requestType: string<'async' | 'sync'>` Default: async. Options (sync or async) when reformatting accountBlock.

- **Return**:
    * Promise<`AccountBlock`>

### revokeReg
Get accountBlock of revoking SBP registration. *this.callContract [constant.CancelRegister_Abi](../constant/constant.md)*

- **Parameters** 
    * `__namedParameters: object`
        - `accountAddress: Address`
        - `nodeName: string`
        - `tokenId: TokenId`
        - `Gid?: string`
        - `prevHash?: Hex`
        - `height?: Uint64`
    - `requestType: string<'async' | 'sync'>` Default: async. Options (sync or async) when reformatting accountBlock.

- **Return**:
    * Promise<`AccountBlock`>

### retrieveReward
Get accountBlock of rewards. *this.callContract [constant.Reward_Abi](../constant/constant.md)*

- **Parameters** 
    * `__namedParameters: object`
        - `accountAddress: Address`
        - `nodeName: string`
        - `toAddress: Address`
        - `tokenId: TokenId`
        - `Gid?: string`
        - `prevHash?: Hex`
        - `height?: Uint64`
    * `requestType: string<'async' | 'sync'>` Default: async. Options (sync or async) when reformatting accountBlock.

- **Return**:
    * Promise<`AccountBlock`>

## Vote

### voting
Get accountBlock of voting. *this.callContract [constant.Vote_Abi](../constant/constant.md)*

- **Parameters** 
    * `__namedParameters: object`
        - `accountAddress: Address`
        - `nodeName: string`
        - `tokenId: TokenId`
        - `Gid?: string`
        - `prevHash?: Hex`
        - `height?: Uint64`
    - `requestType: string<'async' | 'sync'>` Default: async. Options (sync or async) when reformatting accountBlock.

- **Return**:
    * Promise<`AccountBlock`>

### revokeVoting
Get accountBlock when revoking vote. *this.callContract [constant.CancelVote_Abi](../constant/constant.md)*

- **Parameters** 
    * `__namedParameters: object`
        - `accountAddress: Address`
        - `tokenId: TokenId` Default Vite_TokenId
        - `Gid?: string`
        - `prevHash?: Hex`
        - `height?: Uint64`
    * `requestType: string<'async' | 'sync'>` Default: async. Options (sync or async) when reformatting accountBlock.

- **Return**:
    * Promise<`AccountBlock`>

## Pledge

### getQuota
Get accountBlock of quota. *this.callContract [constant.Pledge_Abi](../constant/constant.md)*

- **Parameters** 
    * `__namedParameters: object`
        - `accountAddress: Address`
        - `toAddress: Address`
        - `tokenId: TokenId`
        - `amount: BigInt`
        - `prevHash?: Hex`
        - `height?: Uint64`
    * `requestType: string<'async' | 'sync'>` Default: async. Options (sync or async) when reformatting accountBlock.

- **Return**:
    * Promise<`AccountBlock`>

### withdrawalOfQuota
Get accountBlock of withdraw quota. *this.callContract [constant.CancelPledge_Abi](../constant/constant.md)*

- **Parameters** 
    * `__namedParameters: object`
        - `accountAddress: Address`
        - `toAddress: Address`
        - `tokenId: TokenId`
        - `amount: BigInt`
        - `prevHash?: Hex`
        - `height?: Uint64`
    * `requestType: string<'async' | 'sync'>` Default: async. Options (sync or async) when reformatting accountBlock.

- **Return**:
    * Promise<`AccountBlock`>

## Mintage

### mintage
Get accountBlock of token issuance. *this.callContract [constant.Mint_Abi](../constant/constant.md)*

- **Parameters** 
    * `__namedParameters: object`
        - `accountAddress: Address`
        - `tokenName: string`
        - `decimals: uint8`
        - `totalSupply: BigInt`
        - `tokenSymbol: string`
        - `isReIssuable: boolean`
        - `maxSupply: Uint256`
        - `ownerBurnOnly: boolean`
        - `height?: Uint64`
        - `prevHash?: Hex`
        - `feeType: string<'burn' | 'stake'>` Default burn.
    * `requestType: string<'async' | 'sync'>` Default async. Options (sync or async) when reformatting accountBlock.

- **Return**:
    * Promise<`AccountBlock`>

### mintageCancelPledge
Cancel token staked accountBlock. *this.callContract [constant.CancelMintPledge_Abi](../constant/constant.md)*

- **Parameters** 
    * `__namedParameters: object`
        - `accountAddress: Address`
        - `tokenId: TokenId` Token id
        - `height?: Uint64`
        - `prevHash?: Hex`
    * `requestType: string<'async' | 'sync'>` Default async. Options (sync or async) when reformatting accountBlock

- **Return**:
    * Promise<`AccountBlock`>

### mintageIssue
Get accountBlock of additional token issuance. *this.callContract [constant.Issue_Abi](../constant/constant.md)*

- **Parameters** 
    * `__namedParameters: object`
        - `accountAddress: Address`
        - `tokenId: TokenId` Token id
        - `amount: uint64` Additional amount
        - `beneficial: Address` Additional token receiving address
        - `height?: Uint64`
        - `prevHash?: Hex`
    * `requestType: string<'async' | 'sync'>` Default async. Options (sync or async) when reformatting accountBlock

- **Return**:
    * Promise<`AccountBlock`>

### mintageBurn
Get accountBlock of token destruction. *this.callContract [constant.Burn_Abi](../constant/constant.md)*

- **Parameters** 
    * `__namedParameters: object`
        - `accountAddress: Address`
        - `tokenId: TokenId` Destroyed token id
        - `amount: uint64` Destroyed token amount
        - `height?: Uint64`
        - `prevHash?: Hex`
    - `requestType: string<'async' | 'sync'>` Default: async. Options (sync or async) when reformatting accountBlock.

- **Return**:
    * Promise<`AccountBlock`>

### changeTransferOwner
Get account block of changed transfer owner. *this.callContract [constant.TransferOwner_Abi](../constant/constant.md)*

- **Parameters** 
    * `__namedParameters: object`
        - `accountAddress: Address`
        - `newOwner: Address`
        - `tokenId: TokenId`
        - `height?: Uint64`
        - `prevHash?: Hex`
    * `requestType: string<'async' | 'sync'>` Default: async. Options (sync or async) when reformatting accountBlock

- **Return**:
    * Promise<`AccountBlock`>

### changeTokenType
Get accountBlock of changing token type, change token type from enable additional token issuance to disable. *this.callContract [constant.ChangeTokenType_Abi](../constant/constant.md)*

- **Parameters** 
    * `__namedParameters: object`
        - `accountAddress: Address`
        - `tokenId: TokenId`
        - `height?: Uint64`
        - `prevHash?: Hex`
    * `requestType: string<'async' | 'sync'>` Default: async. Options (sync or async) when reformatting accountBlock

- **Return**:
    * Promise<`AccountBlock`>
