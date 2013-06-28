# getUserMedia

## What is this?

A tiny browser module that gives us a simple API for getting access to a user's camera or microphone by wrapping the `navigator.getUserMedia` API in modern browsers.

It gives us a cleaner node.js-style, error-first API and cross-browser handling. No browser support checking necessary, lack of support is treated in the same way as when the user rejects the request: the callback gets passed an error as the first argument.

Suitable for use with browserify/CommonJS on the client. 

If you're not using browserify or you want AMD support use `getusermedia.bundle.js`.


## Installing

```
npm install getusermedia
```

## How to use it


With this helper it's clean/simple to get access to a user's camera, mic, etc.

```js
var getUserMedia = require('getusermedia');

getUserMedia(function (err, stream) {
    // if the browser doesn't support user media
    // or the user says "no" the error gets passed
    // as the first argument.
    if (err) {
       console.log('failed');
    } else {
       console.log('got a stream', stream);  
    }
});
```

Passing in options is optional. It defaults to `{video: true, audio: true}`;

```js
// optionally pass constraints as the first argument
// they just passed through.
getUserMedia({video: true, audio: false}, function (err, stream) { ... });
```


## Why? Because it's super ugly without this tool

```js
// first deal with browser prefixes
var getUserMedia = navigator.getUserMedia || 
    navigator.mozGetUserMedia || 
    navigator.webkitGetUserMedia;

// make sure it's supported and bind to navigator
if (getUserMedia) {
    getUserMedia = getUserMedia.bind(navigator);
}

// then deal with a weird, positional error handling API
getUserMedia(
    // media constraints
    {video: true, audio: true}, 
    // success callback
    function (stream) {
        // gets stream if successful
    }, 
    // error callback
    function (error) {
        // called if failed to get media
    }
)
```



## License

MIT

## Created By

If you like this, follow: [@HenrikJoreteg](http://twitter.com/henrikjoreteg) on twitter.

