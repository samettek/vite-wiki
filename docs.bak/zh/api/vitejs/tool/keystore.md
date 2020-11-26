# Keystore

## 安装

:::demo
```bash tab:npm
npm install @vite/vitejs-keystore --save
```

```bash tab:yarn
yarn add @vite/vitejs-keystore
```
:::

## 引入

```javascript import
import { keystore } from '@vite/vitejs';
// Or
import * as keystore from '@vite/vitejs-keystore';
```

## Keystore 结构

```json
{
    "uuid": "fe4a9460-0b3a-11e9-8975-e744cf968fe6",
    "crypto":{
        "ciphername": "aes-256-gcm",
        "ciphertext": "0f2eabd62c2b479e18a8445f2a6449cc77895c5ce24e8e93bf24356b0080de67373956a69499145a262a6bed36873e35",
        "nonce": "c1e22b37a56fc4280d1947a0",
        "kdf": "scrypt",
        "scryptparams": {
            "n": 4096,
            "r": 8,
            "p": 6,
            "keylen": 32,
            "salt": "11a75fdee6bc20084628e55ec3c26ea4120dd8053e39757e164f7642b3d0af73"
        }
    },
    "version": 3,
    "timestamp": 1546068361382
}
```

## Methods

### isValid 
keystore是否合法

- **Parameters**
    * `keystore : string` Keystore string

- **Return**
    * `validate : boolean` 是否合法

- **Example**
```javascript
import { isValid } from '@vite/vitejs-keystore';

const result = isValid('{}'); // false
```

### decrypt
解密keystore

- **Parameters**
    * `keystore : string` Keystore string
    * `pwd : string` 密码

- **Return**
    * Promise<`key : string`> 加密前的字符串

### encrypt
加密字符串，生成keystore

- **Parameters**
    * `string` 需要加密的字符串
    * `string` 密码
    * `scryptParams : Object` 加密参数(非必填)
        - n
        - r
        - p
        - keylen
        - salt
    
- **Return**
    * Promise<`keystore: json-string`> keystore字符串
