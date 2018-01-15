# QVM.js
MeagaQuery is a database that is designed to search billions of key's that are similar, like a license plate number or a [GeoKey](https://github.com/lakefox/geokey), and runs on very low end hardware like a laptop.

### Running:

First download this qvm
```
npm install qvm
```
then run it in your application 
```
const qvm = require('qvm');
qvm.startServer(8080); // Your can use any port you want

// rest of your code
```

### Storing a value
#### HTTP

```
curl "http://localhost:8080/qvm/?key=KEY&value=VALUE"

Outputting
>>> {sucess: true}
```
#### Node.JS
``` javascript
qvm.api({
  key: KEY,
  value: VALUE
}, (logs) => {
  // logs >> {sucess: true}
});
```
Replace KEY with the key you want to look up the value with, and replace VALUE with the data you want to store.

### Error's
```
curl "http://localhost:8080/qvm/?key=KEY&value=VALUE"

Outputting
>>> {error: 'file exists, overwrite with &overwrite=true'}
```
This means you are trying to write over a existing file but you can fix it by doing this
#### HTTP
```
curl "http://localhost:8080/qvm/?key=KEY&value=VALUE&overwrite=true"

Outputting
>>> {sucess: true}
```
#### Node.JS
``` javascript
qvm.api({
  key: KEY,
  value: VALUE,
  overwrite: "true" // this has to be a string
}, (logs) => {
  // logs >> {sucess: true}
});
```
### Reading a value
#### HTTP
```
curl "http://localhost:8080/qvm/?q=KEY"

Outputting
>>> VALUE
```
#### Node.JS
``` javascript
qvm.api({
  q: KEY
}, (data) => {
  // Do Whatever
});
```
Replace KEY with the key you previously used to store the value, VALUE is what ever you stored on the server with the KEY

### Error's
#### HTTP
```
curl "http://localhost:8080/database/?q=KEY"

Outputting
>>> {error: 'value doesn't exist'}
```
This means you haven't stored any values with the corresponding key

