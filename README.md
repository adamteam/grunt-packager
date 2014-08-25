# grunt-adam-packager

> Grunt task for Adam Packager projects.

## Getting Started
This plugin requires Grunt `~0.4.2`

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:

```shell
npm install grunt-adam-packager --save-dev
```

Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-adam-packager');
```

## The "packager" task

### Overview
In your project's Gruntfile, add a section named `packager` to the data object passed into `grunt.initConfig()`.

```js
grunt.initConfig({
  packager: {
    options: {
      name: 'Core' // Package name. (todo: use package.json)
    },
    your_target: {
      // Target-specific file lists and/or options go here.
      'adam-all.js': 'src/**.js'
    },
  },
});
```

### Options

#### options.wrap
Type: `Array`
Default value: `[]`

An array containing the package prefix and suffix information.

#### options.strip
Type: `String` or `Array<String|RegExp>`
Default value: `false`

A single, or multiple, strings or regexp to remove from the combined code.

#### options.separator
Type: `String`
Default value: `grunt.util.linefeed`

The delimeter to join all the source files together.

#### options.name
Type: `String` or `Object`

The package name. TODO: Use package.json.

The name of the package, or, if there are multiple packages being built, an
object with the names and paths to their source files.

```js
grunt.initConfig({
  packager: {
    options: {
      name: {
        Core: 'adam'
      }
    },
    all: {
      'dest/adam.js': 'src/**.js',
    },
  },
});
```


#### options.ignoreYAMLheader
Type: `Booelan`
Default value: `false`

Ignores the YAML headers for dependency loading.

#### options.only
Type: `String` or `Array`

The specific components or packages to compile (with their dependencies).

NOTE: You can specify the `.only` value in the `.options` and it will apply to all
configurations globally, but you can also specify an `.only` value for each configuration.
This allows you to build numerous libraries with specific requirements.

```js
grunt.initConfig({
  packager: {
    options: {
      name: {
        base: 'adam',
        mobile: 'mobile'
      }
    },
    // all of both libraries
    all: {
      src: [
        'adam/src/**/*.js',
        'adam-mobile/src/**/*.js'
      ],
      dest: 'adam.js'
    },
    // the Form.Validator component and its requirements
    Polyfill: {
      src: [
        'adam/src/**/*.js',
        'adam-mobile/src/**/*.js'
      ],
      only: [
        'base/Promise'
      ]
      dest: 'promise.js'
    },
    // all of the Mobile package and its requirements
    allOfMobile: {
      src: [
        'adam/src/**/*.js',
        'adam-mobile/src/**/*.js'
      ],
      only: [
        'mobile/*'
      ]
      dest: 'mobile.js'
    }
  },
});
```

### Other Usage Examples

#### Default Options
```js
grunt.initConfig({
  packager: {
    options: {
      name: 'Core'
    },
    all: {
      'dest/adam.js': 'src/**.js',
    },
  },
});
```

#### Strip Options
```js
grunt.initConfig({
  packager: {
    options: {
      name: 'Core',
      strip: '.*compat'
    },
    all: {
      'dest/adam.js': 'src/**.js',
    },
  },
});
```
