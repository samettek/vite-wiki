# Q&A

## Mnemonics

Multiple private keys can be derived from one mnemonic phrases, each having independent address. Refer to [HD Wallet](/tutorial/wallet/hdwallet.md) for more information

:::warning Note
Always keep your mnemonic phrase safe
:::

## Quota

Quota is necessary for sending transaction on Vite. In the Mainnet, quota can be obtained through PoW or staking. Refer to [Quota](/tutorial/rule/quota) for details

## Token Issuance

Refer to [RPC Token Issuance API](../rpc/contract_v2)

## Subscription

Event subscription is provided in `ViteAPI`. Refer to [ViteAPI](./ViteAPI/start) for detailed information

## Sending Transaction

```typescript
import HTTP_RPC from '../../src/HTTP';
import { wallet, accountBlock, ViteAPI, constant } from '@vite/vitejs';

const { Vite_TokenId } = constant;
const { getWallet } = wallet;
const { createAccountBlock } = accountBlcok;

// 1. Get private key and account address from mnemonic phrase
const wallet = getWallet('yourMnemonic');
const { privateKey, address } = wallet.deriveAddress(0);  // get the private key at index 0.

// 2. Get provider by HTTP address
const httpService = new HTTP_RPC("http://example.com");
const provider = new ViteAPI(httpService);

// 3. Create accountBlock instance
const accountBlock = createAccountBlock('send', {
    toAddress: 'your toAddress', 
    tokenId: Vite_TokenId,
    amount: '1000000000000000000000'    // 10 Vite (18 decimals)
}, provider, privateKey);

// 4. Send accountBlock
const sendAccountBlock = async () => {
    await accountBlock.autoSetPreviousAccountBlock();
    return accountBlock.sign().send();
}

sendAccountBlock().then(() => {
    console.log('Send success');
}).catch((err) => {
    console.warn(err);
});
```
