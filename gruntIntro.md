Grunt
===

File Structure
  - Client
    - script.js
  - Server
    - Public
      - Scripts
        - client.min.js <-- grunt creates minified file
      - Vendors <-- grunt creates 
-----------------------------------------------
## Uglify | Minification 
- Creates minified file
- On it's own it does not watch changes - must combine with watch task to watch for changes and update minified file

#### script1.js
```javascript
  console.log('this is a console cool');
  
  var ourFunction = function(){
    console.log('this is a function');
   }
  
  var anotherOne = function (){
    console.log('hey');
   }
  
```

#### gruntfile.js
```javascript
  module.exports = function ( grunt ) {
    grunt.initConfig({
      uglify: {
        my_target: {
          flies: {
          //destination : [target]
          //min: [source code]
          'server/public/scripts/client.min.js' : [client/script.js]
            //anything you want to go into the same min file must ^ go in this array 
            //ie. [client/scripts.js, client/script2.js]
            //[client/*.js ] --> this will min all scripts in client folder
          }
        }
      }
    });
    
    grunt.loadNpmTasks('grunt-contrib-uglify');
```
#### terminal
``` 
 grunt uglify
```

Combining Minified files
 - Services and Controllers must be seperate

-----------------------------------------------

## Watch Tasks
This will watch for changes in the script files and update the minified files and run tasks
```
npm install grunt-contrib-watch --save-dev
```

#### gruntfile.js
```javascript
  module.exports = function ( grunt ) {
    grunt.initConfig({
      uglify: {
        my_target: {
          flies: {
          //destination : [target]
          //min: [source code]
          'server/public/scripts/client.min.js' : [client/*.js]
            
          }
        }
      }, 
      watch: {
        files: ['client/*.js],
        tasks:['uglify']
        }
    });
    
    grunt.loadNpmTasks('grunt-contrib-uglify');
    grunt.loadNpmTasks('grunt-contrib-watch');
```
-----------------------------------------------
## Register Tasks
```javascript
  //grunt name
  grunt.registerTask('name', ['watch']); //below above code to register tasks
  
  OR
  
  //grunt --> allows you to just run grunt in terminal instead of uglifiy and then watch
  grunt.registerTask('default', ['watch']); 
```
-----------------------------------------------

## Copy
```
npm install grunt-contrib-copy --save-dev
npm install bootstrap --save
```

#### gruntfile.js
```javascript
  module.exports = function ( grunt ) {
    grunt.initConfig({
      uglify: {
        my_target: {
          flies: {
          //destination : [target]
          //min: [source code]
          'server/public/scripts/client.min.js' : [client/*.js]
            
          }
        }
      }, 
      watch: {
        files: ['client/*.js],
        tasks:['uglify']
      },
      copy: {
        main: {
          files: [
            //cwd--> current working directory
            {expand: trut, cwd: 'node_modules', src:['bootstrap/**', 'angular/**'], dest:'server/public/vendors'}
         ]
        }
       }
    });
    
    grunt.loadNpmTasks('grunt-contrib-uglify');
    grunt.loadNpmTasks('grunt-contrib-watch');
    grunt.loadNpmTasks('grunt-contrib-copy');
    
    grunt.registerTask('default', ['copy', 'watch']); 
```
