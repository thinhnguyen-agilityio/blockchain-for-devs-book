# Unit Testing
Truffle uses Mocha testing framework and Chai for assertions. If you are not familiar with Mocha go to https://mochajs.org and read the getting started section, it will help you to understand the tests better. In the test directory add new file. There is no convension, if you want to make it clearer with `test` in the name`SimpleStorageTest.js`.

`const SimpleStorage = artifacts.require('SimpleStorage')`
You can use artifacts to get the contract, same as in the **Migrations** chapter.

```js
contract('Simple Storage contract', (accounts) => {
    // The tests should be here
}
```
In **mocha** we have `describe` and for truffle is modified as `contract`. We can add multiple contracts in one file, but keep it clear and use one file per contract. When you run `truffle test` mocha will loop all files in the directory and run them.

Now inside the contract we will write our test cases, the contract is simple and we will check the **set** function and we will compare the result from the **get** function.

```js

it('Should set X correctly', () => {
    let contract = await SimpleStorage.deployed()
    contract.set(4, { from: accounts[0] })
    let result = await contract.get()
    assert.equal(result, 4, "Amount was not correct")
})	
```

In the first line we deployed the contract
```js
let contract = await SimpleStorage.deployed()
```
When we have the contract we can interact with it. We will **set** data to the variable
```js
contract.set(4, { from: accounts[0] })
```

After that we can call the getter method and compare the result with assert.
```js
let result = await contract.get()
assert.equal(result, 4, "Amount was not correct")
```

Now we have our first test and we can run to test is it everything alright, go to the terminal and run 
```
$ truffle test
Using network 'development'.
Compiling .\contracts\SimpleStorage.sol...

   Contract: Simple Storage contract
      √ Should set X correctly
  
  1 passing (78ms)
```
If you have similar output, everything is correct and you can continue to the solidity tests.
## Solidity Tests



