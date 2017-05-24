Unit Testing
===

 - You want tests to have lots of coverage -- you want to write tests that cover large percentage of code 
 - False Positive - test that incorrectly passes
 - When a test fails -- assess the test and the code and see which is the problem

CI - Countinuous Integration
  - circleci.com
  - PhantomJS (headless browser) - allows you to make browser type evens without needed the visual representation of what is happening
    - allows you to run code manipulating DOM behind the scences (ie. click event etc)
  - Mocha --> test runner (nude)
  - Chai --> assertion library
  - Karma --> test Runner (browser) - creates ecostystem for test to run in 
  

### General Testing Structure
  - Create Test Folder - codeFile.test.js --> live inside folder
  - Descripe statements - section tests into multiple chunks
  - scripts (packageJSON) - "test": .......
  - devDependencies --> list dependencies needed for developers - list Unit Testing items here

#### testingCode.test.js
```javascript
describe('description of test', function(){
    
    describe('on page load', function(){
      it('should have a #create button on load', function(){
        onReady();                //if you name functions you can run tests on them - you cannot if they are all nested
        expect($('#create')).to.exist;
       });
    })
    
    //--> subsequent tests 
   
  }// end description of test
```

### Chai | Assertion Library
 - Chai Assertion Library 
 - Brings in more verbs and language that allow for better / more readable test
 - BDD - Behavioral Driven Development
   - Write code and then check with tests
 - TDD - Test Driven Development
   - Write test then code to pass test

## Writing Tests
Terminal - install chai and mocha as dev-dependencies (locally)
#### terminal
```
$: npm install chai--save-dev
$: npm install mocha--save-dev
```

#### moduleOne.js
```javascript
 //Code to be tested

  var addOne = function (number) {
    return number + 1;
  }
 
 module.exports = addOne;
```
### 1. Write test
 - Every `it` block is considered it's own test 
#### addOne.test.js
```javascript
 
 var expect = require('chai').expect;
 var addOne = require('../src/modules/addOne');
 
 describe('testing add one module', function(){
  //what should it do?
  //call add one function with some value --> addOne(8) and expect = 9
  
  it('should add one to the number passed in', function(){
   
    //var ourNumber = 8;
    //var ourNumberPlusOne = addOne(ourNumber);
    //expect(ourNumberPlusOne).to.equal(9);
    // OR condensed to code below
  
    expect(addOne(8)).to.equal(9);
  }); 
  
  it('should return a number type', function () {
   expect(addOne(8)).to.be.a('number');
  });
  
});
```

### 2. Run Test using Mocha
#### terminal
```
 $: mocha test/addOne.test.js
```
### OR Include Test Script in package.json
#### package.json
```
 },
 "scripts": {
  "tests": "mocha test/*.test.js"  //this will run all test.js files in test folder
  },
```
#### terminal
```
$:  npm test
```
