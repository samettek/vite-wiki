# Event Subscription

## What is Event

Events are notifications used to notify front-end program in smart contract. 
When an event is triggered, a log(`VmLog`) specific to the event is logged in the smart contract's response block.

Take the following contract as an example. When method `TransferWithEvent` is called, the contract transfers the received tokens to the specified address and then triggers a `transferEvent` event.

```
pragma soliditypp ^0.4.1;
contract TransferContract {
   event transferEvent(address indexed addr, uint256 value, tokenId tokenid);
   
   onMessage TransferWithEvent(address addr) payable {
      addr.transfer(msg.tokenid ,msg.value);
      emit transferEvent(addr, msg.value, msg.tokenid);      
   }
}
```

A `transferEvent` event contains the following information:
* The hash of contract response block that triggered the event. It indicates the context of the event, and can be used to trace the contract account address, contract account height, request transaction hash, and so on.
* Event signature, which is the hash of `transferEvent(address, uint256, uint256)`.
* Index parameters, which are marked as `indexed` in event definition. Up to 4 index parameters can be defined for an event. Event signature and index parameters are stored in `topics` field of `VmLog`, where event signature occupies `topics[0]`.
* Non-index parameters, which are parameters without `indexed` associated with. Non-index parameters are stored in `data` field of `VmLog`.

Below is an example of event logged when sending 1 VITE to `vite_9990375e0eaf10426d1d1f9b528b6dee158fd3adb0e1b9de70`
```
{
  "accountBlockHash":"0edcbbbbbf0d68e5721187c1866029e2f544e00f2f48358a9df5ca18f5d1d5a2",
  "log": {
    "topics": [
        "f632c631f1cf58a101b09f8fe0262d7c04f04e9b77f255bd2f86fedd1b6af56d",
        "0000000000000000000000009990375e0eaf10426d1d1f9b528b6dee158fd3ad"
    ],
    "data": "0000000000000000000000000000000000000000000000000DE0B6B3A764000000000000000000000000000000000000000000005649544520544f4b454e6e40"
  }
}
```

## What is Subscription

If a type of event is subscribed, the subscriber will be notified when the event occurs. 
For example, if you subscribe to `transferEvent` event of `TransferContract` contract, you will receive a notification when `TransferWithEvent` method is called.

Event subscription can be used to continuously listen for a specified type of transaction that occurs on blockchain. 
It's only allowed to subscribe to events that have not occurred yet. Historical events cannot be subscribed but can only be queried through query interface.

The following parameters need to be specified when subscribing to an event:
* Contract account address. Required.
* Contract account height range. Non-required. With this parameter, it's possible to subscribe to events happening within a certain height range.
* Event signature or index parameter. Non-required. For example, you can subscribe to events of transferring to certain accounts.

## Two Modes of Event Subscription

In the following part we suppose that "server" is a full node supporting event subscription, and "client" is a terminal that subscribes to certain event.

### Persistent Connection

In this mode, a persistent connection is established between client and server, and then client subscribes to event that occurs at server side. 
When a new event is triggered, the server will push it to the client. If the connection is broken, subscription will close.

### Polling

In polling mode, client firstly subscribes to the event. After the subscription is successful, client will periodically request for events from server. 
New events that were triggered since last request, if any, will be returned, otherwise the server returns null.

In this mode, if client does not send request to server for more than 5 minutes, subscription will close automatically. Client must re-subscribe in this situation.

## Other Subscription Types

In Vite TestNet, in addition to events generated by smart contracts, it is also possible to subscribe to new transactions. 
It is not required to specify filtering parameters when subscribing to transaction, and all new transactions will be notified after the subscription is successful.

## Subscription Types in Future

* When transaction is confirmed
* When event is confirmed
* When account balance changes

