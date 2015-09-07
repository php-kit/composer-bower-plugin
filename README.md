
## Composer plugin for installing Bower packages

This Composer plugin allows you to declare, manage and install front-end packages from the Bower repository on your project using Composer.

This is a pure PHP solution. **There's no need to install neither Bower nor Node.js on your computer.**

Besides managing your main application's front-end packages, **it also supports package dependencies**, i.e. other installed composer 
packages may define their own bower dependencies.

This plugin will merge all dependencies in memory, while running. No configuration files on disk will be modified.

> **Note:** this Readme has information that only applies to the final version of the plugin, which is **not yet available**.  
Currently, the plugin **still uses the Bower executable** for installing packages.  
Some of the information on this document may still not apply.  
This notice will be removed as soon as the final version is completed.  
We're sorry for the inconvenience.

### Configuring

Dependencies are specified by an extra configuration section on your project's `composer.json` or on any 
packages' own `composer.json`.

> `bower.json` files are neither required nor supported. This is by design. All configuration information comes from `composer.json`.

#### Example

###### root composer.json

```json
"require": {
  "impactwave/composer-bower-plugin": "dev-master"
},
"extra": {
  "bower": {
    "require": {
      "bootstrap": "~3.3.5"
    },
    "require-dev": {
      "jasmine": "~2.3.4"
    },
    "directory": "vendor/bower_components",
    "scripts": {
      "post-update-cmd": "Namespace\\Class::method or command --with args"
    }
  }
}
```

#### Target installation directory

The dependencies will be installed on `vendor/bower_components` by default.
You can customize that location via the `extra.bower.directory` setting.

> `extra.bower.directory` is valid only on the main `composer.json`.

> `.bowerrc` files are not supported.

### Running

The plugin updates bower dependencies whenever one or more packages are installed or removed.

You may then copy the relevant source code files from the installation directory to a public web directory, using your favorite build tool.

To automate that process, `composer-bower-plugin` exposes a hook for running your build script.

On `composer.json`, you can specify an `extra.bower.scripts.post-update-cmd` key, indicating a class and method name to be invoked or, alternatively,
the name and arguments of a command-line executable script/program.

> `post-update-cmd` will run for both *install* and *update* events.

> Script hooks will only run first for the main `composer.json`.  
Packages cannot specify their own scripts.

## License

This library is open-source software licensed under the [MIT license](http://opensource.org/licenses/MIT).

Copyright &copy; 2015 Impactwave, Lda.

Some parts of the source code originated from the [composer-extra-assets plugin](https://github.com/koala-framework/composer-extra-assets) and have been extensively modified.
