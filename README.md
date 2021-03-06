# EASY_RESTFUL.JS
[![npm](https://img.shields.io/npm/v/pixel-js-k.svg)](https://www.npmjs.com/package/easy-restful)
[![travis](https://travis-ci.org/keicoon/easy-restful.js.svg?branch=master)](https://travis-ci.org/keicoon/easy-restful.js)
## Features
- Provice simple design to restful-api service and support `npm` module.
- Support customize `server`, `db-server`.
    - Using default server `express`.
    - Using default db-server `redis`.
## Install
```
npm i easy-restful
```
## UseCase
### start
```
const EasyRestful = require('easy-restful.js').default;
// # in mac
// const EasyRestful = require('easy-restful.js').get({
//     'redis-server-bin-path': '/Users/jo/Downloads/redis-server',
//     'saved-file-path': '/Users/jo/Documents/easy-restful.js/saved/redisdb.json'
// });
// # in win
// const EasyRestful = require('easy-restful.js').get({
//     'redis-server-bin-path': 'C:\\Program Files\\Redis\\redis-server.exe',
//     'redis-server-conf': 'C:\\Program Files\\Redis\\conf\\redis-dist.conf',
//     'saved-file-path': __dirname + '\\..\\data\\db.json'
// });
```
### register simple restful-api
```
const key = EasyRestful.register('/hello', function (resolve, reject) {
    resolve('hello restful api world');
});

EasyRestful.register('/helloJson', function (resolve, reject) {
    resolve({ "a": 1, "b": "bb" });
});
```
### unreigister restful-api
```
EasyRestful.register('/stopHello', function (resolve, reject) {
    EasyRestful.unrgister(key);
    resolve('success: stophello');
});
```
### using db
```
EasyRestful.register('POST', '/dbAdd/:value', function (resolve, reject) {
    this.db.set('key', this.params.value)
    resolve(`[success] dbAdd : ${this.params.value}`);
});

EasyRestful.register('/dbGet', function (resolve, reject) {
    this.db.get_callback('key', (value) => {
        resolve(value);
    });
    // this.db.get('key').then(value => {
    //     resolve(value);
    // });
});
```
### log
```
EasyRestful.register('/log', function (resolve, reject) {
    resolve(EasyRestful.log, false);
});
```
### close
```
EasyRestful.close();
```

## History
- v0.1.3
    - add port option
- v0.1.2
    - support https
- v0.1.1
    - support windows
- v0.1.0
    - first release