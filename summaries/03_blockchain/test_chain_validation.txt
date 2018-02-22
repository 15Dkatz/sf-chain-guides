Test Chain Validation. In blockchain.test.js, add a second blockchain instance:
```
let bc, bc2;
…
bc = new Blockchain();
bc2 = new Blockchain();
```

Add new unit tests:
```
it('validates a valid chain', () => {
	bc2.addBlock('foo');
	expect(bc.isValidChain(bc2.chain)).toBe(true);
});
it('invalidates a chain with a corrupt genesis block', () => {
	bc2.chain[0].data = 'Bad data';
  expect(bc.isValidChain(bc2.chain)).toBe(false);
});

it('invalidates a corrupt chain', () => {
  bc2.addBlock('foo');
  bc2.chain[1].data = 'Not foo';
  expect(bc.isValidChain(bc2.chain)).toBe(false);
});
```
$ npm run test

