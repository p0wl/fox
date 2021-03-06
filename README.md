**fox** is a new JavaScript testing framework running on NodeJS and browsers. 
Assuming write NPM compatible code, it doesn't require any additional config, HTML files or any such kind of ceremonies, 
just let's you write and run tests in such a simple and quick way.

```bash
$ npm install -g fox
```

# USAGE

Create a new test document and name it `test.js`. [ChaiJS'](http://chaijs.com) `expect` and `assert` modules are injected by default;

```js
describe('Number', function(){

  it('converts a date to a number', function(){
      
      expect( Number(new Date) ).to.be.a('number')
      
  })

})
```

### Run On NodeJS:

```bash
$ fox test # Globbing and multiple parameters are enabled.
OK, passed 1 test.
```

![](https://dl.dropbox.com/s/agkrqwdrw3jlfhs/fox_cli.png?token_hash=AAET5mc15WE-bx9WlW0CLmZwk4N0K0qgcT9PMh72NX_KCA)

### Run On Browsers:

```bash
$ fox test -b # looks for modules like test.js or test/index.js by default.
Visit localhost:7559 to run tests on a web browser
```

Once you pass `-b` parameter, fox [compiles the whole NPM package with related
test modules](https://github.com/azer/fox/blob/master/lib/browser.js#L18) and [publishes](https://github.com/azer/fox/blob/master/lib/server.js#L19) [a web page](https://github.com/azer/fox/blob/master/web/index.html) where you can run and see the test results.

![](https://dl.dropbox.com/s/vxqjrcs21lkyu31/fox_browsers.png?token_hash=AAGmgetvrDsTtDSypyyWiI1jhH2rJqQkBSrghjypyj2k1Q)

# BDD API

before, beforeEach, describe, it, afterEach, after

# CLI API

```
    USAGE

        fox [modules] [options]

    OPTIONS

        -b    --browser    Publishes the tests on localhost:7559
        -g    --grep       Run tests matching with given pattern
        -t    --timeout    Set test-case timeout in milliseconds [2000]
        -v    --version    Show version and exit
        -h    --help       Show help and exit
```

# JavaScript API

Fox exposes an API that you can observe the testing progres... E.g; 

```js

describe('#Foo', function self(){
  
  self.testsuite.onError(function(error, test){
    
    console.log('%s throws %s', test.title, error)
    
  })
  
  it('will sing us a rap song', function(){
    
    throw new Error('fails immediately')
    
  })
 
})

```

Observing errors thrown by all testsuites; 

```js
var fox = require('fox');

fox.suites.onError(function(updates){
  
  errors.forEach(function(update){
  
    var error = update.params[0],
        test = update.params[1];
    
    console.log('%s throws %s', test.title, error.message);
    
  })
  
});

```

# Migrating From Mocha

Unless you have nested `describe` calls, Fox can run your Mocha tests.
