Every blockchain starts with the “genesis block” - a default dummy block to originate the chain.

Add a static genesis function to the `Block` class in `block.js`;
```
static genesis() {
	return new this('Genesis time', '-----', 'f1r57-h45h', []);
}
```

Back in dev-test.js, test out the new genesis block:
```
console.log(Block.genesis().toString());
```
$ npm run dev-test
