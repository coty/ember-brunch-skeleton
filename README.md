# Application

## Quick Start

The following assumes you have installed [node](http://nodejs.org) 0.8.x and
[npm](http://npmjs.org/) 1.1.x. Type:

    npm install -g brunch

To install the project's tool dependencies, execute `npm install` in the project directory.

To build the project, execute `brunch build` in the project directory. The
results of the build are output to the `public` sub-directory. A production build
should append the command option `--minify`; use `brunch build --minify` to produce
a production deployment.

During development, to continuously rebuild the project on every change, execute `brunch watch`.
To run the simple http development server, execute `brunch watch --server`.

## Configure [git-flow](http://nvie.com/posts/a-successful-git-branching-model/) workflow support

    $ cd my-app
    $ git flow init

    Which branch should be used for bringing forth production releases?
      - master
    Branch name for production releases: [master]
    Branch name for "next release" development: [develop]

    How to name your supporting branch prefixes?
    Feature branches? [feature/]
    Release branches? [release/]
    Hotfix branches? [hotfix/]
    Support branches? [support/]
    Version tag prefix? []

## Architectural Guidelines

1. There is no such thing as architectural guidelines.
2. Controllers are responsible for interacting with model objects; a view should not directly interact with model objects.
3. Views are responsible for handling the DOM, not the controller. If the controller needs to walk the view hierarchy, you have sinned.
4. Views communicate with the controller, not directly with the model objects.
5. View template context is automatically bound to the controller’s content.
6. The router coordinates application state and transtitions between states. This is more comprehensive than routing URLs.

## Coding Guidelines

1. Verify your code using [JSHint](http://www.jshint.com/).
JSHint is available as a editor/IDE [plugin](http://www.jshint.com/platforms/).
2. Indent using soft tabs set at 2 spaces. Continuation indents should be set to 4 spaces.
3. Use the strict mode pragma liberally (i.e., `'use strict';`).
4. For the model, view, and controller, implement corresponding unit tests in the matching sub-directory of the `test` directory.
5. The unit tests follow uses the BDD expect assertion style. Unfortunately, the should assertion style is not compatible with IE.    

## Overview

    config.coffee
    package.json
    README.md
    /app/
      assets/
        index.html
        img/
          glyphicons-halflings-white.png
          glyphicons-halflings.png
      controllers/
        application_controller.js
        index.js
      models/
        index.js
      styles/
        application.styl
      templates/
        application.hbs
        index.js
      views/
        application_view.js
        index.js
      app.js
      initialize.js
      router.js
    /test/
      assets/
        test/
          index.html
      controllers/
      models/
      vendor/
        scripts/
          chai-1.3.0.js
          mocha-1.7.0.js
          sinon-1.5.0.js
          sinon-chai-2.1.2.js
        styles/
          mocha-1.7.0.css
      views/
      test-helpers.coffee
    /tools/
      testacular.conf.js
    /vendor/
      scripts/
        bootstrap-2.2.1.js
        console-helper.js
        ember-1.0.0-pre.2.js
        handlebars-1.0.rc.1.js
        jquery-1.8.2.js
      styles/
        bootstrap-2.2.1.css
    /public/
      img/
      stylesheets/
      javascripts/

* `config.coffee` contains your app configuration. This is where you configure what Plugins / Languages to use and what rules are applied to them.
* `app/` and subdirectories (excluding `app/assets`) contains files that are to be compiled. Javascript files are automatically wrapped as commonjs style modules so they can be loaded via `require('module/location')`.
* `app/assets` contains images / static files. The contents of the directory are copied to `public/` without any modification.
* `app/models/index.js`, `app/views/index.js`, and `app/controllers/index.js` are loaded in `initialize.js` and are responsible for loading their respective classes.
* `test/` contains unit tests.
* `vendor/` contains all third-party code. The code wouldn’t be wrapped in modules, it would be loaded directly into the browser.

The generated output is placed in the `public/` (by default) directory when `brunch build` or `brunch watch` is executed.

## Behavior and Logic

Application logic is built using JavaScript. The application is organized as a collection of modules following
the [CommonJS](http://www.commonjs.org) [Modules](http://www.commonjs.org/specs/modules/1.0/) specification.

[Ember.js](http://emberjs.com) Is a JavaScript Model View Controller (MVC) framework for single-page web application.
Ember uses the [Handlebars](http://handlebarsjs.com) client-side logic-less template for generating HTML mark-up
that updates automatically when the underlying data changes.

[jQuery](http://jquery.com) is used by Ember to simplify DOM interaction. The application uses jQuery primarily
for Ajax interactions with the remote resource servers.

## Layout and Styles

Application specific styles are written using the Stylus language and pre-processor. Twitter Bootstrap is used to
provide the application a default style for common elements. [Handlebars](http://handlebarsjs.com) wraps the HTML
layout and integrate with the logic programming in the Ember JS framework.

[Stylus](http://learnboost.github.com/stylus/) is an expressive language that generates CSS.
Stylus provides simplified selector expressions; variables and interpolation, operators, functions,
and mixins.

[Nib](https://github.com/visionmedia/nib) is a library of pre-built Stylus mixins, utilities, components,
and gradient image generation.

[Twitter Bootstrap](http://twitter.github.com/bootstrap/) Is a library of CSS styles and JavaScript UI components.
The CSS includes a number of element and class styles ranging from typography to grid layout support.

## Testing

Unit and integration tests are placed in the `test` directory. To run the tests interactively in the browser:

1. Execute `npm start` or `brunch watch --server` in your project directory.
2. Visit <localhost:3333/test> in your browser.

To run headless tests using brunch's built-in console-based test runner, execute `brunch test`. The
headless tests launch Mocha in [jsdom](https://github.com/tmpvar/jsdom) console environment.

### testacular server

    $ testacular start ./tools/testacular.conf.js --no-auto-watch --browsers Chrome,Firefox

### testacular run

    $ testacular run

## Resources

* [Mocha](http://visionmedia.github.com/mocha/) is a JavaScript test framework with excellent asynchronous testing support and versatile reporting.
* [Chai](http://chaijs.com) is a BDD / TDD assertion library support assert, expect, and should matchers.
* [Sinon](http://sinonjs.org) is test spy, stub, and mock library for JavaScript.
* [Sinon-Chai](https://github.com/domenic/sinon-chai) extends Chai with assertions for the Sinon.JS mocking library.
