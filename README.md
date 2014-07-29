# grunt-zetzer

Grunt plugin for [Zetzer][zetzer]. More documentation in the
[Zetzer][zetzer] repository.

```shell
npm install grunt-stencil --save-dev
```

```js
grunt.loadNpmTasks('grunt-stencil');
```

### Usage Examples

*An elaborate list of examples can be found in [the Wiki](https://github.com/cambridge-healthcare/grunt-stencil/wiki/Examples).*

In your project's Gruntfile, add a section named `stencil` to the data object passed into `grunt.initConfig()`.

```js
grunt.initConfig({
  stencil: {
    options: {
      // Task-specific options go here.
    },
    your_target: {
      // Target-specific file lists and/or options go here.
    },
  },
})
```

[Grunt's rules for defining target and destination files](https://github.com/gruntjs/grunt/wiki/Configuring-tasks#files) apply, but care needs to be taken to make sure each input page maps to a single output file.

#### Custom Options

In this example, doT's it object is used to specify the location of script files and the main title of all pages; and the location of partials and templates is given. All pages in `pages/` will be compiled to `.html` files in `tmp`.

```js
grunt.initConfig({
  stencil: {
    main: {
      options: {
        env: {
          title: "Stencil",
        },
        partials: "content",
        templates: "templates"
      },
      files: [
        {
          expand: true,
          cwd: "src/pages/",
          src: "**/*.dot.html",
          dest: "tmp",
          ext: ".html",
          flatten: true
        }
      ]
    },
  }
})
```

## Contributing

In lieu of a formal styleguide, take care to maintain the existing coding style. Lint and test your code using [Grunt](http://gruntjs.com/). Please ignore W092 errors (wrapping regexps). The warning will show up until there's an option to disable it in jshint.

You can run the test suite with `grunt test` or `grunt testv` for more verbose output.

Each new feature ough to have full test coverage. We usually start by writing a fixture which is a pair of two file: the one to process (the fixture) and it's expected output.
Fixture are html or md files in `spec/fixtures`. Any partials and templates required by this fixture should be stored in `spec/partials` and `spec/templates`, respectively. The expected output of a fixture should be put in `spec/expected`.

Once we run tests and the fixture is failing, we can implement any necessary feature by starting with writing specs (unit tests) in the `spec` directory, (like `spec/my_new_feature_spec.js`) and then implementing it in `lib` directory (`lib/my_new_feature.js`).

Once all the unit tests pass, we can integrate new code back to the task with making the fixture test pass in mind :) .

If you take a look at any file in `lib/` you can notice that there's no dependencies between modules. All dependencies are injected in the task file `tasks/stencil.js`. That's the place where the integration happens.
