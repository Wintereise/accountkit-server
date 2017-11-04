# accountkit-server

Account Kit helps you quickly register for apps using just your phone number or email address — no password needed. It's reliable, easy to use and gives you a choice about how you sign up for apps.

accountkit-server is a nodeJS module based on [node-accountKit](https://github.com/taina0407/node-accountkit) to handle accountkit server side implementation.

The main change between this and [node-accountkit](https://github.com/taina0407/node-accountkit) is replacing callbacks with promises which allows for the use of async/await functions when compiled in ES6+

Other optimizations have been made too.

Full documentation for account kit can be found here [https://developers.facebook.com/docs/accountkit/web](https://developers.facebook.com/docs/accountkit/web)

### Version
0.45.0

### Installation

#### NPM

```sh
npm install --save accountkit-server
```

#### Yarn

```sh
yarn add accountkit-server
```

# Usages

**Step 1** Include module to your entry `.js` file

#### ES5 (and below)
```javascript
var AccountKit = require('accountkit-server');
```

#### ES6+
```javascript
import AccountKit from 'accountkit-server';
```

**Step 2** Configure account kit.
```javascript
Accountkit.configure('<APP_ID>', '<ACCOUNT_KIT_APP_SECRET>'); 

/**
* Default value is true
**/

AccountKit.requireAppSecret(true); 
```

More information [https://developers.facebook.com/apps/](https://developers.facebook.com/apps/)


**Step 4** Use it.

### Promises
```javascript

/**
* Get account info
* @param {authorizationCode} The authorization code recived from the client
**/

AccountKit.getAccountInfo(req.body.auth_code)
    .then((response) => {
        console.log(response);
        
        /**
        {
            "email": {
                "address": "mail.goyalshubham@gmail.com"
            },
            "id": "941488975973375"
        }
        */
    })
    .catch(error => {
        console.log(error);
    });

/**
* Removes the user's account
* @param {id} The AccountKit user's id.
** /

Accountkit.removeUser(accountId)
    .then((response) => {
        console.log(response);
        
        /**
        {
            success: true
        }
        */
    })
    .catch(error => {
        console.log(error);
    });
```

### ES7+ (async/await)
```javascript

try {
    let response = await AccountKit.getAccountInfo(req.body.auth_code);
} catch (e) {
    console.log(e);
}

```

```javascript
try {
    let response = await AccountKit.removeUser(accountId);
} catch (e) {
    console.log(e);
}
```

### Libary Methods

| Function       | Parameters                                  | Definition                                                                                                                    | Returns |
|----------------|---------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|---------|
| getAccountInfo | authorizationCode: String                   | Returns the user from the auth code sent from the client. This information can be used to create a new User in the database.  | Promise |
| removeUser     | id: String                                  | Removed the user from AccountKit via the identifier given from getAccountInfo                                                 | Promise |
| configure      | id: String, secret: String, version: Strign | Configures the AccountKit kit app with the provided information                                                               | Null    |                                        |         |   |

### Contribute

Read the CONTRIBUTING.md file.
