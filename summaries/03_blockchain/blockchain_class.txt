Create the `Blockchain` that creates a chain based on the `Block` class:
Create blockchain.js

blockchain.js:
```
const Block = require('./block');

class Blockchain {
  constructor() {
    this.chain = [Block.genesis()];
  }

  addBlock(data) {
    const block = Block.mineBlock(this.chain[this.chain.length-1], data);
    this.chain.push(block);
    return block;
  }
}

module.exports = Blockchain;
```
