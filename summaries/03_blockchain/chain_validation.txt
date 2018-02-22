Chain validation ensures that incoming chains are not corrupt once there are multiple contributors to the blockchain. To validate a chain, make sure it starts with the genesis block. Also, ensure that its hashes are generated properly.

In the `Blockchain` class, add an `isValidChain` method:
```
isValidChain(chain) {
  if (JSON.stringify(chain[0]) !== JSON.stringify(Block.genesis())) return false;
  for (let i=1; i<chain.length; i++) {
    const block = chain[i];
    const lastBlock = chain[i-1];
    if (
      block.lastHash !== lastBlock.hash ||
      block.hash !== Block.blockHash(block)
    ) {
      return false;
    }
  }
  return true;
}
```

This method depends on a `static blockHash` function in the `Block` class. This will generate the hash of a block based only on its instance. In block.js, in the `Block` class:
```
static blockHash(block) {
	const { timestamp, lastHash, data } = block;
  return Block.hash(timestamp, lastHash, data);
}
```

