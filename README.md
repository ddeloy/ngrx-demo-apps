
## Introduction

This is a proof of concept that demonstrates the ability to share a Typescript package with core functionalities and business logic between an Angular2 web app and a Ionic2 mobile app.

Please check the Medium article [Hybrid mobile apps: sharing logic between Angular2 and Ionic2 apps](https://medium.com/@benorama/hybrid-mobile-apps-sharing-logic-between-angular2-and-ionic2-apps-7c32145b90d5#.m1x3vpyc0) for more info.

**Goals:**

* encapsulate all the business logic in a core module, based on [@ngrx/store](https://github.com/ngrx/store)
* keep specific view layout, markup and navigation logic in the app projects.

Note: [@ngrx/store](https://github.com/ngrx/store) is a RxJS powered state management inspired by Redux for Angular 2 apps. 
It's currently the most popular way to structure complex business logic in Angular2 apps.


## Running the apps locally

```
# Clone the repo
git clone https://github.com/benorama/ngrx-demo-apps.git
```

Prerequisites:
* [Typescript 2.0+](https://www.typescriptlang.org/index.html#download-links)
* [Angular CLI](https://cli.angular.io)
* [Ionic CLI](http://ionicframework.com/docs/cli/)

Note: `ngrx-demo-core` module is shared between the apps with `npm link` but it could be published to `npmjs` and be used as a regular dependency.

### ngrx-demo-core module

First, compile `ngrx-demo-core` shared module. 

It is based on official Ionic module template, which supports Angular's ngc and Ahead-of-Time compiling out of the box.
https://github.com/driftyco/ionic-module-template

```
# Go into core module directory
cd ngrx-demo-apps/core

# Install dependencies (you can get a coffee...)
npm install

# Compile typescript into dist
npm run build

# npm link
# npm link does not work... so we use pack (temporarly)
npm pack
# Or npm publish

# Note: during dev, you can use 'tsc -w'
```

The shared module is now installed locally and can be used in other local npm projects.

### ngrx-demo-web app

Install or link `ngrx-demo-core` shared module and run the web app.

```
# Go into web Angular2 app directory
cd ../web

# Install dependencies (you can get a burger...)
npm install

# Create a symlink from the local node_modules folder to the global shared module symlink
# npm link ngrx-demo-core
# npm link does not work... so we use pack/install (temporarly)
npm install ../core/ngrx-demo-core-0.0.1.tgz 

# Run the web app locally
ng serve
```

### ngrx-demo-mobile app

As we did for the web app, install or link the `ngrx-demo-core` shared module and run the mobile app.

```
# Go into mobile Ionic2 app directory
cd ../mobile

# Install dependencies and typings (you can get a burger...)
npm install

# Create a symlink from the local node_modules folder to the global shared module symlink
# npm link ngrx-demo-core
# npm link does not work... so we use pack/install (temporarly)
npm install ../core/ngrx-demo-core-0.0.1.tgz 

# Run the mobile app locally
ionic serve
```

Note: for more info on using external lib on Ionic2
* [Third Party libraries in Ionic Apps](http://ionicframework.com/docs/v2/resources/third-party-libs/)
* [App Scripts](http://ionicframework.com/docs/v2/resources/app-scripts/)

## Bugs and feedback

If you have any questions or suggestions to improve the demo app, don't hesitate to submit an issue or a pull request!