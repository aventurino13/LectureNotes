Passport Authentication
===

Overview
  - Important to have general overview and be able to make use of the following:
     - Session
     - Cookies
     - Encryption
     - Strategies

Three possible senarios/ states for user
  1. No Account
  2. Create Account --> username password
  3. Logging In --> all following requests
 
app repo:
  https://github.com/aventurino13/prime-passport-lectures
   
App.js
   - Order matters and it must run in a specific order to function
 
Passport 
   - db models 
   - Helps node projects make sure a user is authenticating
   - Different strategies for authentication
   - No matter what strategy you used you will have req.user 
   
### Creating Account / Registration
  - Make post request to server
     - Routed to register 
            ```app.use('register', register)```
      - Mongoose creates new user using model 
        - Fires off pre.save function 
          - Bcrypt --> popular encryption library (package) - runs in node
          - Generate SALT 
              ```javascript 
              bcrypt.genSalt(SALT_WORK_FACTOR, function (err, salt){
              }
              ```
          - Generate Hash
              ```javascript 
              bcrypt.hash(user.password, salt, function (err, hash){  
              }
              ```
        - Tells it to go to the next step 
          ```javascript
          Next()
          ``` 
        - Saved in DB
      - If successs account is created in db
        ```javascript
        res.redirect('/'); 
        ```
        pretend like there was a new request for /
        
 ### Logging In
  - Post to server at / 
  - Go to index route
  ```javascript
    router.pose ('/',
      passport.authenticate('local', {   
        //--> directed to user.strategy.is
      }
  ```
  - Creates mongoose model from user info
  - Finds user based on username given
  - Compare password from user to the password in db
  - Create Session on Server --> store something about this session on the server and users browser
    - Serialize user --> creates serialized ID (random) on server
    - Stores id from DB so that when they loggin again it is easy
    - These can have time limits --> when request from browser if session is expired it will not have temporary session so you will have to login 
  - Creates cookie on browser --> little bit in info
    - Passport usually puts serialized ID from server into the cookie on browser : these two must match to make request
    - Session cookie only lasts until the browser is closed 
    - If you delete cookie and refresh you will be logged out
  - successRedirect:'/user' --> this stays within express/node, only on SERVER , directs to router
    - At this point we have still not yet responded to the browser
  - In response on client --> redirect user to user page
   
### User
  - Every request will now come with a cookie --> passport will make use of this
  - On page load controller sends $http request
     - Cookie is sent automatically 
  - Passport adds req.user to the request object
    - req.user --> 
      - want this exist on request object only if they are logged in 
  - Check if user is logged in
    - req.isAuthenticated() 
      - must use on every route you want protected

  ![alt text](LectureNotes/passportAuth.jpg)
 
  
