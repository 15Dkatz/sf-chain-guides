Add a function to add a generate a block based off of some provided `data` to store, and a given `lastBlock.` Call the function `mineBlock`. Generating a block is equated to an act of mining since it takes computational power to “mine” the block. Later on, we’ll make the demand for spending computational power more explicit.

Add the `static mineBlock()` function to the `Block` class:
```
static mineBlock(lastBlock, data) {
	const timestamp = Date.now();
	const lastHash = lastBlock.hash;
  const hash = ‘todo-hash’;
  return new this(timestamp, lastHash, hash, data);
}

Now test the new `mineBlock` function. In dev-test.js, delete all of the lines except for the first line that requires the `Block` class.
```
const fooBlock = Block.mineBlock(Block.genesis(), 'foo');
console.log(fooBlock.toString());
```

