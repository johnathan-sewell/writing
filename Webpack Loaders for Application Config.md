# Webpack Loaders for Application Config

Most of the Node.js based apps I work on use a configuration module to read in environment variables or command ine args on the server side, and output a configuration object tha the rest of the app can use.

We use a handy library called [Konfiga](https://github.com/chrisnewtn/konfiga) (Chris Newton) which gives your app a global configuration object built from environment and command line arguments.

But... if your app is static and doesn't run in or server from Node.js, you need a build step to generate the static config file for you, I've done this via a Webpack Loader.

### Config via a Webpack Loader

This example application is configurable via command line args, as seen in the scipts section of package.json:

```JSON
"scripts": {
    "dev": "webpack --watch",
    "production": "webpack --socket-host=http://123.123.123.123 --socket-port=3000"
}
```

The `socket-host` and `socket-port` arguments are used in this app to connect to a WebSockets server. I'm using a JSON config file, this is what it looks like:

```JSON
{
    "socketHost": {
        "defaultValue": "http://127.0.0.1",
        "cmdLineArgName": "socket-host"
    },
    "socketPort": {
        "defaultValue": "3000",
        "cmdLineArgName": "socket-port"
    }
}
```

Now, in order to convert this JSON into JavaScript configuration I can use in the app, I use a Webpack Loader (and Konfiga). The loader reads in the cong JSON, parses it to a JavaScript object, and uses Konfiga to fill in the required commnd line args:

```JavaScript
const konfiga = require('konfiga');

module.exports = function(content) {
    const config = konfiga(JSON.parse(content));
    return `module.exports = ${JSON.stringify(config)};`;
};
```

The resulting configuration comes out in Webpack like this:
```JavaScript
/***/ function(module, exports) {
	module.exports = {"socketHost":"http://213.219.38.100","socketPort":"3000"};
/***/ }
```

So configuration is now loaded wherever it's needed in the app:
```JavaScript
const appConfig = require('./config/konfigaLoader!./config/appConfig');

// appConfig is an object:
//{
// 	socketHost: 'http://213.219.38.100',
// 	socketPort: '3000'
// }
```
