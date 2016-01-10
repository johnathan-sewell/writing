# Application Config with Webpack Loaders

Many Node.js based apps use a configuration module to read in environment variables or command ine args on the server side, and output a configuration object tha the rest of the app can use.

## Config without Node.js

Even a single HTML/JavaScript page could have configuartion passed to it from Node.js, provided it is served up by a Node.js server. (You could pass configuration values in a cookie or inject it into the HTML when Node is serving it). But... there are cases where Node.js is not serving up your application. In my case this was in a Chrome extension.

## Webpack

We use Webpack in the Chrome extension because it allows us to use ES2015 (expecially Modules) via [babel-loader](https://github.com/babel/babel-loader).

### Config via a Webpack Loader

The extension is configurable via command line args:

```JSON
"scripts": {
    "dev": "webpack --watch",
    "production": "webpack --socket-host=http://123.123.123.123 --socket-port=3000"
  },
```

TO be able to easily switch between running the Chrome extension in development against various test servers, and switch it to run in production
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
