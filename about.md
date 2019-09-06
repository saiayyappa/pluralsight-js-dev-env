# For a JS Starter kit following decisions have to be considered

Editors and Configurations : VSCode
Package Management : npm
Development Webserver : express
Automation : npm scripts
Transpiling : babel
Bundling : webpack
Linting : ESLint
HTTP : fetch
Testing and CI : mocha, chai.js, JSDOM, travis, appveyor
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
- Dev can debug transpiled and bundled code using source maps of 
    transpiled version
- Source maps are downloaded only when developer tools is open because
    to save bandwidth

## Linting
- Catch error at compile time, enforces consistency, avoid mistakes
- JSLine, JSHint, ESLint(de facto)
- for configuring ESLint using package.json
```javascript
  {
    "name": "mypackage",
    "version": "0.0.1",
    "eslintConfig": {
      "plugins": ["example"],
      "env": {
        "example/custom": true
      }
    }
  }
  ```
- many plugins such as eslist-plugin-angular, eslint-plugin-node
- check this https://github.com/dustinspecker/awesome-eslint
- presents - from scratch, recommened by ESLint, airbnb, standard JS, XO
- use eslint-loader (to lint whenever we save) / use elsint-watch a
    node package for better warning and error formatting
- ESLint doesn't support most of the experimental features, for that
    use Babel-ESLint for using various Expermental features in Stages-X
- Linting via automated build process helps to check and universally
    configure, easy to peer program

## Automated Testing
- various tests: unit, integration, UI
### Testing Framework : Mocha
- mocha, jasmine, tape, Qunit, AVA, Jest
### Assertion Library : Chai
- chai, should.js, expect
### Helper Libraries : JSDOM
- JSDOM : simulate browser's DOM, run DOM-related tests
    without a browser
- Cheerio: jQuery for the server, query virtual DOM using
    jQuery selectors
### Where to run tests? : Node
- Browser -- Karma, Testem
- Headless Browser -- PhantomJS
- In-memory DOM -- JSDOM
### Where to place test files? : Alongside
- centralized to tests directory
- alongside to src files => easy imports, lower friction testing, 
    convenient to open, no recreating folder structure,
    clear visibility, easy to move files
### When to run test: When we hit save(for unit tests):
- rapid feedback 
- facilitates Test-driven development
- automatic = low friction
- increases test visibility
### Unit vs Integration
- test a small unit | test multiple units
- often single function | involves clicking and waiting
- fast | slow
- run upon save | run on demance since requires external resources
### Why CI?
- Forgot to commit new file
- Forgot to update package.json
- Commit doesn't run cross-platform
- node version conflicts
- bad merge
- didn't run tests 
- catch mistakes quickly
### Purpose of CI
- run automated build and check which commit has broke the build
- run tests
- check code coverage
- automate deployment
### CI
- travis(linux-based), appveyor(windows-based), jenkins, circleCI,
    Semaphore, snapCI

## HTTP Mock API
- Call approaches: http, request, XHR, jQuery, framework-based, 
    fetch, isomorphic-fetch, xhr, SuperAgent, Axios
- recommended: request(if you use only node),
    Fetch(if you need for support only in browser)
    SuperAgent, Axios(if app renders on both client and server)
- always centralize API
- Advantages of Mock API: unit testing, instant response, 
    keep working when services are down, rapid prototyping,
    avoid inter-team bottlenecks, work offline
    eg. Nock, static JSON, api-mock, JSON server, JSON schema faker
      browsersync, express
- with static JSON app loads same data everytime, so changing data
    doesn't reflect upon reload
- JSON server creates fake db and simulates real db and supports
    CRUD(overcomes disAdv of static JSON). Get a full fake REST API
    with zero coding in less than 30 seconds (seriously).
- JSON schema maker creates different fake data every time you start
    app. Its used along with JSON server. This allows to catch edge
    cases in design such as pagination, overflow, sorting and 
    formatting
- Express is more dynamic where we can set real db filled with mock
    data. But services have to be written to fetch data from db. If
    separate service is writing services its better to move on to
    JSON server. If service layer is already completed use Express.
### Mocking HTTP API
1. Declare schema
  - JSON schema faker
2. Generate Random Data
  - faker.js
  - change.js
  - regexp.js
3. Serve Data via API
  - JSON Server

## Project Structure: Demo App
- directory structure and file naming
- framework usuage
- testing
- mock api
- automated deployment
- codifies decisions
### Tips
- Put JS in .js file not in HTML script tag
- consider organizing by feature rather than by type
    of file (like in MVC)
- extract logic into POJO's

## Production Build
- Minification : for quick loading and save bandwidth
    removes comments, removes whitespace and new lines
    dead code elimination / tree-shaking, debug via sourcemap
- SourceMaps : support debugging
- Dynamic HTML : for production specific concerns
- Cache Busting : ensure client receive latest version of code upon 
    deployment
- Bundle Splitting : don't have to download entire app when just 
    part of it changes
- Error Logging : to log bugs in production