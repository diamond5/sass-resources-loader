# sass-resources-loader

This loader will `@import` your SASS resources into every `require`d SASS module. So you can use your shared variables & mixins across all SASS styles without manually importing them in each file. Made to work with CSS Modules!

## Installation

Get it via npm:

```bash
npm install sass-resources-loader
```

## Usage

Create your file (or files) with resources:

```scss
/* resources.scss */

$section-width: 700px;

@mixin section-mixin {
  margin: 0 auto;
  width: $section-width;
}
```

**NB!** Do not include anything that will be actually rendered in CSS, because it will be added to every imported SASS file.

Provide path to the file and apply loader in webpack config:

```js
/* webpack.config.js */

module: {
  loaders: [
    // Apply loader
    { test: /\.scss$/, loader: 'style!css!sass!sass-resources' },
  ],
},

// Provide path to the file with resources
sassResources: './path/to/resources.scss',

// Or array of paths
sassResources: [ './path/to/vars.scss', './path/to/mixins.scss' ]
```

Now you can use these resources without manually importing them:

```scss
/* component.scss */

.section {
  @include section-mixin; // <--- `section-mixin` is defined here
}
```

```js
import React from 'react';
import css from './component.scss';

// ...

render() {
  return (
    <div className={css.section} />
  );
}
```