type `npm run` to see a list of the available npm scripts (I always used `cat package.json` before I know about this)

pre and post hooks are useful for example if you want to run a lint script before the test script
```json
"scripts": {
  "lint": "jshint *.js",
  "test": "mocha",
  "pretest": "npm run lint"
}
```
http://www.sitepoint.com/guide-to-npm-as-a-build-tool/

* use `&&` to call one task after another (`&` to fork), use pipe `|` to pipe output between commands
