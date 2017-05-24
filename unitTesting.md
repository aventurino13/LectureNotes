Unit Testing
===

 - You want tests to have lots of coverage -- you want to write tests that cover large percentage of code 
 - False Positive - test that incorrectly passes
 - When a test fails -- assess the test and the code and see which is the problem

CI - Countinuous Integration
  - circleci.com
  - PhantomJS (headless browser) - allows you to make browser type evens without needed the visual representation of what is happening
    - allows you to run code manipulating DOM behind the scences (ie. click event etc)
  - Mocha --> test runner
  - Chai --> assertion library
  

### General Testing Structure
  - Create Test Folder - codeFile.test.js --> live inside folder
  - Descripe statesments - section tests into multiple chunks
  - scripts (packageJSON) - "test": 'mocha start'
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

### Chai
 - Chai Assertion Library 
 - Brings in more verbs and language that allow for better / more readable test
 - BDD - Behavioral Driven Development
   - Write code and then check with tests
 - TDD - Test Driven Development
   - Write test then code to pass test

