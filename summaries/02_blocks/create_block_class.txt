Create the block class with a file called block.js. Each black has a `hash`, `lastHash`, and `timestamp` attribute.
Create block.js

In block.js: 
```
class Block {
constructor(timestamp, lastHash, hash, data) {
	this.timestamp = timestamp;
  this.lastHash = lastHash;
  this.hash = hash;
  this.data = data;
}
toString() {
	return `Block -
          Timestamp : ${this.timestamp}
 		      Last Hash : ${this.lastHash.substring(0, 10)}
          Hash      : ${this.hash.substring(0, 10)
          Data      : ${this.data}`;
  }
}
```
Test the new block class. Create dev-test.js alongside block.js:
```
const Block = require(‘./block’);
const block = new Block();
const block = new Block(‘foo’, ‘bar’, ‘zoo’, ‘baz’);
console.log(block.toString())
```
In `package.json`, find the scripts section and add:
```
“dev-test”: “nodemon dev-test”
````
Then in the command line, run:
$ npm run dev-test

