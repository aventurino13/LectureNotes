Passport Authentication
===

Three possible senarios/ states for user
  1. No Account
  2. Create Account --> username password
  3. Logging In --> all following requests
 
  app repo:
  https://github.com/aventurino13/prime-passport-lectures
    - Angular application
   
   App.js
   - Order matters and it must run in a specific order to function
   - 
 
 Passport 
   - Helps node projects make sure a user is authenticating
   - Different strategies for authentication
    - No matter what strategy you used you will have req.user 
   
1. Creating Account
  - Make post request to server
     - routed to register 
            ```app.use('register', register)```
      - mongoose creates new user using model 
        - fires off pre.save function 
          - generate SALT 
              ```javascript 
              bcrypt.genSalt(SALT_WORK_FACTOR, function (err, salt){
              }```
          - generate Hash
              ```javascript bcrypt.hash(user.password, salt, function (err, hash){  
              }```
        - ```Next()``` Tells it to go to the next step
        - Saved in DB
      - If successs account is created in db
        ```res.redirect('/');``` --> pretend like there was a new request for /
