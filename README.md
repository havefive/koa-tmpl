# koa-tmpl
A template project with eggjs and parse-server
(中文版本请参看[这里](./README_CN.md))

# Please read first 
https://github.com/eggjs/egg

https://github.com/parse-community/parse-server

# Examples

https://github.com/eggjs/examples

# Steps

1. install eggjs and init project
```
$ npm install egg-init -g
$ egg-init --type simple showcase && cd showcase
$ npm install
$ npm run dev
$ open http://localhost:7001

```
2. intall Parse-server

```
npm install parse-server --save
```
3. edit index.js

```

'use strict';
var ParseServer = require('parse-server').ParseServer;
var databaseUri = process.env.DATABASE_URI || process.env.MONGODB_URI;
var databaseUri = 'mongodb://localhost:27017/dev';

if (!databaseUri) {
  console.log('DATABASE_URI not specified, falling back to localhost.');
}

var api = new ParseServer({
  databaseURI: 'mongodb://localhost:27017/dev',
  cloud: process.env.CLOUD_CODE_MAIN || __dirname + '/cloud/main.js',
  appId: 'appId',
  masterKey: 'key', //Add your master key here. Keep it secret!
  serverURL: 'http://localhost:1370/parse',  // Don't forget to change to https if needed
  liveQuery: {
    classNames: ["Posts", "Comments"] // List of classes to support for query subscriptions
  },
  appName: 'Parse App',
  // The email adapter
  publicServerURL:''
});

// npm run dev DO NOT read this file

var port = process.env.PORT || 1370;
var httpServer = require('http').createServer();
httpServer.listen(port, function() {
    console.log('parse-server-example running on port ' + port + '.');
});

// This will enable the Live Query real-time server
ParseServer.createLiveQueryServer(httpServer);

require('egg').startCluster({
  baseDir: __dirname,
  port: process.env.PORT || 7001, // default to 7001
});



```
parse-server will work on port 1370


To be continued

