Unit Testing
===

CI - Countinuous Integration
  - circleci.com
  - PhantomJS (headless browser) - allows you to make browser type evens without needed the visual representation of what is happening
    - allows you to run code manipulating DOM behind the scences (ie. click event etc)
  - Mocha --> test runner
  - Chai --> assertion library
  

### General Testing Structure
  - Create Test Folder - codeFile.test.js --> live inside folder
  - Descripe statesments - section tests into multiple chunks 

#### testingCode.test.js
```javascript
describe('description of test', function(){
    
    describe('on page load', function(){
      it('should have a #create button on load', function(){
        onReady();        //if you name functions you can run tests on them - you cannot if they are all nested
        expect($('#create')).to.exist;
       });
    })
    
    //--> subsequent tests 
   
  }// end description of test
```

 
  

