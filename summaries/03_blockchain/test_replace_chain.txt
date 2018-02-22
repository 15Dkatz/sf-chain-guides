Test the new chain replacement functionality. In blockchain.test.js:
```
it('replaces the chain with a valid chain', () => {
	bc2.addBlock('goo');
  bc.replaceChain(bc2.chain);
  expect(bc.chain).toEqual(bc2.chain);
});

it('does not replace the chain with one of less than or equal length', () => {
	bc.addBlock('foo');
  bc.replaceChain(bc2.chain);
  expect(bc.chain).not.toEqual(bc2.chain);
});
```
$ npm run test

