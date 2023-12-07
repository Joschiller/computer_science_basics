# JavaScript

- [Usage](#usage)
- [References](#references)
- [Overview](#overview)
- [Output](#output)
- [HTML](#html)
- [ECMAScript6:](#ecmascript6)

## Usage

- web development
- scripting

## References

> https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript
>
> https://gist.github.com/gaearon/683e676101005de0add59e8bb345340c

## Overview

```js
var <name> = <value>;
```

- data types are inferred automatically
- operators:
  - arithmetic: `+`, `-`, `*`, `/`, `%`, `++`, `--`, `+=`, `-=`, `/=`, `*=`, `%=`
  - comparision: <, >, >=, <=, == (same value), === (identity), !=, !==
  - boolean: ||, &&, !
  - string concatenation with `+`
- comments: `// ...`, `/* ... */`
- control structures:
  - if, else
  - switch, case, default break
  - for(init, condition, step)
  - while(condition)
  - do, white(condition)
  - break, continue
- functions:
  - `function <name>(<param>) { ... }` -> `return`
- objects:
  ```js
  function name(param) {
    this.attr = value
    ...
  }
  ```
  - call with `new name(param)`
  - can also be created on demand without using a function
    ```js
    var name = { attr = value[, ...] }
    ```
- arrays

  ```js
  var arr = [
    /* elements */
  ];
  new Array(/* elements */);
  new Array(/* size */);

  // access
  arr[index];
  arr.length;
  arr1.concat(arr2); // creates new array

  // associative array
  arr["..."];
  ```

- helper: `Math` and `Date` object provide helper functions
  ```js
  // date
  .setInterval(function, millis), clearInterval() // calls a function after a certain amount of tile
  new Date() // now
  new Date(/* string */) // specific date
  .getFullYear()
  .getMonth()
  .getDate()
  ```

## Output

```js
document.write(...) // SHOULD NOT BE USED (https://developer.mozilla.org/en-US/docs/Web/API/Document/write?retiredLocale=de), writes to html document
console.log(...) // output to console
alert(...) // popup dialog
prompt(...[, ...]) // requests input
confirm(...) // request confirmation
```

## HTML

- selecting elements: `document.getElementById("...")`
  - attriutes can be changed
  - children of elements can be added or removed
- provides possibility to perform animations and add events

## ECMAScript6:

- let und const
- template strings: `...${...}...`
- `for(let variable in arr)`
- lambdas, forEach, filter, ...
- default parameters for functions
- simpler ways of creating functions within objects
- spread operator `...` for rest parameters
- classes (constructors, class methods)
- `Map`, `Set`
- iterators, generators
