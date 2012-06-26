
# SuperTest

  HTTP assertions made easy via [super-agent](http://github.com/visionmedia/superagent).

## About

  The motivation with this module is to provide a high-level abstraction for testing
  HTTP, while still allowing you to drop down to the lower-level API provided by super-agent.

## Example

  You may pass an `http.Server`, or a `Function` to `request()` - if the server is not
  already listening for connections then it is bound to an ephemeral port for you so
  there is no need to keep track of ports.

  SuperTest works with any test framework, here is an example without using any 
  test framework at all:

```js
var request = require('./')
  , express = require('express');

var app = express();

app.get('/user', function(req, res){
  res.send(201, { name: 'tobi' });
});

request(app)
  .get('/user')
  .expect('Content-Type', /json/)
  .expect('Content-Length', '20')
  .expect(201)
  .end(function(err, res){
    if (err) throw err;
  });
```