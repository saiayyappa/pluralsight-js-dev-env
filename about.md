# For a JS Starter kit following decisions have to be considered

Editors and Configurations : VSCode
Package Management : npm
Development Webserver : express
Automation : npm scripts
Transpiling : babel
Bundling : webpack
Linting
HTTP
Testing and CI
Project Structure
Production Build
Automated Deployment

For Integration: Git
For Deployment : Heroku

## Editor: What to look for
- Strong ES2015+ Support
- AutoCompletion
- Parse ES6 imports
- Report unused imports
- Automated refactoring
- Framework Intelligence
- Built-in terminal
- Recommended -- Atom, WebStorm, Brackets, VSCode

## Package Managers
- bower(irrelavant), npm(most recommended), jspm(also a bundler), jam, volo
- https://gist.github.com/coryhouse/29bd1029b623beb4c7f79b748dcba844
- package security -- retire.js, Node Security Platform
- npm now has security scanning built-in

## Development Web Servers
- http-server, live-server
    light weight, easily configurable, limited capabilities
- express
    comprehensive, highly configurable, production grade, can run it
    everywhere
    alternatives: koa, hapi
- budo
    integrates with browserify, hot reloading
- webpack
    fast, serves directly from memory
    avoids pulling another dependency
    it doesn't require generating physical files
- browsersync
    dedivated IP for sharing work on LAN
    all interactions remain same
    great for cross-device testing
    integrates with browserify, webpack, gulp
- all the ones mentioned above(except express) are only used for development
- sharing work-in progress using localtunnel, ngrock, now, surge
- browsersync & localtunnel are good combination since we can test in various
    devies simultaneously

## Automation
- grunt
    first js task-runner, config over code(grunt json file)
    file-oriented(writes intermediary files between steps)
- gulp
    in-memory streams(or pipes)
    you don't have to write to disk after each step in task
    instead you simply pipe the output of a previous step to
    next step through in-memory
    code over config
- npm scripts (most recommended)
    declared in scripts section of package.json file
    leverage OS command line
    directly use npm packages
    call separate node scripts
    convention-based pre/post hooks
    no need for separate plugins, use tools directly(avoid extra
    layer of abstraction)
    simple debugging, better docs
    https://www.freecodecamp.org/news/why-i-left-gulp-and-grunt-for-npm-scripts-3d6853dd22b8/#.atd15pnxx
- nsp is build into node by default so need of security-check script

## Transpiling
- Babel: modern, allows to use experimental feature in standards-based way
    transpiles to ES5, standardized JS, leverage full JS ecosystem
- TypeScript: superset of JS, enhanced autocompletion, safer refactoring
    type safety, can aid maintenance on large code bases by clarifying
    developer intent, additional non-standard features
- TS cannot be used with react which uses JSX which is not supported by 
    TS but babel can be used because code is following JS standards but
    TS adds enhancement to existing JS such as interfaces, thus new syntaxes
    of other template engine such JSX cannot be used.(but support was added later)
- no type defs, annotations required, ES6 imports are statically analyzable in Babel

## Bundling
- CommonJS doesn't work in web browsers. So all the require/import 
    statement do not work, hence we need to bundle all the dependencies.
- We need to bundle npm packages in a way that browser can consume.
- To package any JS into a single file or strategically into separate
    file, for different portions of the app.
- improve node performance
- types of modules: IIFE, AMD,UMD, CJS, ES6
    recommended: CJS, ES6(most because of its fail fast feature)
- Bundlers: Require.JS(not used), browserify, webpack(recommended), rollup, jspm