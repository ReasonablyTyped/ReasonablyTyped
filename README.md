<h1 align="center"><img src="https://github.com/rrdelaney/ReasonablyTyped/raw/master/docs/logo.png"></h1>

<pre align="center">
  $ npm install --global reasonably-typed
</pre>

<h4 align="center"><i>Converts TypeScript and Flow definitions to Reason interfaces</i></h4>

<hr>

<h3 align="center">Take your Flow or TypeScript definition</h3>

```js
// class.js
declare module 'classes' {
  declare type State = {
    id: number,
    storeName: string,
  }

  declare export class Store {
    constructor(initialState: State): Store;
    state: State;
    update(nextState: State): void;
  }
}
```

<h3 align="center">Run retyped</h3>

<pre align="center">
$ retyped class.js
</pre>

<h3 align="center">Get Reason</h3>

```reason
/* Module classes */

type state = Js.t {. id : float, storeName : string};

module Store = {
  type t = Js.t {. state : state, update : (state => unit) [@bs.meth]};
  external make : state => t = "Store" [@@bs.new] [@@bs.module "classes"];
};
```

## Docs

<p><details>
<summary><b><a href="https://rrdelaney.github.io/ReasonablyTyped">Examples</a></b></summary>
</details></p>

<p><details>
<summary><b>TypeScript</b></summary>

TypeScript has a similar workflow. Compile your TypeScript file with:

```
$ retyped my-definition.d.ts
```

</details></p>

<p><details>
<summary><b>Command-line Usage</b></summary>

```
Usage:
  $ retyped ...files

Examples:
  $ retyped file1.js file2.js file3.d.ts                                           [boolean]
```

</details></p>

<p><details>
<summary><b>Usage as a library</b></summary>
ReasonablyTyped also exports a library for use! See the example below:

```js
// lib-usage.js
import * as ReasonablyTyped from 'reasonably-typed'

const libSrc = fs.readFileSync('lib.js').toString()
const bsInterface = ReasonablyTyped.compile(libSrc)
```

**`format (code: string) => string`**

Formats a block of code using `refmt`

**`compile (code: string, filename?: string) => string`**

Compiles a libdef, formats the result, and handles errors cleanly

</details></p>

## Development

See [CONTRIBUTING](CONTRIBUTING.md).

## Status

[![CircleCI](https://circleci.com/gh/ReasonablyTyped/ReasonablyTyped.svg?style=svg)](https://circleci.com/gh/ReasonablyTyped/ReasonablyTyped)

## Roadmap

* [x] Basic types like `string`
* [x] Function types
* [x] Record types
* [ ] Literals as types
* [x] Union types
* [ ] Instersection types
* [x] Named types
* [x] Optional parameters
* [x] Classes
* [x] Generics
* [x] Built-ins like Promises
* [x] React components
