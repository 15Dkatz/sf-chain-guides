A hashing function generates a unique value for the combination of data attributes in the block. The hash for a new block is based on its own timestamp, the data it stores, and the hash of the block that came before it.

Install the `crypto-js` module which has the SHA256 (Secure Hashing Algorithm 256-bit) function:
$ npm i crypto-js --save

In block.js, require the sha256 from the `crypto-js` module at the top:
```
const SHA256 = require('crypto-js/sha256');
```

Then add a new static hash function to the Block class:
```
static hash(timestamp, lastHash, data) {
	return SHA256(`${timestamp}${lastHash}${data}`).toString();
}
```

Now replace the ‘todo-hash’ stub in the `mineBlock` function:
```
const hash = Block.hash(timestamp, lastHash, data);
```

Check the command line - `npm run dev-test` should still be running. Notice the generated hash of the block.
