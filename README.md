atrule-bem
---
[![Travis](https://img.shields.io/travis/tbremer/postcss-atrule-bem-prefixer.svg?style=flat-square)](https://travis-ci.org/tbremer/postcss-atrule-bem)
[![npm](https://img.shields.io/npm/v/postcss-atrule-bem.svg?style=flat-square)](https://www.npmjs.com/package/postcss-atrule-bem)
[![npm](https://img.shields.io/npm/l/postcss-atrule-bem.svg?style=flat-square)](https://github.com/tbremer/postcss-atrule-bem/blob/master/LICENSE)

_Efficiently create BEM components._

## Input / Output
### Put in:
```css
@block btn {
  background-color: var(--primary);
  border: .0625rem solid var(--primary-constrast);
  color: var(--black);

  @element icon {
    color: var(--primary-contrast-high)
  }

  @modifier transparent {
    background-color: transparent;
    border-color: transparent
  }
}
```

### Get out:
```css
.btn {
    background-color: var(--primary);
    border: .0625rem solid var(--primary-constrast);
    color: var(--black)
}
.btn__icon {
    color: var(--primary-contrast-high)
}
.btn--transparent {
    background-color: transparent;
    border-color: transparent
}
```

## Options

#### `strict`

Type: `Boolean`

Default: `true`

**Disallows improperly formed components**
- Block's can only have: Elements and Modifiers.
- Elements can only have Modifiers.
- Modifiers cannot house any types.

_**Side Effect:** turning off `strict` turns off warnings_

#### `warn`

Type: `Boolean`

Default: `true`

**Turns on warnings for imporperly formed components**

#### `shortcuts`

Type: `Boolean`

Default: `false`

#### `separators`

Type: `Object`

Default: `{
    element: '__',
    modifier: '--'
  }`

## Usage

Add *atrule-bem* to your build tool:

```bash
npm install --save-dev postcss-atrule-bem-prefixer
```

#### Node

```js
import atRuleBem from 'postcss-atrule-bem-prefixer';

atRuleBem.process(/* your css */);
```

#### PostCSS

Add *PostCSS* to your build tool:

```bash
npm install postcss --save-dev
```

Load *atrule-bem* as a PostCSS plugin:

```js
import atRuleBem from 'postcss-atrule-bem-prefixer';

postcss([ atRuleBem() ])
.process(/* your css */, /* options */);
```

### Examples
```css
/* you can chain selectors with commas `,` */

/* input: */
@block foo {
  @element bar, baz {}
}

/* output: */
.foo {}
.foo__bar, .foo__baz {}
```

### Pull requests welcome.

Open for pull requests in the following areas:

- Collision detection
  - throw a warning and don't compile when:
    - a block is created twice (name collisions)
    - a block makes reference to another block

## Updating 3.0 for CommonJS users.
I added a babel plugin to correctly adapt the default export to the expected CommonJS type.

To upgrade change `const atRuleBem = require('postcss-atrule-bem-prefixer').default;` to `const atRuleBem = require('postcss-atrule-bem-prefixer');`
