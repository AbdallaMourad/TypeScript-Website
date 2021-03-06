---
display: "jsxImportSource"
oneline: "The module specifier for importing the jsx factory functions"
---

Declares the module specifier to be used for importing the `jsx` and `jsxs` factory functions when using [`jsx`](#jsx) as `"react-jsx"` or `"react-jsxdev"` which were introduced in TypeScript 4.1.

With [React 17](https://reactjs.org/blog/2020/09/22/introducing-the-new-jsx-transform.html) the library supports a new form of JSX transformation via a separate import.

For example with this code:

```tsx
import React from "react";

function App() {
  return <h1>Hello World</h1>;
}
```

Using this TSConfig:

```json tsconfig
{
  "compilerOptions": {
    "target": "esnext",
    "module": "commonjs",
    "jsx": "react-jsx"
  }
}
```

The emitted JavaScript from TypeScript is:

```tsx twoslash
// @showEmit
// @jsx: react-jsx
// @module: commonjs
// @target: esnext
import React from "react";

function App() {
  return <h1>Hello World</h1>;
}
```

With `"jsxImportSource": "preact"`:

```tsx twoslash
// @showEmit
// @jsxImportSource: preact
// @jsx: react-jsx
// @target: esnext
// @module: commonjs
// @noErrors

import React from "react";

function App() {
  return <h1>Hello World</h1>;
}
```

Alternatively, you can use a per-file pragma to set this option, for example:

```tsx
/** @jsxImportSource preact */

export function App() {
  return <h1>Hello World</h1>;
}
```

Would add `preact/jsx-runtime` as an import for the `_jsx` factory.

_Note:_ In order for this to work like you would expect, your `tsx` file must include an `export` or `import` so that it is considered a module.
