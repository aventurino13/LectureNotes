Grunt
===

File Structure
  - Client
    - script.js
  - Server
    - Public
      - Scripts
        

#### gruntfile.js
```javascript
  module.exports = function ( grunt ) {
    grunt.initConfig({
      uglify: {
        my_target: {
          flies: {
          //destination : [target]
          //min: [source code]
          'server/public/scripts/client.min.js' : [client/script.js
          }
        }
      }
    })
```
#### terminal
``` grunt uglify
```
