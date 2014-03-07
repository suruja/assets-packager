[![NPM version](https://badge.fury.io/js/assets-packager.png)](https://badge.fury.io/js/assets-packager)
[![Build Status](https://secure.travis-ci.org/GoalSmashers/assets-packager.png)](https://travis-ci.org/GoalSmashers/assets-packager)
[![Dependency Status](https://david-dm.org/GoalSmashers/assets-packager.png?theme=shields.io)](https://david-dm.org/GoalSmashers/assets-packager)
[![devDependency Status](https://david-dm.org/GoalSmashers/assets-packager/dev-status.png?theme=shields.io)](https://david-dm.org/GoalSmashers/assets-packager#info=devDependencies)

## What is assets-packager?

Assets-packager is a node.js-based tool for compiling, minifying, and packaging
CSS and JavaScript assets into production-ready packages.

CSS bundles are created from assets which are

* compiled from [LESS](https://github.com/less/less.js) templates (optional)
* minified using [clean-css](https://github.com/GoalSmashers/clean-css)
* bundled
* preprocessed via [enhance-css](https://github.com/GoalSmashers/enhance-css)
  (inline images, asset hosts, etc)
* packaged (and optionally precompressed)

And JavaScripts ones are

* bundled
* minified using the wonderful [UglifyJS](https://github.com/mishoo/UglifyJS)
* packaged (and optionally precompressed)


## Usage

### What are the requirements?

```
node.js 0.8.0+ on *nix (fully tested on OS X 10.6+ and CentOS) and Windows
```

### How to install assets-packager?

```
npm install -g assets-packager
```

### Tl;dr. Give me a quick demo!

OK. Here are commands to run

```bash
git clone git@github.com:GoalSmashers/assets-packager.git
cd assets-packager/examples
assetspkg -c assets.yml -g
```

Now check _examples/public/javascripts/bundled_ and _examples/public/stylesheets/bundled_ for bundled code.
That's it!

### Is it fast?

You should have just witnessed it by yourself. :-)

We use it on our production servers at [GoalSmashers.com](http://goalsmashers.com)
and it builds 20 CSS and 15 JavaScript bundles from hundreds of assets in around 15 seconds.

So yes, it is fast!

### How to use assets-packager in my application?

First of all it assumes you have Rails-like directory structure for your assets, e.g:

- public
    - javascripts
        - _some javascripts_
    - stylesheets
        - _some stylesheets_

Then it also needs a configuration file (here we name it **assets.yml**)
with a definition of JS/CSS bundles, e.g:

```yml
# stylesheets
stylesheets:
  application: 'reset,grid,base,application'
# javascripts
javascripts:
  application:
    - 'vendor/jquery'
    - 'application,helpers'
```

We recommend placing it somewhere else than in your _public_ folder (could be _config_ in case of Rails).

Now you can bundle all these packages with a single command:

```
assetspkg -c assets.yml
```

All the packages go into _public/javascripts/bundled_ and _public/stylesheets/bundled_.
You'll probably want to put that command somewhere into your build/deploy script.

### How to use assets-packager CLI?

Assets-packager accepts the following command line arguments:

```
assetspkg [options]

-h, --help                  Output usage information
-v, --version               Output the version number
-a, --assethosts [list]     assets host to use in CSS bundles (defaults to none)
-b, --cacheboosters         add MD5 hash to file names aka hard cache boosters (defaults to false)
--bj, --js-bundled [path]   path to JavaScript root directory (relative to --root option)
--bs, --styles-bundled [path]   path to stylesheets root directory (relative to --root option)
-c, --config [path]         path to file with bundles definition (defaults to ./config/assets.yml)
-g, --gzip                  gzip packaged files (defaults to false)
-i, --indent [value]        indentation level in spaces when used with --nm switch
-j, --concurrent [value]    number of concurrent tasks executed at once (defaults to number of logical CPUs)
-l, --line-break-at [value] number of characters per line in optimized JavaScript (defaults to off which means no line splitting)
-n, --noembedversion        create a version of packaged CSS without embedded images (defaults to false)
--nm, --nominifyjs          combine JS files without minification (defaults to false)
-o, --only [list]           package only given assets group (or groups if separated by comma)
--pj, --js-path [path]      path to JavaScript root directory (relative to --root option)
--ps, --styles-path [path]  path to stylesheets root directory (relative to --root option)
-r, --root [path]           root directory with assets directories (defaults to ./public)
```

### What are the assets-packager's dev commands?

First clone the source, then run:

* `npm run check` to check JS sources with [JSHint](https://github.com/jshint/jshint/)
* `npm test` for the test suite

### The feature I want is not there!

Open an issue. Or better: fork the project, add the feature
(don't forget about tests!) and send a pull request.


## Contributors

* Jean-Denis Vauguet [@chikamichi](https://github.com/chikamichi) - `--nominifyjs` and `--indent` options allow for combination-only processing.


## License

Assets-packager is released under the [MIT License](https://github.com/GoalSmashers/assets-packager/blob/master/LICENSE).
