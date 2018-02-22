Create the vital input object which provides information about the sender in the transaction. This information includes the sender’s original balance, his or her public key, and most important, his or her signature for the transaction. To generate signatures, the elliptic module gives a convenient sign method within the keyPair object. This takes any data in its hash form, and returns a signature based on the keyPair. Later on, this generated signature and the matching public key can be used to verify the authenticity of the signature. Add this signing feature to the Wallet class called sign. In wallet/index.js:
```
sign(dataHash) {
  return this.keyPair.sign(dataHash);
}
```

Also create a static signTransaction method, that will generate the input object for a transaction:
```
static signTransaction(transaction, senderWallet) {
  transaction.input = {
    timestamp: Date.now(),
    amount: senderWallet.balance,
    address: senderWallet.publicKey,
    signature: senderWallet.sign(transaction.outputs)
  };
}
```

The sign method wants the data to be in a hash. It’s much more efficient to have a hash value with a fixed number of characters, rather than a potentially large object that could be full of long pieces of data. Luckily, there is a hash function that is being used to generate the hashes for blocks in the blockchain. Let’s take advantage of that function, and place it in the ChainUtil class.

- Head to block.js.

Cut the SHA256 requirement and stick it into the chain util file. Then declare a static hash function within here that takes an arbitrary piece of data, then stringifies it, passes it into the SHA256 hashing function, and returns the string form of the hash object:

```
const SHA256 = require('crypto-js/sha256');
…

static hash(data) {
  return SHA256(JSON.stringify(data)).toString();
}

```

Since we’ve the SHA256 function was removed from the block class, use the new ChainUtil hash method in its place. In block.js, import the ChainUtil class:
```
const ChainUtil = require('../chain-util');
```
Then the static hash function of the block class will call the ChainUtil hash function in place of the previous SHA256 function call:
```
static hash(timestamp, lastHash, data, nonce, difficulty) {
  return ChainUtil.hash(`${timestamp}${lastHash}${data}${nonce}${difficulty}`);
}
```
Ddo the same thing in the transaction class to create a hash for the transaction outputs. Head to transaction.js. Now within the sign function call from the sender wallet, make sure to create a hash for the transaction outputs, before we generate the signature:
```
signature: senderWallet.sign(ChainUtil.hash(transaction.outputs))
```

Lastly, make sure to generate an input by using this function whenever a new transaction is created. Therefore, call the `signTransaction` function in `newTransaction`, passing in the transaction instance, and the senderWallet:
```
Transaction.signTransaction(transaction, senderWallet);
```

