# bip38grs

[![js-standard-style](https://cdn.rawgit.com/feross/standard/master/badge.svg)](https://github.com/feross/standard)

A JavaScript component that adheres to the [BIP38](https://github.com/bitcoin/bips/blob/master/bip-0038.mediawiki) standard to secure your crypto currency private keys. Fully compliant with Node.js and the browser (via Browserify).


## Why?
BIP38GRS is a standard process to encrypt Groestlcoin private keys that is impervious to brute force attacks thus protecting the user.


## Package Info
- github: [https://github.com/groestlcoin/bip38grs](https://github.com/groestlcoin/bip38grs)
- tests: [https://github.com/groestlcoin/bip38grs/tree/master/test](https://github.com/groestlcoin/bip38grs/tree/master/test)
- issues: [https://github.com/groestlcoin/bip38grs/issues](https://github.com/groestlcoin/bip38grs/issues)
- license: **MIT**
- versioning: [http://semver-ftw.org](http://semver-ftw.org)


## Usage

### Installation

    npm install --save bip38grs


### API
### encrypt(buffer, compressed, passphrase[, progressCallback, scryptParams])

``` javascript
var bip38 = require('bip38grs')
var wif = require('wifgrs')

var myWifString = '5KGUthnCyV7hxAp4EJ3wixaVmmBMgwj1Rps9AStA9j2DeQaihtk'
var decoded = wif.decode(myWifString)

var encryptedKey = bip38.encrypt(decoded.privateKey, decoded.compressed, 'TestingOneTwoThree')
console.log(encryptedKey)
// => '6PRJZa3mD7BM9Y2vpnPCZWoPsFgRXW79u7A3LtW6MifAnakB5bJ5pZY9oE'
```


### decrypt(encryptedKey, passphrase[, progressCallback, scryptParams])

``` javascript
var bip38 = require('bip38grs')
var wif = require('wifgrs')

var encryptedKey = '6PRJZa3mD7BM9Y2vpnPCZWoPsFgRXW79u7A3LtW6MifAnakB5bJ5pZY9oE'
var decryptedKey = bip38.decrypt(encryptedKey, 'TestingOneTwoThree', function (status) {
  console.log(status.percent) // will print the percent every time current increases by 1000
})

console.log(wif.encode(0x80, decryptedKey.privateKey, decryptedKey.compressed))
// => '5KGUthnCyV7hxAp4EJ3wixaVmmBMgwj1Rps9AStA9j2DeQaihtk'
```


# References
- https://github.com/bitcoin/bips/blob/master/bip-0038.mediawiki
- https://github.com/pointbiz/bitaddress.org/issues/56 (Safari 6.05 issue)
- https://github.com/casascius/Bitcoin-Address-Utility/tree/master/Model
- https://github.com/nomorecoin/python-bip38-testing/blob/master/bip38.py
- https://github.com/pointbiz/bitaddress.org/blob/master/src/ninja.key.js
