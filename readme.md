# @rindo/sass

This package is used to easily precompile Sass files within Rindo components. Internally this plugin uses a pure JavaScript implementation of [Sass](https://www.npmjs.com/package/sass). Please see the
[Behavioral Differences from Ruby Sass](https://www.npmjs.com/package/sass#behavioral-differences-from-ruby-sass) doc if issues have surfaced since upgrading from previous versions which used used the `node-sass` implementation.

First, npm install within the project:

```
npm install @rindo/sass --save-dev
```

Next, within the project's rindo config, import the plugin and add it to the config's `plugins` property:

#### rindo.config.ts
```ts
import { Config } from '@rindo/core';
import { sass } from '@rindo/sass';

export const config: Config = {
  plugins: [
    sass()
  ]
};
```

During development, this plugin will kick-in for `.scss` or `.sass` style urls, and precompile them to CSS.


## Options

Sass options can be passed to the plugin within the rindo config, which are used directly by `sass`. Please reference [sass documentation](https://www.npmjs.com/package/sass) for all available options. Note that this plugin automatically adds the component's directory to the `includePaths` array.


### Inject Globals Sass Paths

The `injectGlobalPaths` config is an array of paths that automatically get added as `@import` declarations to all components. This can be useful to inject Sass variables, mixins and functions to override defaults of external collections. For example, apps can override default Sass variables of [Navify components](https://www.npmjs.com/package/@navify/core). Relative paths within `injectGlobalPaths` should be relative to the rindo config file.

```js
exports.config = {
  plugins: [
    sass({
      injectGlobalPaths: [
        'src/globals/variables.scss',
        'src/globals/mixins.scss'
      ]
    })
  ]
};
```

Note that each of these files are always added to each component, so in most cases they shouldn't contain CSS because it'll get duplicated in each component. Instead, `injectGlobalPaths` should only be used for Sass variables, mixins and functions, but does not contain any CSS.
