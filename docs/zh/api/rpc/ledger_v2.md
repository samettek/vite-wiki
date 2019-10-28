---
sidebarDepth: 4
---

# Ledger
:::tip 维护者
[lyd00](https://github.com/lyd00) && [vite-crzn](https://github.com/vite-crzn)
:::


## ledger_getAccountBlocks

- **Parameters**:

  * `Address`: 账户地址
  * `Hash`: (可选)查询的起始AccountBlock的Hash。如果填写null，则默认为当前账户最新的AccountBlock的Hash
  * `TokenTypeId`: （可选）筛选出与TokenTypeId相关的AccountBlocks。如果填写null，则不筛选AccountBlocks
  * `uint64`: 查询的AccountBlock数量

- **Return**:
  * `list<AccountBlock>`: AccountBlock具体参考common_models_v2模块设计

- **Example**:

::: demo

```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 17,
	"method": "ledger_getAccountBlocks",
	"params": ["vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10", null, null, 3]
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 17,
    "result": [
        {
            "blockType": 4,
            "height": "21846",
            "hash": "7c534db9946950197dbce8654c0538278ec38e2b1bb3e229c84df26cf936a739",
            "previousHash": "5a78365f4f7e9c29d57c8f087c9691bfff63a4889cde5d03a89cb24d34abbdf3",
            "address": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
            "publicKey": "dTwfba0WWN2amkGLuMaanCNiGgJsT0ArM//zaDO3Mro=",
            "producer": "vite_8370865362e739fb71615b8b33f9e394d85743093bdfaede6c",
            "fromAddress": "vite_ea6a2f80f3469a001586cca12ac1676bb24484153c419d3db9",
            "toAddress": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
            "sendBlockHash": "37702663fbad5d405d78b9c53bd3206f4040ac17843852fef0d125973030318c",
            "tokenId": "tti_5649544520544f4b454e6e40",
            "amount": "0",
            "fee": "0",
            "data": "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA",
            "difficulty": null,
            "nonce": null,
            "signature": "FLPFkplSkoq31iJpYeNho2MyZR1BKmOD3V54U9XV3PTRWnjm5e7sOnCNWW8EgCMPbK+WYImxPueYfnZXEcnDAw==",
            "quotaByStake": "33184",
            "totalQuota": "33184",
            "vmLogHash": null,
            "triggeredSendBlockList": [
                {
                    "blockType": 2,
                    "height": "0",
                    "hash": "dda7b2c0d2d6c1c1ca3c9bdb061dd4a14ee892d29ab0cdd7fc552c1e57d6f0d2",
                    "previousHash": "0000000000000000000000000000000000000000000000000000000000000000",
                    "address": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
                    "publicKey": null,
                    "producer": "vite_3345524abf6bbe1809449224b5972c41790b6cf2e22fcb5caf",
                    "fromAddress": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
                    "toAddress": "vite_ea6a2f80f3469a001586cca12ac1676bb24484153c419d3db9",
                    "sendBlockHash": "0000000000000000000000000000000000000000000000000000000000000000",
                    "tokenId": "tti_5649544520544f4b454e6e40",
                    "amount": "61984000000000000000000",
                    "fee": "0",
                    "data": null,
                    "difficulty": null,
                    "nonce": null,
                    "signature": null,
                    "quotaByStake": "0",
                    "totalQuota": "0",
                    "vmLogHash": null,
                    "triggeredSendBlockList": null,
                    "tokenInfo": {
                        "tokenName": "VITE",
                        "tokenSymbol": "VITE",
                        "totalSupply": "999344176075854028300627070",
                        "decimals": 18,
                        "owner": "vite_0000000000000000000000000000000000000004d28108e76b",
                        "tokenId": "tti_5649544520544f4b454e6e40",
                        "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
                        "ownerBurnOnly": false,
                        "isReIssuable": true,
                        "index": 0,
                        "isOwnerBurnOnly": false
                    },
                    "confirmations": "3605345",
                    "firstSnapshotHash": "33d527c8f6ba7fdef69a6bf6171b53ae000460e08486bb25fb88d44f4c789147",
                    "receiveBlockHeight": "38",
                    "receiveBlockHash": "7a6e4ab1420c3a1d319431ba77757f780578622c938afd1eb7bc8bdc4fe947fc",
                    "timestamp": 1562208615
                }
            ],
            "tokenInfo": {
                "tokenName": "VITE",
                "tokenSymbol": "VITE",
                "totalSupply": "999344176075854028300627070",
                "decimals": 18,
                "owner": "vite_0000000000000000000000000000000000000004d28108e76b",
                "tokenId": "tti_5649544520544f4b454e6e40",
                "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
                "ownerBurnOnly": false,
                "isReIssuable": true,
                "index": 0,
                "isOwnerBurnOnly": false
            },
            "confirmations": "3605345",
            "firstSnapshotHash": "33d527c8f6ba7fdef69a6bf6171b53ae000460e08486bb25fb88d44f4c789147",
            "receiveBlockHeight": null,
            "receiveBlockHash": null,
            "timestamp": 1562208615
        },
        {
            "blockType": 4,
            "height": "21845",
            "hash": "5a78365f4f7e9c29d57c8f087c9691bfff63a4889cde5d03a89cb24d34abbdf3",
            "previousHash": "4d2c1bc90e235b5a5fdec69bda0ebe6494f0c01b2af53accaa1beff00b9fa976",
            "address": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
            "publicKey": "1cgxEjT1L3x+mPzKsBnV4DSPiU+RTmY7akbrTCxcArE=",
            "producer": "vite_165a295e214421ef1276e79990533953e901291d29b2d4851f",
            "fromAddress": "vite_f74d18fc6431cb9d813c62a47a9063c4b9488219dc22c2736d",
            "toAddress": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
            "sendBlockHash": "fc2c937d542fd5b02aeadb0acb3a2f015e1cc92b94873304ab8642f703e4c059",
            "tokenId": "tti_5649544520544f4b454e6e40",
            "amount": "16000000000000000000",
            "fee": "0",
            "data": "eo15oJWpGqoIm4hP9riEZRvcSXLUs8QKC7XBStD6yyAA",
            "difficulty": null,
            "nonce": null,
            "signature": "XccA38Yxcgt1EZDdSNrgcZNC3YJ088HKNBdTt72noa1F+SbEBxmWnUjSKj5h/FlO/3SXrYnt0rU97L8JkY3lBA==",
            "quotaByStake": "105710",
            "totalQuota": "105710",
            "vmLogHash": "56d05270b0d62a8dac3a01908177ed6e47899eced76bc9fa7716e808d6068705",
            "triggeredSendBlockList": [
                {
                    "blockType": 2,
                    "height": "0",
                    "hash": "6cb62e1576bfc6652251a89b540972aceaa678f51ef4b92156b5d1a387f8b178",
                    "previousHash": "0000000000000000000000000000000000000000000000000000000000000000",
                    "address": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
                    "publicKey": null,
                    "producer": "vite_3345524abf6bbe1809449224b5972c41790b6cf2e22fcb5caf",
                    "fromAddress": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
                    "toAddress": "vite_f74d18fc6431cb9d813c62a47a9063c4b9488219dc22c2736d",
                    "sendBlockHash": "0000000000000000000000000000000000000000000000000000000000000000",
                    "tokenId": "tti_5649544520544f4b454e6e40",
                    "amount": "30000000000000000000",
                    "fee": "0",
                    "data": null,
                    "difficulty": null,
                    "nonce": null,
                    "signature": null,
                    "quotaByStake": "0",
                    "totalQuota": "0",
                    "vmLogHash": null,
                    "triggeredSendBlockList": null,
                    "tokenInfo": {
                        "tokenName": "VITE",
                        "tokenSymbol": "VITE",
                        "totalSupply": "999344176075854028300627070",
                        "decimals": 18,
                        "owner": "vite_0000000000000000000000000000000000000004d28108e76b",
                        "tokenId": "tti_5649544520544f4b454e6e40",
                        "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
                        "ownerBurnOnly": false,
                        "isReIssuable": true,
                        "index": 0,
                        "isOwnerBurnOnly": false
                    },
                    "confirmations": "3607047",
                    "firstSnapshotHash": "462da9711b54219036d26b6cf8533a510e75680089a2a1ec54201bf14bdce16c",
                    "receiveBlockHeight": "547",
                    "receiveBlockHash": "3536cd55cb61723bf29d1ac193d39e6f049c2475370a91b8a68a7750e5d57bf5",
                    "timestamp": 1562206877
                }
            ],
            "tokenInfo": {
                "tokenName": "VITE",
                "tokenSymbol": "VITE",
                "totalSupply": "999344176075854028300627070",
                "decimals": 18,
                "owner": "vite_0000000000000000000000000000000000000004d28108e76b",
                "tokenId": "tti_5649544520544f4b454e6e40",
                "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
                "ownerBurnOnly": false,
                "isReIssuable": true,
                "index": 0,
                "isOwnerBurnOnly": false
            },
            "confirmations": "3607047",
            "firstSnapshotHash": "462da9711b54219036d26b6cf8533a510e75680089a2a1ec54201bf14bdce16c",
            "receiveBlockHeight": null,
            "receiveBlockHash": null,
            "timestamp": 1562206877
        },
        {
            "blockType": 4,
            "height": "21844",
            "hash": "4d2c1bc90e235b5a5fdec69bda0ebe6494f0c01b2af53accaa1beff00b9fa976",
            "previousHash": "b91ce0f015e7d89e87925762a8996326a979b27f7d2d7ed8d22c327937584ee4",
            "address": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
            "publicKey": "O4QZHbAsZQ4KHHzxEPuLdnVT+DiJomRrG6+zYSUSZRc=",
            "producer": "vite_10513d54e0c38a304ad9e7902c82277328b4df76dd31871f37",
            "fromAddress": "vite_f74d18fc6431cb9d813c62a47a9063c4b9488219dc22c2736d",
            "toAddress": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
            "sendBlockHash": "080b41f1cb5194df8d5b8903a6ed987f36291d172f93a8c67c75a87a3769308d",
            "tokenId": "tti_5649544520544f4b454e6e40",
            "amount": "16000000000000000000",
            "fee": "0",
            "data": "wao4N2P26LmbJEmmYuINTMJoQ1MX0+EWEXSTK5CHCh4A",
            "difficulty": null,
            "nonce": null,
            "signature": "RUo6punEG3XzqO/2bL3vOlOMXM9xpvUxToEBgqtP7GLYYr/9ZxrK5GamaaUHA/OyXq8jwrrX5hf1z/F8nT1BCw==",
            "quotaByStake": "116522",
            "totalQuota": "116522",
            "vmLogHash": "e449ac3a53689813ef73d149f8ebb83f3fdc77812d21aaf399575dca353de895",
            "triggeredSendBlockList": [
                {
                    "blockType": 2,
                    "height": "0",
                    "hash": "1a92be3b93725056f9df1906e1fcd1fc123f704d879b020f836daa41eacc42dd",
                    "previousHash": "0000000000000000000000000000000000000000000000000000000000000000",
                    "address": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
                    "publicKey": null,
                    "producer": "vite_3345524abf6bbe1809449224b5972c41790b6cf2e22fcb5caf",
                    "fromAddress": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
                    "toAddress": "vite_f74d18fc6431cb9d813c62a47a9063c4b9488219dc22c2736d",
                    "sendBlockHash": "0000000000000000000000000000000000000000000000000000000000000000",
                    "tokenId": "tti_5649544520544f4b454e6e40",
                    "amount": "4000000000000000000",
                    "fee": "0",
                    "data": null,
                    "difficulty": null,
                    "nonce": null,
                    "signature": null,
                    "quotaByStake": "0",
                    "totalQuota": "0",
                    "vmLogHash": null,
                    "triggeredSendBlockList": null,
                    "tokenInfo": {
                        "tokenName": "VITE",
                        "tokenSymbol": "VITE",
                        "totalSupply": "999344176075854028300627070",
                        "decimals": 18,
                        "owner": "vite_0000000000000000000000000000000000000004d28108e76b",
                        "tokenId": "tti_5649544520544f4b454e6e40",
                        "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
                        "ownerBurnOnly": false,
                        "isReIssuable": true,
                        "index": 0,
                        "isOwnerBurnOnly": false
                    },
                    "confirmations": "3607067",
                    "firstSnapshotHash": "dd23c7d1c866311a41977fc008830558ad34d9bcd790ce4dad6367ee52dfedc6",
                    "receiveBlockHeight": "545",
                    "receiveBlockHash": "6172267c757d6234c833aaa05f393ba4a733e584a83ac8c43acf2c6c2da8510f",
                    "timestamp": 1562206856
                }
            ],
            "tokenInfo": {
                "tokenName": "VITE",
                "tokenSymbol": "VITE",
                "totalSupply": "999344176075854028300627070",
                "decimals": 18,
                "owner": "vite_0000000000000000000000000000000000000004d28108e76b",
                "tokenId": "tti_5649544520544f4b454e6e40",
                "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
                "ownerBurnOnly": false,
                "isReIssuable": true,
                "index": 0,
                "isOwnerBurnOnly": false
            },
            "confirmations": "3607067",
            "firstSnapshotHash": "dd23c7d1c866311a41977fc008830558ad34d9bcd790ce4dad6367ee52dfedc6",
            "receiveBlockHeight": null,
            "receiveBlockHash": null,
            "timestamp": 1562206856
        }
    ]
}
```

:::

## ledger_getAccountBlockByHash

- **Parameters**:
  * `Hash`: 查询的AccountBlock的Hash

- **Return**:
  * `AccountBlock`: AccountBlock具体参考common_models_v2模块设计

- **Example**:

::: demo

```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 17,
	"method": "ledger_getAccountBlockByHash",
	"params": ["7c534db9946950197dbce8654c0538278ec38e2b1bb3e229c84df26cf936a739"]
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 17,
    "result": {
        "blockType": 4,
        "height": "21846",
        "hash": "7c534db9946950197dbce8654c0538278ec38e2b1bb3e229c84df26cf936a739",
        "previousHash": "5a78365f4f7e9c29d57c8f087c9691bfff63a4889cde5d03a89cb24d34abbdf3",
        "address": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
        "publicKey": "dTwfba0WWN2amkGLuMaanCNiGgJsT0ArM//zaDO3Mro=",
        "producer": "vite_8370865362e739fb71615b8b33f9e394d85743093bdfaede6c",
        "fromAddress": "vite_ea6a2f80f3469a001586cca12ac1676bb24484153c419d3db9",
        "toAddress": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
        "sendBlockHash": "37702663fbad5d405d78b9c53bd3206f4040ac17843852fef0d125973030318c",
        "tokenId": "tti_5649544520544f4b454e6e40",
        "amount": "0",
        "fee": "0",
        "data": "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA",
        "difficulty": null,
        "nonce": null,
        "signature": "FLPFkplSkoq31iJpYeNho2MyZR1BKmOD3V54U9XV3PTRWnjm5e7sOnCNWW8EgCMPbK+WYImxPueYfnZXEcnDAw==",
        "quotaByStake": "33184",
        "totalQuota": "33184",
        "vmLogHash": null,
        "triggeredSendBlockList": [
            {
                "blockType": 2,
                "height": "0",
                "hash": "dda7b2c0d2d6c1c1ca3c9bdb061dd4a14ee892d29ab0cdd7fc552c1e57d6f0d2",
                "previousHash": "0000000000000000000000000000000000000000000000000000000000000000",
                "address": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
                "publicKey": null,
                "producer": "vite_3345524abf6bbe1809449224b5972c41790b6cf2e22fcb5caf",
                "fromAddress": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
                "toAddress": "vite_ea6a2f80f3469a001586cca12ac1676bb24484153c419d3db9",
                "sendBlockHash": "0000000000000000000000000000000000000000000000000000000000000000",
                "tokenId": "tti_5649544520544f4b454e6e40",
                "amount": "61984000000000000000000",
                "fee": "0",
                "data": null,
                "difficulty": null,
                "nonce": null,
                "signature": null,
                "quotaByStake": "0",
                "totalQuota": "0",
                "vmLogHash": null,
                "triggeredSendBlockList": null,
                "tokenInfo": {
                    "tokenName": "VITE",
                    "tokenSymbol": "VITE",
                    "totalSupply": "999369292029736282857580488",
                    "decimals": 18,
                    "owner": "vite_0000000000000000000000000000000000000004d28108e76b",
                    "tokenId": "tti_5649544520544f4b454e6e40",
                    "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
                    "ownerBurnOnly": false,
                    "isReIssuable": true,
                    "index": 0,
                    "isOwnerBurnOnly": false
                },
                "confirmations": "3622745",
                "firstSnapshotHash": "33d527c8f6ba7fdef69a6bf6171b53ae000460e08486bb25fb88d44f4c789147",
                "receiveBlockHeight": "38",
                "receiveBlockHash": "7a6e4ab1420c3a1d319431ba77757f780578622c938afd1eb7bc8bdc4fe947fc",
                "timestamp": 1562208615
            }
        ],
        "tokenInfo": {
            "tokenName": "VITE",
            "tokenSymbol": "VITE",
            "totalSupply": "999369292029736282857580488",
            "decimals": 18,
            "owner": "vite_0000000000000000000000000000000000000004d28108e76b",
            "tokenId": "tti_5649544520544f4b454e6e40",
            "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
            "ownerBurnOnly": false,
            "isReIssuable": true,
            "index": 0,
            "isOwnerBurnOnly": false
        },
        "confirmations": "3622745",
        "firstSnapshotHash": "33d527c8f6ba7fdef69a6bf6171b53ae000460e08486bb25fb88d44f4c789147",
        "receiveBlockHeight": null,
        "receiveBlockHash": null,
        "timestamp": 1562208615
    }
}
```

:::

## ledger_getAccountBlockByHeight

- **Parameters**:
  * `Address`: 查询账号地址
  * `uint64`: 查询的AccountBlock的高度

- **Return**:
  * `AccountBlock`: AccountBlock具体参考common_models_v2模块设计

- **Example**:

::: demo

```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 17,
	"method": "ledger_getAccountBlockByHeight",
	"params": ["vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10", 21846]
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 17,
    "result": {
        "blockType": 4,
        "height": "21846",
        "hash": "7c534db9946950197dbce8654c0538278ec38e2b1bb3e229c84df26cf936a739",
        "previousHash": "5a78365f4f7e9c29d57c8f087c9691bfff63a4889cde5d03a89cb24d34abbdf3",
        "address": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
        "publicKey": "dTwfba0WWN2amkGLuMaanCNiGgJsT0ArM//zaDO3Mro=",
        "producer": "vite_8370865362e739fb71615b8b33f9e394d85743093bdfaede6c",
        "fromAddress": "vite_ea6a2f80f3469a001586cca12ac1676bb24484153c419d3db9",
        "toAddress": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
        "sendBlockHash": "37702663fbad5d405d78b9c53bd3206f4040ac17843852fef0d125973030318c",
        "tokenId": "tti_5649544520544f4b454e6e40",
        "amount": "0",
        "fee": "0",
        "data": "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA",
        "difficulty": null,
        "nonce": null,
        "signature": "FLPFkplSkoq31iJpYeNho2MyZR1BKmOD3V54U9XV3PTRWnjm5e7sOnCNWW8EgCMPbK+WYImxPueYfnZXEcnDAw==",
        "quotaByStake": "33184",
        "totalQuota": "33184",
        "vmLogHash": null,
        "triggeredSendBlockList": [
            {
                "blockType": 2,
                "height": "0",
                "hash": "dda7b2c0d2d6c1c1ca3c9bdb061dd4a14ee892d29ab0cdd7fc552c1e57d6f0d2",
                "previousHash": "0000000000000000000000000000000000000000000000000000000000000000",
                "address": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
                "publicKey": null,
                "producer": "vite_3345524abf6bbe1809449224b5972c41790b6cf2e22fcb5caf",
                "fromAddress": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
                "toAddress": "vite_ea6a2f80f3469a001586cca12ac1676bb24484153c419d3db9",
                "sendBlockHash": "0000000000000000000000000000000000000000000000000000000000000000",
                "tokenId": "tti_5649544520544f4b454e6e40",
                "amount": "61984000000000000000000",
                "fee": "0",
                "data": null,
                "difficulty": null,
                "nonce": null,
                "signature": null,
                "quotaByStake": "0",
                "totalQuota": "0",
                "vmLogHash": null,
                "triggeredSendBlockList": null,
                "tokenInfo": {
                    "tokenName": "VITE",
                    "tokenSymbol": "VITE",
                    "totalSupply": "999998383901711633310557566",
                    "decimals": 18,
                    "owner": "vite_0000000000000000000000000000000000000004d28108e76b",
                    "tokenId": "tti_5649544520544f4b454e6e40",
                    "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
                    "ownerBurnOnly": false,
                    "isReIssuable": true,
                    "index": 0,
                    "isOwnerBurnOnly": false
                },
                "confirmations": "4299959",
                "firstSnapshotHash": "33d527c8f6ba7fdef69a6bf6171b53ae000460e08486bb25fb88d44f4c789147",
                "receiveBlockHeight": "38",
                "receiveBlockHash": "7a6e4ab1420c3a1d319431ba77757f780578622c938afd1eb7bc8bdc4fe947fc",
                "timestamp": 1562208615
            }
        ],
        "tokenInfo": {
            "tokenName": "VITE",
            "tokenSymbol": "VITE",
            "totalSupply": "999998383901711633310557566",
            "decimals": 18,
            "owner": "vite_0000000000000000000000000000000000000004d28108e76b",
            "tokenId": "tti_5649544520544f4b454e6e40",
            "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
            "ownerBurnOnly": false,
            "isReIssuable": true,
            "index": 0,
            "isOwnerBurnOnly": false
        },
        "confirmations": "4299954",
        "firstSnapshotHash": "33d527c8f6ba7fdef69a6bf6171b53ae000460e08486bb25fb88d44f4c789147",
        "receiveBlockHeight": null,
        "receiveBlockHash": null,
        "timestamp": 1562208615
    }
}
```

:::

## ledger_getAccountBlocksByAddress

- **Parameters**:
  * `Address`: 查询账号地址
  * `uint64`: 分页查询AccountBlocks的页数, 顺序是按AccountBlocks的高度从高到低
  * `uint64`: 分页查询AccountBlocks的个数, 顺序是按AccountBlocks的高度从高到低

- **Return**:
  * List<`AccountBlock`>: AccountBlock具体参考common_models_v2模块设计

- **Example**:

::: demo

```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 17,
	"method": "ledger_getAccountBlocksByAddress",
	"params": ["vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10", 0, 3]
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 17,
    "result": [
        {
            "blockType": 4,
            "height": "21846",
            "hash": "7c534db9946950197dbce8654c0538278ec38e2b1bb3e229c84df26cf936a739",
            "previousHash": "5a78365f4f7e9c29d57c8f087c9691bfff63a4889cde5d03a89cb24d34abbdf3",
            "address": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
            "publicKey": "dTwfba0WWN2amkGLuMaanCNiGgJsT0ArM//zaDO3Mro=",
            "producer": "vite_8370865362e739fb71615b8b33f9e394d85743093bdfaede6c",
            "fromAddress": "vite_ea6a2f80f3469a001586cca12ac1676bb24484153c419d3db9",
            "toAddress": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
            "sendBlockHash": "37702663fbad5d405d78b9c53bd3206f4040ac17843852fef0d125973030318c",
            "tokenId": "tti_5649544520544f4b454e6e40",
            "amount": "0",
            "fee": "0",
            "data": "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA",
            "difficulty": null,
            "nonce": null,
            "signature": "FLPFkplSkoq31iJpYeNho2MyZR1BKmOD3V54U9XV3PTRWnjm5e7sOnCNWW8EgCMPbK+WYImxPueYfnZXEcnDAw==",
            "quotaByStake": "33184",
            "totalQuota": "33184",
            "vmLogHash": null,
            "triggeredSendBlockList": [
                {
                    "blockType": 2,
                    "height": "0",
                    "hash": "dda7b2c0d2d6c1c1ca3c9bdb061dd4a14ee892d29ab0cdd7fc552c1e57d6f0d2",
                    "previousHash": "0000000000000000000000000000000000000000000000000000000000000000",
                    "address": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
                    "publicKey": null,
                    "producer": "vite_3345524abf6bbe1809449224b5972c41790b6cf2e22fcb5caf",
                    "fromAddress": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
                    "toAddress": "vite_ea6a2f80f3469a001586cca12ac1676bb24484153c419d3db9",
                    "sendBlockHash": "0000000000000000000000000000000000000000000000000000000000000000",
                    "tokenId": "tti_5649544520544f4b454e6e40",
                    "amount": "61984000000000000000000",
                    "fee": "0",
                    "data": null,
                    "difficulty": null,
                    "nonce": null,
                    "signature": null,
                    "quotaByStake": "0",
                    "totalQuota": "0",
                    "vmLogHash": null,
                    "triggeredSendBlockList": null,
                    "tokenInfo": {
                        "tokenName": "VITE",
                        "tokenSymbol": "VITE",
                        "totalSupply": "1000032113155962510026863838",
                        "decimals": 18,
                        "owner": "vite_0000000000000000000000000000000000000004d28108e76b",
                        "tokenId": "tti_5649544520544f4b454e6e40",
                        "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
                        "ownerBurnOnly": false,
                        "isReIssuable": true,
                        "index": 0,
                        "isOwnerBurnOnly": false
                    },
                    "confirmations": "4368185",
                    "firstSnapshotHash": "33d527c8f6ba7fdef69a6bf6171b53ae000460e08486bb25fb88d44f4c789147",
                    "receiveBlockHeight": "38",
                    "receiveBlockHash": "7a6e4ab1420c3a1d319431ba77757f780578622c938afd1eb7bc8bdc4fe947fc",
                    "timestamp": 1562208615
                }
            ],
            "tokenInfo": {
                "tokenName": "VITE",
                "tokenSymbol": "VITE",
                "totalSupply": "1000032113155962510026863838",
                "decimals": 18,
                "owner": "vite_0000000000000000000000000000000000000004d28108e76b",
                "tokenId": "tti_5649544520544f4b454e6e40",
                "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
                "ownerBurnOnly": false,
                "isReIssuable": true,
                "index": 0,
                "isOwnerBurnOnly": false
            },
            "confirmations": "4368185",
            "firstSnapshotHash": "33d527c8f6ba7fdef69a6bf6171b53ae000460e08486bb25fb88d44f4c789147",
            "receiveBlockHeight": null,
            "receiveBlockHash": null,
            "timestamp": 1562208615
        },
        {
            "blockType": 4,
            "height": "21845",
            "hash": "5a78365f4f7e9c29d57c8f087c9691bfff63a4889cde5d03a89cb24d34abbdf3",
            "previousHash": "4d2c1bc90e235b5a5fdec69bda0ebe6494f0c01b2af53accaa1beff00b9fa976",
            "address": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
            "publicKey": "1cgxEjT1L3x+mPzKsBnV4DSPiU+RTmY7akbrTCxcArE=",
            "producer": "vite_165a295e214421ef1276e79990533953e901291d29b2d4851f",
            "fromAddress": "vite_f74d18fc6431cb9d813c62a47a9063c4b9488219dc22c2736d",
            "toAddress": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
            "sendBlockHash": "fc2c937d542fd5b02aeadb0acb3a2f015e1cc92b94873304ab8642f703e4c059",
            "tokenId": "tti_5649544520544f4b454e6e40",
            "amount": "16000000000000000000",
            "fee": "0",
            "data": "eo15oJWpGqoIm4hP9riEZRvcSXLUs8QKC7XBStD6yyAA",
            "difficulty": null,
            "nonce": null,
            "signature": "XccA38Yxcgt1EZDdSNrgcZNC3YJ088HKNBdTt72noa1F+SbEBxmWnUjSKj5h/FlO/3SXrYnt0rU97L8JkY3lBA==",
            "quotaByStake": "105710",
            "totalQuota": "105710",
            "vmLogHash": "56d05270b0d62a8dac3a01908177ed6e47899eced76bc9fa7716e808d6068705",
            "triggeredSendBlockList": [
                {
                    "blockType": 2,
                    "height": "0",
                    "hash": "6cb62e1576bfc6652251a89b540972aceaa678f51ef4b92156b5d1a387f8b178",
                    "previousHash": "0000000000000000000000000000000000000000000000000000000000000000",
                    "address": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
                    "publicKey": null,
                    "producer": "vite_3345524abf6bbe1809449224b5972c41790b6cf2e22fcb5caf",
                    "fromAddress": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
                    "toAddress": "vite_f74d18fc6431cb9d813c62a47a9063c4b9488219dc22c2736d",
                    "sendBlockHash": "0000000000000000000000000000000000000000000000000000000000000000",
                    "tokenId": "tti_5649544520544f4b454e6e40",
                    "amount": "30000000000000000000",
                    "fee": "0",
                    "data": null,
                    "difficulty": null,
                    "nonce": null,
                    "signature": null,
                    "quotaByStake": "0",
                    "totalQuota": "0",
                    "vmLogHash": null,
                    "triggeredSendBlockList": null,
                    "tokenInfo": {
                        "tokenName": "VITE",
                        "tokenSymbol": "VITE",
                        "totalSupply": "1000032113155962510026863838",
                        "decimals": 18,
                        "owner": "vite_0000000000000000000000000000000000000004d28108e76b",
                        "tokenId": "tti_5649544520544f4b454e6e40",
                        "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
                        "ownerBurnOnly": false,
                        "isReIssuable": true,
                        "index": 0,
                        "isOwnerBurnOnly": false
                    },
                    "confirmations": "4369892",
                    "firstSnapshotHash": "462da9711b54219036d26b6cf8533a510e75680089a2a1ec54201bf14bdce16c",
                    "receiveBlockHeight": "547",
                    "receiveBlockHash": "3536cd55cb61723bf29d1ac193d39e6f049c2475370a91b8a68a7750e5d57bf5",
                    "timestamp": 1562206877
                }
            ],
            "tokenInfo": {
                "tokenName": "VITE",
                "tokenSymbol": "VITE",
                "totalSupply": "1000032113155962510026863838",
                "decimals": 18,
                "owner": "vite_0000000000000000000000000000000000000004d28108e76b",
                "tokenId": "tti_5649544520544f4b454e6e40",
                "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
                "ownerBurnOnly": false,
                "isReIssuable": true,
                "index": 0,
                "isOwnerBurnOnly": false
            },
            "confirmations": "4369891",
            "firstSnapshotHash": "462da9711b54219036d26b6cf8533a510e75680089a2a1ec54201bf14bdce16c",
            "receiveBlockHeight": null,
            "receiveBlockHash": null,
            "timestamp": 1562206877
        },
        {
            "blockType": 4,
            "height": "21844",
            "hash": "4d2c1bc90e235b5a5fdec69bda0ebe6494f0c01b2af53accaa1beff00b9fa976",
            "previousHash": "b91ce0f015e7d89e87925762a8996326a979b27f7d2d7ed8d22c327937584ee4",
            "address": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
            "publicKey": "O4QZHbAsZQ4KHHzxEPuLdnVT+DiJomRrG6+zYSUSZRc=",
            "producer": "vite_10513d54e0c38a304ad9e7902c82277328b4df76dd31871f37",
            "fromAddress": "vite_f74d18fc6431cb9d813c62a47a9063c4b9488219dc22c2736d",
            "toAddress": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
            "sendBlockHash": "080b41f1cb5194df8d5b8903a6ed987f36291d172f93a8c67c75a87a3769308d",
            "tokenId": "tti_5649544520544f4b454e6e40",
            "amount": "16000000000000000000",
            "fee": "0",
            "data": "wao4N2P26LmbJEmmYuINTMJoQ1MX0+EWEXSTK5CHCh4A",
            "difficulty": null,
            "nonce": null,
            "signature": "RUo6punEG3XzqO/2bL3vOlOMXM9xpvUxToEBgqtP7GLYYr/9ZxrK5GamaaUHA/OyXq8jwrrX5hf1z/F8nT1BCw==",
            "quotaByStake": "116522",
            "totalQuota": "116522",
            "vmLogHash": "e449ac3a53689813ef73d149f8ebb83f3fdc77812d21aaf399575dca353de895",
            "triggeredSendBlockList": [
                {
                    "blockType": 2,
                    "height": "0",
                    "hash": "1a92be3b93725056f9df1906e1fcd1fc123f704d879b020f836daa41eacc42dd",
                    "previousHash": "0000000000000000000000000000000000000000000000000000000000000000",
                    "address": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
                    "publicKey": null,
                    "producer": "vite_3345524abf6bbe1809449224b5972c41790b6cf2e22fcb5caf",
                    "fromAddress": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
                    "toAddress": "vite_f74d18fc6431cb9d813c62a47a9063c4b9488219dc22c2736d",
                    "sendBlockHash": "0000000000000000000000000000000000000000000000000000000000000000",
                    "tokenId": "tti_5649544520544f4b454e6e40",
                    "amount": "4000000000000000000",
                    "fee": "0",
                    "data": null,
                    "difficulty": null,
                    "nonce": null,
                    "signature": null,
                    "quotaByStake": "0",
                    "totalQuota": "0",
                    "vmLogHash": null,
                    "triggeredSendBlockList": null,
                    "tokenInfo": {
                        "tokenName": "VITE",
                        "tokenSymbol": "VITE",
                        "totalSupply": "1000032113155962510026863838",
                        "decimals": 18,
                        "owner": "vite_0000000000000000000000000000000000000004d28108e76b",
                        "tokenId": "tti_5649544520544f4b454e6e40",
                        "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
                        "ownerBurnOnly": false,
                        "isReIssuable": true,
                        "index": 0,
                        "isOwnerBurnOnly": false
                    },
                    "confirmations": "4369916",
                    "firstSnapshotHash": "dd23c7d1c866311a41977fc008830558ad34d9bcd790ce4dad6367ee52dfedc6",
                    "receiveBlockHeight": "545",
                    "receiveBlockHash": "6172267c757d6234c833aaa05f393ba4a733e584a83ac8c43acf2c6c2da8510f",
                    "timestamp": 1562206856
                }
            ],
            "tokenInfo": {
                "tokenName": "VITE",
                "tokenSymbol": "VITE",
                "totalSupply": "1000032113155962510026863838",
                "decimals": 18,
                "owner": "vite_0000000000000000000000000000000000000004d28108e76b",
                "tokenId": "tti_5649544520544f4b454e6e40",
                "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
                "ownerBurnOnly": false,
                "isReIssuable": true,
                "index": 0,
                "isOwnerBurnOnly": false
            },
            "confirmations": "4369913",
            "firstSnapshotHash": "dd23c7d1c866311a41977fc008830558ad34d9bcd790ce4dad6367ee52dfedc6",
            "receiveBlockHeight": null,
            "receiveBlockHash": null,
            "timestamp": 1562206856
        }
    ]
}
```

:::

## ledger_getLatestAccountBlock

- **Parameters**:
  * `Address`: 查询账号地址
  
- **Return**:
  * `AccountBlock`: AccountBlock具体参考common_models_v2模块设计

- **Example**:

::: demo

```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 17,
	"method": "ledger_getLatestAccountBlock",
	"params": ["vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10"]
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 17,
    "result": {
        "blockType": 4,
        "height": "21846",
        "hash": "7c534db9946950197dbce8654c0538278ec38e2b1bb3e229c84df26cf936a739",
        "previousHash": "5a78365f4f7e9c29d57c8f087c9691bfff63a4889cde5d03a89cb24d34abbdf3",
        "address": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
        "publicKey": "dTwfba0WWN2amkGLuMaanCNiGgJsT0ArM//zaDO3Mro=",
        "producer": "vite_8370865362e739fb71615b8b33f9e394d85743093bdfaede6c",
        "fromAddress": "vite_ea6a2f80f3469a001586cca12ac1676bb24484153c419d3db9",
        "toAddress": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
        "sendBlockHash": "37702663fbad5d405d78b9c53bd3206f4040ac17843852fef0d125973030318c",
        "tokenId": "tti_5649544520544f4b454e6e40",
        "amount": "0",
        "fee": "0",
        "data": "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA",
        "difficulty": null,
        "nonce": null,
        "signature": "FLPFkplSkoq31iJpYeNho2MyZR1BKmOD3V54U9XV3PTRWnjm5e7sOnCNWW8EgCMPbK+WYImxPueYfnZXEcnDAw==",
        "quotaByStake": "33184",
        "totalQuota": "33184",
        "vmLogHash": null,
        "triggeredSendBlockList": [
            {
                "blockType": 2,
                "height": "0",
                "hash": "dda7b2c0d2d6c1c1ca3c9bdb061dd4a14ee892d29ab0cdd7fc552c1e57d6f0d2",
                "previousHash": "0000000000000000000000000000000000000000000000000000000000000000",
                "address": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
                "publicKey": null,
                "producer": "vite_3345524abf6bbe1809449224b5972c41790b6cf2e22fcb5caf",
                "fromAddress": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
                "toAddress": "vite_ea6a2f80f3469a001586cca12ac1676bb24484153c419d3db9",
                "sendBlockHash": "0000000000000000000000000000000000000000000000000000000000000000",
                "tokenId": "tti_5649544520544f4b454e6e40",
                "amount": "61984000000000000000000",
                "fee": "0",
                "data": null,
                "difficulty": null,
                "nonce": null,
                "signature": null,
                "quotaByStake": "0",
                "totalQuota": "0",
                "vmLogHash": null,
                "triggeredSendBlockList": null,
                "tokenInfo": {
                    "tokenName": "VITE",
                    "tokenSymbol": "VITE",
                    "totalSupply": "1000045942413038967590996145",
                    "decimals": 18,
                    "owner": "vite_0000000000000000000000000000000000000004d28108e76b",
                    "tokenId": "tti_5649544520544f4b454e6e40",
                    "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
                    "ownerBurnOnly": false,
                    "isReIssuable": true,
                    "index": 0,
                    "isOwnerBurnOnly": false
                },
                "confirmations": "4420249",
                "firstSnapshotHash": "33d527c8f6ba7fdef69a6bf6171b53ae000460e08486bb25fb88d44f4c789147",
                "receiveBlockHeight": "38",
                "receiveBlockHash": "7a6e4ab1420c3a1d319431ba77757f780578622c938afd1eb7bc8bdc4fe947fc",
                "timestamp": 1562208615
            }
        ],
        "tokenInfo": {
            "tokenName": "VITE",
            "tokenSymbol": "VITE",
            "totalSupply": "1000045942413038967590996145",
            "decimals": 18,
            "owner": "vite_0000000000000000000000000000000000000004d28108e76b",
            "tokenId": "tti_5649544520544f4b454e6e40",
            "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
            "ownerBurnOnly": false,
            "isReIssuable": true,
            "index": 0,
            "isOwnerBurnOnly": false
        },
        "confirmations": "4420245",
        "firstSnapshotHash": "33d527c8f6ba7fdef69a6bf6171b53ae000460e08486bb25fb88d44f4c789147",
        "receiveBlockHeight": null,
        "receiveBlockHash": null,
        "timestamp": 1562208615
    }
}
```

:::

## ledger_getAccountInfoByAddress

- **Parameters**:
  * `Address`: 查询账号地址
  
- **Return**:
  * `AccountInfo` AccountInfo具体参考common_models_v2模块设计

- **Example**:
::: demo

```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 17,
	"method": "ledger_getAccountInfoByAddress",
	"params": ["vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10"]
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 17,
    "result": {
        "address": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
        "blockCount": "21846",
        "balanceInfoMap": {
            "tti_5649544520544f4b454e6e40": {
                "tokenInfo": {
                    "tokenName": "VITE",
                    "tokenSymbol": "VITE",
                    "totalSupply": "1001699224353751966255398604",
                    "decimals": 18,
                    "owner": "vite_0000000000000000000000000000000000000004d28108e76b",
                    "tokenId": "tti_5649544520544f4b454e6e40",
                    "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
                    "ownerBurnOnly": false,
                    "isReIssuable": true,
                    "index": 0,
                    "isOwnerBurnOnly": false
                },
                "balance": "0"
            }
        }
    }
}
```

:::

## ledger_getLatestSnapshotHash

- **Return**:
  * `Hash` 最新的snapshot block的hash

- **Example**:
::: demo

```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 17,
	"method": "ledger_getLatestSnapshotHash"
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 17,
    "result": "d580deefe3ce5ec9340d163543f93130f2e40ccd4546da8246baba6d0dc25d1f"
}
```
:::

## ledger_sendRawTransaction

- **Parameters**: `Object`: `AccountBlock`
  * `blockType`: `byte` 交易类型 `必填`
  * `height`: `string` 高度 `必填`
  * `hash`: `Hash` 该交易的Hash `必填`
  * `previousHash`: `Hash`  出块账户链上上一个块的哈希 `必填` 如果是账户链上第一个交易，填0-Hash
  * `address`: `Address` 出块账户地址 `必填`
  * `publicKey`: `[]byte`  交易签名的公钥 `必填`
  * `signature`: `[]byte` 签名 `必填`
   
  选填：是否进行Pow，仅在需要进行Pow时指定，否则可忽略difficulty和nonce字段，或填写null
  * `difficulty`: `*string` 需要计算的PoW难度
  * `nonce`: `[]byte` Pow的nonce值
     
  选填：区分交易类型（send/receive）
  * `sendBlockHash`: `Hash`  表示receive交易所对应的send交易的hash，仅在receive交易中指定，send交易的sendBlockHash为0-Hash或忽略该字段
  * `toAddress`: `Address`  交易的接受地址，仅在send交易中指定，receive交易忽略该字段
  * `tokenId`: `TokenTypeId` 该交易的币种ID，仅在send交易中指定，当交易不实际发生金额时，tokenId为0-TokenTypeId或忽略该字段，receive交易忽略该字段
  * `amount`: `*string` 该交易发生的金额，仅在send交易中指定，当交易不实际发生金额时为"0"或null或忽略该字段， receive交易忽略该字段
  * `fee`: `*string` 发送该交易使用的手续费，无需指定币种默认为ViteToken，仅在send交易中指定， 所有receive交易忽略该字段
  * `data`: `[]byte` 交易数据，对于普通账户data仅可在send中指定，可为留言或者调用合约的交易数据，无需求时可为null或忽略改字段

- **Returns**: 
  `AccountBlock`: AccountBlock具体参考common_models_v2模块设计


- **Example**:

::: demo

```json tab:Request Send
{
	"jsonrpc": "2.0",
	"id": 17,
	"method": "ledger_sendRawTransaction",
	"params": [{
        "blockType": 2,
        "height": "2",
        "hash": "67f4d528a5194c46d594221d3d992257a3004ccdee7c5d7b2748d77e06a80caf",
        "previousHash": "d517e8d4dc9c676876b72ad0cbb4c45890804aa438edd1f171ffc66276202a95",
        "address": "vite_ab24ef68b84e642c0ddca06beec81c9acb1977bbd7da27a87a",
        "publicKey": "WHZinxslscE+WaIqrUjGu2scOvorgD4Q+DQOOcDBv4M=",
        "toAddress": "vite_0000000000000000000000000000000000000003f6af7459b9",
        "sendBlockHash": "0000000000000000000000000000000000000000000000000000000000000000",
        "tokenId": "tti_5649544520544f4b454e6e40",
        "amount": "1000000000000000000000000",
        "fee": "0",
        "data": "jefc/QAAAAAAAAAAAAAAqyTvaLhOZCwN3KBr7sgcmssZd7sA",
        "signature": "F5VzYwsNSr6ex2sl9hDaX67kP9g4TewMWcw7Tp57VkE1LQZO0i1toYEsXJ3MgcZdsvP67EymXXn1wpwhxnS3CQ=="
    }]
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": [
       {
            "blockType": 2,
            "height": "2",
            "hash": "67f4d528a5194c46d594221d3d992257a3004ccdee7c5d7b2748d77e06a80caf",
            "prevHash": "d517e8d4dc9c676876b72ad0cbb4c45890804aa438edd1f171ffc66276202a95",
            "previousHash": "d517e8d4dc9c676876b72ad0cbb4c45890804aa438edd1f171ffc66276202a95",
            "accountAddress": "vite_ab24ef68b84e642c0ddca06beec81c9acb1977bbd7da27a87a",
            "address": "vite_ab24ef68b84e642c0ddca06beec81c9acb1977bbd7da27a87a",
            "publicKey": "WHZinxslscE+WaIqrUjGu2scOvorgD4Q+DQOOcDBv4M=",
            "producer": "vite_ab24ef68b84e642c0ddca06beec81c9acb1977bbd7da27a87a",
            "fromAddress": "vite_ab24ef68b84e642c0ddca06beec81c9acb1977bbd7da27a87a",
            "toAddress": "vite_0000000000000000000000000000000000000003f6af7459b9",
            "fromBlockHash": "0000000000000000000000000000000000000000000000000000000000000000",
            "sendBlockHash": "0000000000000000000000000000000000000000000000000000000000000000",
            "tokenId": "tti_5649544520544f4b454e6e40",
            "amount": "1000000000000000000000000",
            "fee": "0",
            "data": "jefc/QAAAAAAAAAAAAAAqyTvaLhOZCwN3KBr7sgcmssZd7sA",
            "difficulty": null,
            "nonce": null,
            "signature": "F5VzYwsNSr6ex2sl9hDaX67kP9g4TewMWcw7Tp57VkE1LQZO0i1toYEsXJ3MgcZdsvP67EymXXn1wpwhxnS3CQ==",
            "quota": "105000",
            "quotaByStake": "105000",
            "quotaUsed": "105000",
            "totalQuota": "105000",
            "utUsed": "5",
            "logHash": null,
            "vmLogHash": null,
            "sendBlockList": null,
            "triggeredSendBlockList": null,
            "tokenInfo": {
                "tokenName": "Vite Token",
                "tokenSymbol": "VITE",
                "totalSupply": "999925000000000000000000000",
                "decimals": 18,
                "owner": "vite_ab24ef68b84e642c0ddca06beec81c9acb1977bbd7da27a87a",
                "tokenId": "tti_5649544520544f4b454e6e40",
                "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
                "ownerBurnOnly": false,
                "isReIssuable": true,
                "index": 0,
                "isOwnerBurnOnly": false
            },
            "confirmedTimes": "1793337",
            "confirmations": "1793337",
            "confirmedHash": "f5033a11251672f413cb01d9c52dc53eaa98f0731065405d0c2c8ca80c6bbe06",
            "firstSnapshotHash": "f5033a11251672f413cb01d9c52dc53eaa98f0731065405d0c2c8ca80c6bbe06",
            "receiveBlockHeight": "2",
            "receiveBlockHash": "656c7cd0f5c306b96dc8e6fc461364213b5ce0c7fdb485d489df5771771566bc",
            "timestamp": 1567513226
        }
    ]
}
```

:::

## ledger_getUnreceivedBlocksByAddress

- **Parameters**:

  * `Address`: 账户地址
  * `uint64`: 页码, 从0开始
  * `uint64`: 每页大小

- **Return**:
  * `list<AccountBlock>` AccountBlock具体参考common_models_v2模块设计

- **Example**:

::: demo

```json tab:Request
{
    "jsonrpc": "2.0",
    "id": 2,
    "method": "ledger_getUnreceivedBlocksByAddress",
    "params": [
        "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
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
            "height": "556",
            "hash": "12ec1d40a6c7560ba77b3764977c609189299dcf63d6586b50374714d0b8e013",
            "prevHash": "9a6c20d7d7fc927d89de6d9991a7904330007751f9d7d24dec141cbdb8b9e5ef",
            "previousHash": "9a6c20d7d7fc927d89de6d9991a7904330007751f9d7d24dec141cbdb8b9e5ef",
            "accountAddress": "vite_f74d18fc6431cb9d813c62a47a9063c4b9488219dc22c2736d",
            "address": "vite_f74d18fc6431cb9d813c62a47a9063c4b9488219dc22c2736d",
            "publicKey": "yNr85NJpkjKoaobFuWwIcoIdQR+ZRPrG5myrBhGxG5Q=",
            "producer": "vite_f74d18fc6431cb9d813c62a47a9063c4b9488219dc22c2736d",
            "fromAddress": "vite_f74d18fc6431cb9d813c62a47a9063c4b9488219dc22c2736d",
            "toAddress": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
            "fromBlockHash": "0000000000000000000000000000000000000000000000000000000000000000",
            "sendBlockHash": "0000000000000000000000000000000000000000000000000000000000000000",
            "tokenId": "tti_5649544520544f4b454e6e40",
            "amount": "16000000000000000000",
            "fee": "0",
            "data": "9HgjCQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABvBbWdOyAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAG8FtZ07IAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAbwW1nTsgAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABvBbWdOyAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAG8FtZ07IAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAbwW1nTsgAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABvBbWdOyAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAG8FtZ07IAAA=",
            "difficulty": "124419654",
            "nonce": "QxyYTRkNbco=",
            "signature": "sgcYMzD3L0KsEOeA9DckCPcOHeC7tTjiJdEcjS97guMKkOqHznnZ1naWkmDFJrtaNij1weRWMZ/27Y4rYc/DAw==",
            "quota": "0",
            "quotaByStake": "0",
            "quotaUsed": "38680",
            "totalQuota": "38680",
            "utUsed": "1.842",
            "logHash": null,
            "vmLogHash": null,
            "sendBlockList": null,
            "triggeredSendBlockList": null,
            "tokenInfo": {
                "tokenName": "VITE",
                "tokenSymbol": "VITE",
                "totalSupply": "1001186579383872099206960787",
                "decimals": 18,
                "owner": "vite_0000000000000000000000000000000000000004d28108e76b",
                "tokenId": "tti_5649544520544f4b454e6e40",
                "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
                "ownerBurnOnly": false,
                "isReIssuable": true,
                "index": 0,
                "isOwnerBurnOnly": false
            },
            "confirmedTimes": "5345754",
            "confirmations": "5345754",
            "confirmedHash": "ab88339a58d481a3b132f5c3c69ba14ab5b31d77b8860985b17951e990e190b4",
            "firstSnapshotHash": "ab88339a58d481a3b132f5c3c69ba14ab5b31d77b8860985b17951e990e190b4",
            "receiveBlockHeight": null,
            "receiveBlockHash": null,
            "timestamp": 1562219525
        }
    ]
}
```


:::
## ledger_getUnreceivedBlocksInBatch

- **Parameters**:

  *  `PagingQueryBatch`- Object 具体字段类型如下
    |    名称    |  类型  |     说明      |
    | :--------: | :----: | :-----------: |
    |  address   | string |   账户地址    |
    | pageNumber | uint64 | 页码, 从0开始 |
    | pageCount  | uint64 |   每页大小    |

- **Return**:

  * `map<string Address, list<AccountBlock>>` AccountBlock具体参考common_models_v2模块 设计

- **Example**:

::: demo

```json tab:Request
{
    "jsonrpc": "2.0",
    "id": 2,
    "method": "ledger_getUnreceivedBlocksInBatch",
    "params": [
        [{
    		"address": "vite_00000000000000000000000000000000000000042d7ef71894", 
    		"pageNumber": 0 ,
    		"pageCount": 1
    	},{
    		"address": "vite_68c5edf9069efe327e01e925790d868c7f7972d815016cf18a", 
    		"pageNumber": 0 ,
    		"pageCount": 1
    	}
    	]
    ]	
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": {
        "vite_68c5edf9069efe327e01e925790d868c7f7972d815016cf18a": [
            {
                "blockType": 2,
                "height": "170",
                "hash": "81a9a5e2747e28584db752a814bde0ee8894604df3707a9067e13f8297a090d5",
                "prevHash": "55e7088d3405aebed75c9e311303f52bbbc1827b11d86fd7840406e4f4bc42f8",
                "previousHash": "55e7088d3405aebed75c9e311303f52bbbc1827b11d86fd7840406e4f4bc42f8",
                "accountAddress": "vite_ba2ae946be1f56a8c83ce3e1d80a53d8137c264684d5dd7610",
                "address": "vite_ba2ae946be1f56a8c83ce3e1d80a53d8137c264684d5dd7610",
                "publicKey": "u7OxKqv0EqysClekERWf8FK3NgsEVnS6dq0Cu53en4o=",
                "producer": "vite_ba2ae946be1f56a8c83ce3e1d80a53d8137c264684d5dd7610",
                "fromAddress": "vite_ba2ae946be1f56a8c83ce3e1d80a53d8137c264684d5dd7610",
                "toAddress": "vite_68c5edf9069efe327e01e925790d868c7f7972d815016cf18a",
                "fromBlockHash": "0000000000000000000000000000000000000000000000000000000000000000",
                "sendBlockHash": "0000000000000000000000000000000000000000000000000000000000000000",
                "tokenId": "tti_5649544520544f4b454e6e40",
                "amount": "0",
                "fee": "0",
                "data": "6SXjDQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAbwW1nTsgAAA",
                "difficulty": null,
                "nonce": null,
                "signature": "8qNYBI2+rQOH6LmS+Skl5/lXCLaW3bZHVGfS8IFraol5LiGuukmjfzsiNGQTDpB7MN006K9VcCGE05eZKeyVAg==",
                "quota": "23448",
                "quotaByStake": "23448",
                "quotaUsed": "23448",
                "totalQuota": "23448",
                "utUsed": "1.117",
                "logHash": null,
                "vmLogHash": null,
                "sendBlockList": null,
                "triggeredSendBlockList": null,
                "tokenInfo": {
                    "tokenName": "VITE",
                    "tokenSymbol": "VITE",
                    "totalSupply": "1001186579383872099206960787",
                    "decimals": 18,
                    "owner": "vite_0000000000000000000000000000000000000004d28108e76b",
                    "tokenId": "tti_5649544520544f4b454e6e40",
                    "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
                    "ownerBurnOnly": false,
                    "isReIssuable": true,
                    "index": 0,
                    "isOwnerBurnOnly": false
                },
                "confirmedTimes": "5257692",
                "confirmations": "5257692",
                "confirmedHash": "9c9a436d1d8b06c8a9955955890877b40c5e493c4054f59d36a3bfabf315772f",
                "firstSnapshotHash": "9c9a436d1d8b06c8a9955955890877b40c5e493c4054f59d36a3bfabf315772f",
                "receiveBlockHeight": null,
                "receiveBlockHash": null,
                "timestamp": 1562309573
            }
        ]
    }
}
```

:::


## ledger_getUnreceivedTransactionSummaryByAddress

- **Parameters**:

  *  `Address`- 账户地址

- **Return**:

  * `AccountInfo` AccountInfo具体参考common_models_v2模块设计

- **Example**:

::: demo

```json tab:Request
{
    "jsonrpc": "2.0",
    "id": 2,
    "method": "ledger_getUnreceivedTransactionSummaryByAddress",
    "params": [
        "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10"
    ]
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": {
        "address": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
        "blockCount": "6",
        "balanceInfoMap": {
            "tti_5649544520544f4b454e6e40": {
                "tokenInfo": {
                    "tokenName": "VITE",
                    "tokenSymbol": "VITE",
                    "totalSupply": "1001186579383872099206960787",
                    "decimals": 18,
                    "owner": "vite_0000000000000000000000000000000000000004d28108e76b",
                    "tokenId": "tti_5649544520544f4b454e6e40",
                    "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
                    "ownerBurnOnly": false,
                    "isReIssuable": true,
                    "index": 0,
                    "isOwnerBurnOnly": false
                },
                "balance": "96000000000000000000",
                "transactionCount": "6"
            }
        }
    }
}
```
:::


## ledger_getUnreceivedTransactionSummaryInBatch

- **Parameters**:

  *  `list<Address>`- 账户地址列表

- **Return**:

  * `list<AccountInfo>` AccountInfo具体参考common_models_v2模块 设计

- **Example**:

::: demo

```json tab:Request
{
    "jsonrpc": "2.0",
    "id": 2,
    "method": "ledger_getUnreceivedTransactionSummaryInBatch",
    "params": [[
        "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
        "vite_68c5edf9069efe327e01e925790d868c7f7972d815016cf18a"
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
            "address": "vite_0b573f9d1fca7d830fc0d1552e3ff7b7f44455e38c8218fd10",
            "blockCount": "6",
            "balanceInfoMap": {
                "tti_5649544520544f4b454e6e40": {
                    "tokenInfo": {
                        "tokenName": "VITE",
                        "tokenSymbol": "VITE",
                        "totalSupply": "1001186579383872099206960787",
                        "decimals": 18,
                        "owner": "vite_0000000000000000000000000000000000000004d28108e76b",
                        "tokenId": "tti_5649544520544f4b454e6e40",
                        "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
                        "ownerBurnOnly": false,
                        "isReIssuable": true,
                        "index": 0,
                        "isOwnerBurnOnly": false
                    },
                    "balance": "96000000000000000000",
                    "transactionCount": "6"
                }
            }
        },
        {
            "address": "vite_68c5edf9069efe327e01e925790d868c7f7972d815016cf18a",
            "blockCount": "1",
            "balanceInfoMap": {
                "tti_5649544520544f4b454e6e40": {
                    "tokenInfo": {
                        "tokenName": "VITE",
                        "tokenSymbol": "VITE",
                        "totalSupply": "1001186579383872099206960787",
                        "decimals": 18,
                        "owner": "vite_0000000000000000000000000000000000000004d28108e76b",
                        "tokenId": "tti_5649544520544f4b454e6e40",
                        "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
                        "ownerBurnOnly": false,
                        "isReIssuable": true,
                        "index": 0,
                        "isOwnerBurnOnly": false
                    },
                    "balance": "0",
                    "transactionCount": "1"
                }
            }
        }
    ]
}
```

:::

## ledger_getVmLogs

- **Parameters**:
  * `Hash`: 查询AccountBlock的Hash

- **Return**:
  * `List<VmLog>` AccountBlock的VmLog列表

- **Example**:
::: demo

```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 17,
	"method": "ledger_getVmLogs",
	"params": ["5a78365f4f7e9c29d57c8f087c9691bfff63a4889cde5d03a89cb24d34abbdf3"]
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 17,
    "result": [
        {
            "topics": [
                "00d73e74672366b05e8980c144e4c523f171cee9fcae60041d97ae1f540a4de5",
                "0000000000000000000000f74d18fc6431cb9d813c62a47a9063c4b948821900"
            ],
            "data": "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABoFVpDZ24AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA=="
        }
    ]
}
```

:::

## ledger_getVmlogsByFilter
根据参数查询历史日志。返回值按账户块高度从低到高排序。

- **Parameters**: 
  - 查询参数，同`subscribe_createVmlogFilter`，注意`fromHeight`和`toHeight`都填0时会查询整个账户链，可能会导致返回数据过多，最好指定明确的查询高度范围

- **Returns**:  
	- `Array<VmlogMessage>` 日志信息，同`subscribe_getChangesByFilterId`返回值
	
::: demo
```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 1,
	"method": "ledger_getVmlogsByFilter",
	"params": [{
		"addressHeightRange":{
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
      "vmlog": {
        "topics": [
          "28e6ea56797f4a1b22a1d1986cb6c22e80099ba8e4fd14d42accfaedfe5f6640"
        ],
        "data": "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAGQQurTFV9WklB2DRvsX8wLCgyoVomYHSCebb9Br/hQ+RAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABwYLIcJLnbQjGl+qeU7YWlTWwfsoF6mescP5xz2fDTEg="
      },
      "accountBlockHash": "e4917f357a4588ec1752797ee5516939f46078f5356b14422d4a9dfe45f88bf5",
      "accountBlockHeight": "10",
      "address": "vite_8810e12ec2d4d61e7568cac25ebd5dd44735d36a405b94f1fa",
      "removed": false
    }
  ]
}
```
:::

## ledger_getPoWDifficulty
用户账户通过ledger_sendRawTransaction创建交易时获取difficulty。接口逻辑为先根据交易参数计算所需配额，然后判断账户是否有抵押受益金额，如果抵押获得的配额足够，则不需要计算PoW；如果没有抵押或者抵押获得的配额不够，则计算PoW难度。
如果接口返回error，通常是交易data过长，或者当前交易不能通过计算PoW来获取配额，例如在同一个快照块内账户链上上一笔交易已通过PoW来获取配额，那么新交易不允许再次计算PoW。

- **Parameters**: 
  * `GetPoWDifficultyParams`
    * `address`: `string address` 账户地址
    * `previousHash`: `string hash` 账户链上上一个块的哈希
    * `blockType`: `byte` 交易类型
    * `toAddress`: `string address` 响应账户地址，交易类型为请求交易时填写
    * `data`: `string base64` 备注，交易类型为请求交易填写

- **Returns**: 
  - `GetPoWDifficultyResult`
    - `requiredQuota`: `string uint64`  交易需要的配额
    - `difficulty`: `string bigint` 需要计算的PoW难度，如果为空字符串，说明不需要计算PoW
    - `qc`: `string bigint ` 拥堵系数 * 1e18
    - `isCongestion`: `bool` 全网是否拥堵，true表示当前全网拥堵，此时配额成本提高，false表示不拥堵
    
- **Example**:
::: demo
```json tab:Request
{
	"jsonrpc": "2.0",
	"id": 1,
	"method": "ledger_getPoWDifficulty",
	"params": [{
		"address":"vite_ab24ef68b84e642c0ddca06beec81c9acb1977bbd7da27a87a",
		"previousHash":"7b5dcb470889997100e0e09cd292d221ad1c11bb0daf8b9fa39a2d1f90210aa0",
		"blockType":2,
		"toAddress":"vite_0000000000000000000000000000000000000004d28108e76b",
		"data":"8pxs4gAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAGAAAAAAAAAAAAAAAAAICy1ooG9SwPu0VPZ17lQ1+3hyUgAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAFc3VwZXIAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA=",
	}]
}
```
```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "requiredQuota": 32152,
        "difficulty": "102920708",
        "qc": "1000000000000000000",
        "isCongestion": false
    }
}
```
:::
