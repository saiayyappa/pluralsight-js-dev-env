# For a JS Starter kit following decisions have to be considered

Editors and Configurations
Package Management
Development Webserver
Automation
Transpiling
Bundling
Linting
HTTP
Testing and CI
Project Structure
Production Build
Automated Deployment

For Integration: Git
For Deployment : Heroku

Editor: What to look for
- Strong ES2015+ Support
- AutoCompletion
- Parse ES6 imports
- Report unused imports
- Automated refactoring
- Framework Intelligence
- Built-in terminal
- Recommended -- Atom, WebStorm, Brackets, VSCode

Package Managers
- bower(irrelavant), npm(most recommended), jspm(also a bundler), jam, volo
- https://gist.github.com/coryhouse/29bd1029b623beb4c7f79b748dcba844
- package security -- retire.js, Node Security Platform
- npm now has security scanning built-in

Development Web Servers
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

Automation
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

