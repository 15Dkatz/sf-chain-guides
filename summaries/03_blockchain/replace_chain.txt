If another contributor to a blockchain submits a valid chain, replace the current chain with the incoming one. Only replace chains that are actually longer than the current chain. Handle this with a `replaceChain` function in the `Blockchain` class:
```
replaceChain(newChain) {
  if (newChain.length <= this.chain.length) {
    console.log('Received chain is not longer than the current chain.');
    return;
  } else if (!this.isValidChain(newChain)) {
    console.log('The received chain is not valid.');
    return;
  }

  console.log('Replacing blockchain with the new chain.');
  this.chain = newChain;
}
```

