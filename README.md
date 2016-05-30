# electron-log
[![Build Status](https://travis-ci.org/megahertz/electron-log.svg?branch=master)](https://travis-ci.org/megahertz/electron-log)
[![npm version](https://badge.fury.io/js/electron-log.svg)](https://badge.fury.io/js/electron-log)

## Description

Just a very simple logging module for your Electron application.
No dependencies. No complicated configuration. Just require and use.
Also it can be used without Electron.

By default it writes logs to the following locations:

 * **on Linux:** `~/.config/<app name>/log.log`
 * **on OS X:** `~/Library/Logs/<app name>/log.log`
 * **on Windows:** `$HOME/AppData/Roaming/<app name>/log.log`

## Installation

Install with [npm](https://npmjs.org/package/comments-parser):

    npm install electron-log

## Usage

```js
var log = require('electron-log');

log.info('Hello, log');
```
    

### Transport
Transport is a simple function which requires an object which describes a message.
By default, two transports is active: console and file. The file path is 
depend on current platform.

#### Disable default transport:

```js
log.transport.file = false;
log.transport.console = false;
```
    
#### Override transport:

```js
log.transports.console = function(msg) {
  console.log(`[${msg.date.toLocaleTimeString()} ${msg.level}] ${msg.text}`);
};
```
    
#### Console Transport

```js
// Log level
log.transports.console.level = 'warning';

/** 
 * Set output format template. Available variables:
 * Main: {level}, {text}
 * Date: {y},{m},{d},{h},{i},{s},{ms}
 */
log.transports.console.format = '{h}:{i}:{s}:{ms} {text}';

// Set a function which formats output
log.transports.console.format = (msg) => msg.text;
```
    
#### File transport

```js
// Same as for console transport
log.transports.file.level = 'warning';
log.transports.file.format = '{h}:{i}:{s}:{ms} {text}';

// Write to this file, must be set before first logging
log.transports.file.file = __dirname + '/log.txt';

// fs.createWriteStream options, must be set before first logging
log.transports.file.streamConfig = { flags: 'w' };

// set existed file stream
log.transports.file.stream = fs.createWriteStream('log.txt');
```

## License

Licensed under MIT.