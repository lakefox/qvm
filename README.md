# QVM.js
QVM is a wrapper that runs over [MEGAQUERY](https://github.com/lakefox/megaquery) that provides an increible amount of encryption to you database. 

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
qvm.startServer is optional only if you want a http api. !WARNING this is NOT secured do not open this api to anyone only server's or a trusted endpoint!

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
#### Versioning
Whenever you store a value the value is stored in a blockchain, that means this database is append only. So when you query the database it returns the most recent value stored but every change is stored on the database so you can request old values but you can't remove a value this is useful because you are able to keep a record of every change in a value. [Read more on append only databases](http://usblogs.pwc.com/emerging-technology/the-rise-of-immutable-data-stores/)
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
Replace KEY with the key you previously used to store the value
### Reading old versions
#### HTTP
```
curl "http://localhost:8080/qvm/?q=KEY&block=0"

Outputting
>>> VALUE
```
#### Node.JS
``` javascript
qvm.api({
  q: KEY,
  block: 0
}, (data) => {
  // Do Whatever
});
```
Replace block with the index of the data you want to find, the versioning works like an array starting at 0 and going up from there.
### Error's
#### HTTP
```
curl "http://localhost:8080/qvm/?q=KEY"

Outputting
>>> {error: 'value doesn't exist'}
```
This means you haven't stored any values with the corresponding key

```
curl "http://localhost:8080/qvm/?q=KEY&block=12938108"

Outputting
>>> {error: 'block out of range: block < 3'}
```
This means that there are < 3 versions stored on the server so you need to pick a value between 0-2
