# Bexio
[![Dependencies](https://david-dm.org/mathewmeconry/bexio/status.svg)](https://david-dm.org/mathewmeconry/bexio)
[![Known Vulnerabilities](https://snyk.io/test/npm/bexio/badge.svg)](https://snyk.io/test/npm/bexio)
[![codecov](https://codecov.io/gh/mathewmeconry/bexio/branch/master/graph/badge.svg)](https://codecov.io/gh/mathewmeconry/bexio)
[![Tests](https://github.com/mathewmeconry/bexio/workflows/Test/badge.svg)](https://github.com/mathewmeconry/bexio/actions)
[![Publish](https://github.com/mathewmeconry/bexio/workflows/Publish/badge.svg)](https://github.com/mathewmeconry/bexio/actions)
![npm](https://img.shields.io/npm/v/bexio)

## Description
**Basic build and NPM-Package is in ES6!**

NPM Package for the API of [Bexio](https://www.bexio.com)

## Typings
The typings for the module are already included in the package

## API Documentation
The whole documentation of the API can be found here: [https://docs.bexio.com/](https://docs.bexio.com/)

## Support
NodeJS >= 10.0

## Functions
### Implemented
You can find a list of all implements functions in the [wiki](https://github.com/mathewmeconry/bexio/wiki)

### Missing
You can find a list of all missing functions here: [Missing Functions](https://github.com/mathewmeconry/bexio/wiki#missing-functions).  
If you need a function implemented, please fill out an issue.

### Additional
#### fake login
This can be used to automatically generate an access token without user input.  
The function returns the following object:
```javascript
{
    access_token: string,
    expires_in: number,
    refresh_token: string,
    org: string,
    user_id: number,
    valid_until: Date
}
```

## TLTR;
### get the auth url for the bexio authentication
```javascript
const Bexio = require('bexio');

// initialize the object
const bexioApi = new Bexio.default('CLIENT_ID', 'CLIENT_SECRET', 'http://127.0.0.1/callback', [Bexio.Scopes.CONTACT_SHOW]);

// get the auth url
bexioApi.getAuthUrl()
```

### get the access token
```javascript
bexioApi.generateAccessToken("QUERY_STRING_OF_THE_BEXIO_RESPONSE")
```


### check if it is initialized properly
```javascript
bexioApi.isInitialized()
```

### refresh the token
gets handled by the package

## Example with express
List all contacts ordered by name
```javascript
const Bexio = require('bexio');
const express = require('express');
const createServer = require('http').createServer;

// initialize the object
const bexioApi = new Bexio.default('CLIENT_ID', 'CLIENT_SECRET', 'http://127.0.0.1/callback', [Bexio.Scopes.CONTACT_SHOW]);

// initialize express and server
const app = express();
const server = createServer(app);

// redirect the user to the Bexio login page
app.get('/', (req, res) => {
    if(!bexioApi.isInitialized()) {
        res.redirect(bexioApi.getAuthUrl())
    } else {
        res.redirect('/list_contacts')
    }
});

// receive the callback of the bexio login page and get the access token
app.get('/callback', (req, res) => {
    bexioApi.generateAccessToken(req.query).then(() => {
        res.send('success')
    }).catch(err => {
        res.send(err)
    });
});

// list all contacts
app.get('/list_contacts', (req, res) => {
    bexioApi.contacts.list({ order_by: 'name_1' }).then(contacts => {
        res.send(contacts)
    }).catch(err => {
        res.send(err)
    })
});

// listen on port 3000
server.listen(3000, () => {
    console.log('Listening on port 3000')
});
```

## Fake login
### preinitialized API
```javascript
const Bexio = require('bexio');

// initialize the object
const bexioApi = new Bexio.default('CLIENT_ID', 'CLIENT_SECRET', 'http://127.0.0.1/callback', [Bexio.Scopes.CONTACT_SHOW]);

bexioApi.fakeLogin('USERNAME', 'PASSWORD').then(res => {
    if(res) {
        console.log(res)
    } else {
        console.log('Failed')
    }
}).catch(err => {
    console.log('Failed')
    console.log(err)
})

```
### static variant
```javascript
const Bexio = require('bexio');

Bexio.fakeLogin('CLIENT_ID', 'CLIENT_SECRET', [Bexio.Scopes.CONTACT_SHOW], 'USERNAME', 'PASSWORD').then(res => {
    if(res) {
        console.log(res)
    } else {
        console.log('Failed')
    }
}).catch(err => {
    console.log('Failed')
    console.log(err)
})
```


## Contributing
1. Fork it!
2. Create your feature branch: `git checkout -b my-new-feature`
3. Commit your changes: `git commit -am 'Add some feature'`
4. Push to the branch: `git push origin my-new-feature`
5. Submit a pull request :D


## License
MIT
