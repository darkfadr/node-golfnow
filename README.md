#Golf Now API

[![npm](https://img.shields.io/npm/v/node-golfnow.svg)](https://www.npmjs.com/package/node-golfnow) 
[![npm](https://img.shields.io/npm/dt/nodegolfnow.svg)](https://www.npmjs.com/package/nodegolfnow) 
[![Build Status](https://travis-ci.org/darkfadr/node-golfnow.svg?branch=master)](https://travis-ci.org/darkfadr/node-golfnow)

> Promise based API library that exposes an abstraction over the GolfNow Affiliate API. Doing this cause I didn't like the implementation of another solution.

[![forthebadge](http://forthebadge.com/images/badges/no-ragrets.svg)](http://forthebadge.com)
[![forthebadge](http://forthebadge.com/images/badges/makes-people-smile.svg)](http://forthebadge.com)
[![forthebadge](http://forthebadge.com/images/badges/built-with-love.svg)](http://forthebadge.com)

## Installation
`$ npm install --save node-golfnow`

## Usage
```javascript
import golfnow from 'node-golfnow';
//const golfnow = require('golfnow'); // for non import env

const api = golfnow({
	client_id: 'insert client id here',
	client_secret: 'supper secret client key right here',
	channel_id: 19189 //optional || default is 1
});

api.root()
	.then(res => console.log(res.data));
	.catch(err => console.log(err.response.data));
```

## API
At it's core `node-golfnow` uses `axios`. It currently exposes abstactions around the `[root, channels, course, courses, rateTags, invoices]` resouces of the API, however any missing or new enpoint can be implemented via the the extension `get` and `post` methods

### Root
```javascript
api.root()
	.then(res => console.log(res.data));
	.catch(err => console.log(err.response.data));
```

### Setting API context
**Important: you must use the `.setChannel([chanel_id:required])` method to establish the context in which your API runs in.**  _I know...I know...this is dictated by the API, but hopefully in the near future this can be abstracted that out :)_
```javascript
api.setChannel(12345);
```


### Channels
If a channel is not passed, then it will return a list of channels that you have access to.
```javascript
api.channels([channel_id:optional])
	.then(res => {
		api.setChannel(/*le channel id*/)
		console.log(res.data)
	});
	.catch(err => console.log(err.response.data));
```

### Custom endpoints
The sdk exposes the `get` and `post` methods for customized integration with the GolfNow Affiliate API

```javascript
const channel = api.getChannel();

api.get(`/channels/${channel}/customers/${customer-email}/reservations/${reservation-id}`)
	.then(res => console.log(res.data));
	.catch(err => console.log(err.response.data));


app.post(url, payload)
	.then(res => console.log(res.data));
	.catch(err => console.log(err.response.data));
```

## Tests
`$ npm test`

## Contributors
Ashley Narcisse <ashlay49@gmail.com>
