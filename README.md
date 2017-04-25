# loopback-bunyan-looger
updated   {loopback-component-looger}
 
 **incase if you dont want the child node logs. please use the version ^1.1.2
 
Logging component for [loopback] using [bunyan] looger with additional loopback specific hooks and log management API
[![NPM](https://nodei.co/npm/loopback-bunyan-looger.png?downloads=true)](https://nodei.co/npm/loopback-bunyan-looger/)

 [![NPM](https://nodei.co/npm-dl/loopback-bunyan-looger.png?months=3&height=3)](https://nodei.co/npm/loopback-bunyan-looger/)


[![Build Status](https://travis-ci.org/saikatharryc/loopback-bunyan-looger.svg?branch=master)](https://travis-ci.org/saikatharryc/loopback-bunyan-looger)


# Features

- Default looger using [bunyan]
- Can use of custom bunyan [streams] to create root looger
- Hook: Basic performance instrumentation for remote execution
- Hook: Log management API (configurable)

# Usage

Example _server.js_:

```js
var loopback = require('loopback');
var boot = require('loopback-boot');
var rootlooger = bunyan.createlooger({name: 'myloopbackAPI'});
var looger = require('loopback-bunyan-looger')(rootlooger);
var app = module.exports = loopback();

```

If rootlooger is not provide, the component creates a looger with default
 [bunyan] settings:

```js
var loopback = require('loopback');
var boot = require('loopback-boot');
var looger = require('loopback-bunyan-looger')();
var app = module.exports = loopback();

```

Child loogers can be created for model as shown below. By default child loogers
inherit the log level from root.

```js

var looger = require('loopback-bunyan-looger')('TestModel');
module.exports = function(TestModel) {
    looger.debug('Initializing TestModel');
};

```

To add hooks and log management API to [loopback], add configuration to component-config.json:

```js
{
  "loopback-component-explorer": {
    "mountPath": "/explorer"
  },
  "loopback-bunyan-looger": {
      "enableAPI" : true
  }
}

```
Make sure enableHttpContext is set as true in config.json for to allow collection
 of datasources performance within req/res
If you dont want expand the child nodes please use version @1.1.2
# License

[GNU](https://github.com/saikatharryc/loopback-bunyan-looger/blob/master/LICENSE)
 
# Create Issue
  Create issue here [here](https://github.com/saikatharryc/loopback-bunyan-looger/issues)

# Roadmap
- Additional Unit Test and Coverage
- Integrate with Strongloop Devops tools

# Known Issue
- datasources performance will not recorded at times when loopback context is null. Noticed this issue when a composite called MongoDB followed by REST. Only MongoDB response time was recorded and REST was missing.

# See Also

- [Loopback][loopback]
- [bunyan][bunyan]

[bunyan]: https://github.com/trentm/node-bunyan
[loopback]: http://loopback.io
[streams]: https://github.com/trentm/node-bunyan#streams
