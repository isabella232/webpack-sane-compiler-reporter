# webpack-sane-compiler-reporter

[![NPM version][npm-image]][npm-url] [![Downloads][downloads-image]][npm-url] [![Build Status][travis-image]][travis-url] [![Coverage Status][codecov-image]][codecov-url] [![Dependency status][david-dm-image]][david-dm-url] [![Dev Dependency status][david-dm-dev-image]][david-dm-dev-url] [![Greenkeeper badge][greenkeeper-image]][greenkeeper-url]

[npm-url]:https://npmjs.org/package/webpack-sane-compiler-reporter
[npm-image]:http://img.shields.io/npm/v/webpack-sane-compiler-reporter.svg
[downloads-image]:http://img.shields.io/npm/dm/webpack-sane-compiler-reporter.svg
[travis-url]:https://travis-ci.org/moxystudio/webpack-sane-compiler-reporter
[travis-image]:http://img.shields.io/travis/moxystudio/webpack-sane-compiler-reporter/master.svg
[codecov-url]:https://codecov.io/gh/moxystudio/webpack-sane-compiler-reporter
[codecov-image]:https://img.shields.io/codecov/c/github/moxystudio/webpack-sane-compiler-reporter/master.svg
[david-dm-url]:https://david-dm.org/moxystudio/webpack-sane-compiler-reporter
[david-dm-image]:https://img.shields.io/david/moxystudio/webpack-sane-compiler-reporter.svg
[david-dm-dev-url]:https://david-dm.org/moxystudio/webpack-sane-compiler-reporter?type=dev
[david-dm-dev-image]:https://img.shields.io/david/dev/moxystudio/webpack-sane-compiler-reporter.svg
[greenkeeper-image]:https://badges.greenkeeper.io/moxystudio/webpack-sane-compiler-reporter.svg
[greenkeeper-url]:https://greenkeeper.io

Beautiful reporting for [webpack-sane-compiler](https://github.com/moxystudio/webpack-sane-compiler) compilation events.

<img src="images/output.png" alt="Example output" width="80%">


## Installation

`$ npm install webpack-sane-compiler-reporter --save-dev`


## Usage

```js
const startReporting = require('webpack-sane-compiler-reporter');

const { stop, options } = startReporting(compiler, {/* options */});

// Now, just call compiler.run() or compiler.watch() to start a compilation and start outputting reports
// Calling stop() will stop listening to the compiler events
// Furthermore, you have access to the options that were computed by the merge of provided options and the defaults
```

### Available options:

| Name   | Description   | Type     | Default |
| ------ | ------------- | -------- | ------- |
| stats | Display webpack stats after each compilation | boolean/string (`true`, `false` or `'once'`) | true |
| write | Function responsible for printing/outputting the generated report messages | function | Prints to `stderr` |
| [printStart](https://github.com/moxystudio/webpack-sane-compiler-reporter/blob/bf70f5cfd594219fd06ba81677b18ded34770df2/index.js#L18) | Function responsible for generating a message when a compilation starts | function | ![Example output](images/start.png) |
| [printSuccess](https://github.com/moxystudio/webpack-sane-compiler-reporter/blob/bf70f5cfd594219fd06ba81677b18ded34770df2/index.js#L19) | Function responsible for generating a message when a compilation succeeds | function | ![Example output](images/success.png) |
| [printFailure](https://github.com/moxystudio/webpack-sane-compiler-reporter/blob/bf70f5cfd594219fd06ba81677b18ded34770df2/index.js#L20)  |Function responsible for generating a message when a compilation fails | function | ![Example output](images/failure.png) |
| [printStats](https://github.com/moxystudio/webpack-sane-compiler-reporter/blob/bf70f5cfd594219fd06ba81677b18ded34770df2/index.js#L21) | Function responsible for generating a message representing a WebpackStats instance | function | ![Example  output](images/stats.png) |
| [printError](https://github.com/moxystudio/webpack-sane-compiler-reporter/blob/bf70f5cfd594219fd06ba81677b18ded34770df2/index.js#L22) | Function responsible for generating a message of a Error instance | function | ![Example output](images/error.png) |


### API

As shown in the [usage](#usage) section above, the result of adding reporting on a compiler is a function that, when invoked, stops listening to the compiler events, hence halting any further output.

### Other exports

For convenience this package also exports the [renderers](lib/renderers.js) used internally:

```js
const reporter = require('webpack-sane-compiler-reporter');

reporter(compiler, {
    printSuccess: (stats) => reporter.renderers.renderSuccess(stats),
});
```


## Tests

`$ npm test`   
`$ npm test -- --watch` during development


## License

[MIT License](http://opensource.org/licenses/MIT)
