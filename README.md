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
grunt watch
```

In a new terminal tab/pane/window from your project's root, do:

```shell
node server/app
```

Go to [http://localhost:3000](http://localhost:3000). You'll probably also want to change the
names `myApp` and `ngBoilerplate` to your own app's name throughout at some point.

##Structure

The project is set up with two completely independent directories - `/client` and `/server`. They're
both already set up with individual `.gitignore` files, so that you can split these up into
two separate git repos if you prefer. If not, feel free to remove them and just use the one in the
project root.

In `/client`, `grunt-loopback-angular` and `grunt-docular` have been installed and a grunt task called
`loopback` registered in `Gruntfile.js`. The `loopback` task has been added to `default` so that besides
being available via `grunt loopback`, it will automatically run when you do `grunt`. An initial
`lb-services.js` file has been generated and injected as a dependency of the angular app.

In `/server` is a barebones Loopback API. There's nothing more here than whatever is normally generated
by `slc lb project myApp` except that `app.js` has been set up to serve the AngularJS app when `/` is
requested. By default, Loopback will look for the `index.html` file in `/client/build`, where your
Angular sources will be located in development, and automatically serve it to the client. To switch
to production mode, just comment out the two `// DEVELOPMENT` sections and uncomment the two
`// PRODUCTION` sections in `/server/app.js`:

```javascript
// The static file server should come after all other routes
// Every request that goes through the static middleware hits
// the file system to check if a file exists.

// PRODUCTION
// app.use(loopback.static(path.join(__dirname, '..', 'client', 'bin')));

// DEVELOPMENT
app.use(loopback.static(path.join(__dirname, '..', 'client', 'build')));

// Requests that don't match any of the above should be sent to
// index, where we'll handle them using HTML5 history (Angular client)

// PRODUCTION
// app.use(function(req, res) {
//   res.sendfile(path.join(__dirname, '..', 'client', 'bin', 'index.html'));
// });

// DEVELOPMENT
app.use(function(req, res) {
  res.sendfile(path.join(__dirname, '..', 'client', 'build', 'index.html'));
});
```

##Usage

To work on the whole application, you'll need two terminal or tmux windows/tabs/panes - one for the
client and one for the server. In the client tab, just run `grunt watch` and your sources will be
built and tests run. In the server tab, just run `node server/app` and Loopback will serve the sources
from the `/client/build` directory. In this way, you can have the Loopback API and client-side grunt
tasks running simultaneously.

If you want to work on the client-side app only, you can do so just as you normally would with
`ng-boilerplate` - run `grunt watch` and open `file:///path/to/client/build/index.html` in your browser.

When you're ready to deploy, you can do `grunt compile` and `node ../server/app`, do a quick
once-over, and push according to your deployment or CI process. All you need to push to production is `/server`
and `/client/bin`.

For information specific to [Loopback](http://loopback.io) or
[ng-boilerplate](https://joshdmiller.github.io/ng-boilerplate), see their respective documentation.
A lot of great documentation is included in various README files throughout the `/client` if you're
not familiar with ng-boilerplate.
