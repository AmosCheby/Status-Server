# Status-Server

##### An API that helps users check if a webpage is up or down and prompts users with a text message if the state of saved sites changes

# API Structure

### dependency tree

           index 
             |   
       ----    ----   
       |           |
       |           |         
    server      workers     
       |           |         
       |           |              
     handlers     logs        
       |           |      
       |           |        
       |-----------|
             |
             |
           helpers
             |
             |
           data
             |
             |
          config
          
          index--initializes the server and workers.
          
          servers---handles all user request and response.
          
          workers-----handles all data logs and checks.
          
          handlers---hanldles all routes on the server.
          
          logs----handles creation of logfiles and their compression and update.
          
          helpers---handles hashing of passwords, parsing payload to json , texting users, creating.
          
          data----handles file creation and data extraction.
          
          config---handles environment configuration.
        
 
# User Guide

#### id serves as a private key while publickey serves as a public key
## Routes

### /ping

##### Method for generating public keys

```bash

const options = {
  method: 'GET',
};

fetch('https://status.up.railway.app/ping', options)
  .then(response => response.json())
  .then(response => console.log(response))
  .catch(err => console.error(err));
  
  ```
  
  ### /tokens
  
  ### A token is a a key needed by a user to edit data i.e a token is required to:
  #### POST
  
  ##### used to create a token, reqiured parameters are
  
  ###### payload
  
  - phone
  - password

you can only used the phone password you used in creating a user

```bash

const options = {
  method: 'POST',
  headers: {publickey: 'k7d5ih4q27nwicpxw3tr'},
  body: '{"password":"lightighvt","phone":"8022623069"}'
};

fetch('https://status.up.railway.app/tokens', options)
  .then(response => response.json())
  .then(response => console.log(response)) // returns { phone, id, expires }
  .catch(err => console.error(err));
  
  ```
  
  #### GET
  
  ##### used to get user stored data reqires
  
  ###### headers
  - id
  
  ###### query
  - phone
  - password
 
 ```bash
 const options = {
  method: 'GET',
  headers: {publickey: 'k7d5ih4q27nwicpxw3tr', id: '5fjikzbymsxi036o2ebf'}
};

fetch('https://status.up.railway.app/tokens?id=usg3t5war42alp6jck0j', options)
  .then(response => response.json())
  .then(response => console.log(response))
  .catch(err => console.error(err));
  ```
  #### PUT
  
  ##### used to update token data or extend expiration time by a day, requires
  
  ###### headers
  - id
  
  ###### payload
  - firstName (optional)
  - lastName (optional)
  - password (optional)
  - phone (required)
  
```bash 
const options = {
  method: 'PUT',
  headers: {publickey: 'k7d5ih4q27nwicpxw3tr', id: '7afrngqinomsv37pt1g0'},
  body: '{"id":id,"extend":true}'
};

fetch('https://status.up.railway.app/tokens', options)
  .then(response => response.json())
  .then(response => console.log(response))
  .catch(err => console.error(err));
  
 ```
#### DELETE

##### used to delete a token's data, requires

  ###### headers
  - id
  
  ###### payload
  - phone
 
```bash
const options = {
  method: 'DELETE',
  headers: {publickey: 'k7d5ih4q27nwicpxw3tr', id: '7afrngqinomsv37pt1g0'}
};

fetch('https://status.up.railway.app/users?id=id', options)
  .then(response => response.json())
  .then(response => console.log(response))
  .catch(err => console.error(err));
  
  ```
  
  

  

  ### /users
  
  #### POST
  
  ##### used to create a user, reqiured parameters are
  
  ###### payload
  
  - firstName
  - lastName
  - phone
  - password
  - tosAgreement

```bash

const options = {
  method: 'POST',
  headers: {publickey: 'k7d5ih4q27nwicpxw3tr', id: '7afrngqinomsv37pt1g0'},
  body: '{"lastName":"onyela","firstName":"Udoka","password":"lightighvt","countrycode":"234","phone":"8022623069","tosAgreement":true}'
};

fetch('https://status.up.railway.app/users', options)
  .then(response => response.json())
  .then(response => console.log(response))
  .catch(err => console.error(err));
  
  ```
  
  #### GET
  
  ##### used to get user stored data reqires
  
  ###### headers
  - id
  
  ###### query
  - phone
 
 ```bash
 
 const options = {
  method: 'GET',
  headers: {publickey: 'k7d5ih4q27nwicpxw3tr', id: '7afrngqinomsv37pt1g0'}
};

fetch('https://status.up.railway.app/users', options)
  .then(response => response.json())
  .then(response => console.log(response))
  .catch(err => console.error(err));
  
  ```
  #### PUT
  
  ##### used to update user data requires
  
  ###### headers
  - id
  
  ###### payload
  - firstName (optional)
  - lastName (optional)
  - password (optional)
  - phone (required)
  
```bash 
const options = {
  method: 'PUT',
  headers: {publickey: 'k7d5ih4q27nwicpxw3tr', id: '7afrngqinomsv37pt1g0'},
  body: '{"lastName":"onyela","firstName":"Udoka","password":"lightighvt","countrycode":"234","phone":"8022623069","tosAgreement":true}'
};

fetch('https://status.up.railway.app/users', options)
  .then(response => response.json())
  .then(response => console.log(response))
  .catch(err => console.error(err));
  
 ```
#### DELETE

##### used to delete a user's data requires

  ###### headers
  - id
  
  ###### payload
  - phone
 
```bash
const options = {
  method: 'DELETE',
  headers: {publickey: 'k7d5ih4q27nwicpxw3tr', id: '7afrngqinomsv37pt1g0'}
};

fetch('https://status.up.railway.app/users?phone=8022623069', options)
  .then(response => response.json())
  .then(response => console.log(response))
  .catch(err => console.error(err));
  
  ```
  ### /checks
  #### POST
