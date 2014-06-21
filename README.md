#loopback-ng-boilerplate

This project is an application skeleton for a typical __Loopback+AngularJS__ web app, which you can use
to quickly bootstrap your own projects. It brings together [Loopback](http://loopback.io) and
[ng-boilerplate](https://joshdmiller.github.io/ng-boilerplate).

##Quick Start

__Note:__ Hopefully, you have your environment set up such that you don't need sudo to do `npm` anything
but if not, just add sudo where appropriate.

```shell
mkdir myApp && cd myApp
git clone https://carlodicelico.github.com/loopback-ng-boilerplate .
cd server && npm install
cd ../client && npm install && bower install
grunt compile
node ../server/app
```

Go to [http://localhost:3000](http://localhost:3000). You'll probably also want to change the
names `myApp` and `ngBoilerplate` to your own app's name throughout.

##Structure

The project is set up with two completely independent directories - `/client` and `/server`. They're
both already set up with individual `.gitignore` files. This is so that you can split these up into
two separate git repos if you prefer.

In `/server` is a barebones loopback API. There's nothing more here than whatever is normally generated
by `slc lb project myApp` except that `app.js` has been set up to serve the AngularJS app when `/` is
requested. Loopback will look for the `index.html` file in `/client/bin`, where your compiled and
minified sources will be located in production, and automatically serve it to the client.

In `/client`, `grunt-loopback-angular` and `grunt-docular` have been installed and a grunt task called
`loopback` registered in `Gruntfile.js`. The `loopback` task has been added to `default` so that besides
being available via `grunt loopback`, it will automatically run when you do `grunt`. An initial
`lb-services.js` file has been generated and injected as a dependency of the angular app.

##Usage

If you want to work on the client-side app only, you can do so just as you
normally would with `ng-boilerplate` - run `grunt watch` and open `/client/src/index.html` in your
browser.

When you're ready to deploy, you can do `grunt compile` and `node ../server/app`, do a quick
once-over, and push according to your deployment process. All you need to push to production is `/server`
and `/client/bin`.

For information specific to [Loopback](http://loopback.io) or
[ng-boilerplate](https://joshdmiller.github.io/ng-boilerplate), see their respective documentation.
