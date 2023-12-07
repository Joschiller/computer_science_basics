# TypeScript

- [Usage](#usage)
- [References](#references)
- [Overview](#overview)
- [Types](#types)
  - [Narrowing](#narrowing)
  - [Properties](#properties)
  - [Functions](#functions)
  - [Arrays](#arrays)
  - [Classes](#classes)
  - [Type Manipulation](#type-manipulation)
    - [Generics](#generics)
    - [`keyof`, `typeof`](#keyof-typeof)
    - [Indexed Access Types](#indexed-access-types)
    - [Conditional Types](#conditional-types)
    - [Mapped Types](#mapped-types)
    - [Template Literal Types](#template-literal-types)
- [Modules](#modules)

## Usage

- web development
- scripting
- based on [JavaScript](./JavaScript.md)
  - adds type informations
  - checks for existance of properties instead of returning undefined
  - prevents errors
  - <span style="color:red"><b>only applied at compile time</b></span> (TypeScript Compiler (tsc) compiles back to JavaScript)
  - compiler options:
    - `--noEmitOnError`: does not compile if any error occurs
    - `--noImplicitAny`: if compiler infers data type to any this has to be declared explicitly
    - `--strictNullChecks`: every possible occurrence of null|undefined must be handled manually
    - `--strictPropertyInitialization`: all class fields must be initialized directly in the constructor

## References

> https://www.typescriptlang.org/docs/handbook/intro.html

## Overview

```ts
{let|var|const} name[: type][= value] // `?` in type states optional type (e.g. for parameters or properties)
```

- data types
  - primitives: string, number, bigint, boolean, null, undefined, symbol
  - `typeof variable` returns the string representation of the primitive type
  - `any` can hold every data type
  - Arrays:
    - `type[]`
    - declaration: `[x, y, z, ...]`
  - booleans
    - falsy: 0, NaN, `""` empty string, `0n` bigint zero, null, undefined
    - truthy: anything else
- operators, comments, control structures, functions: see [JavaScript](./JavaScript.md)

## Types

```ts
this; // current object, mostly inferred by TypeScript
void; // empty return type => void functions can return values but those are ignored
object; // most general type (!= Object => always use object)
unknown; // any value, but without any direct options => MUST be narrowed down
any; // any value
never; // should never be observed (e.g. return type of error methods or when no type of a union is left in a switch)
Function; // all function types => bind, call, apply
```

Types are associated according to their structure (combination of property names and types)

```ts
// type syntax
type name = { /* list of properties */ }
type name = type1 | type2 | ... // union type, can contain all subtypes, supports all identical properties => divide using narrowing
(<value> as <type>) // type assertion, can be nested
// interface syntax
interface name { /* list of properties */ }

// extending a type
type B = A  & { ... }
// extending an interface
interface A { ... }
interface A { ... } // now A contains more properties
interface C extends A, B { ... }

// intersections
type C = A & B // A and B can be types/interfaces, C has all properites of A and B

// literal types (represents a single value as the value itself)
const variable = value as const
const variable: value = value
const variable = { /* properties for the type */ } as const // all properties of the type are literal types
const variable = value1 | value2 | ... // enum-like
```

### Narrowing

> - splitting or merging types using operators/functions
> - return statements can lead to narrowing e.g. in switch statements or if-else-branches (control flow analysis)

- `Array.isArray(value)`
- `typeof` type guards

  supports: string, number, bigint, boolean, symbol, undefined, object, function

  problem, if null is possible

  ```ts
  if (typeof value === "type name") {
    // distinct type available here
  }
  ```

- thruthyness narrowing (see [Overview](#overview))

  null is treated as false, problem: empty string is also false

  ```ts
  if (value) {
    // value is truthy here
  }
  ```

- `in` operator narrowing

  checks, if a property is contained in a value

  ```ts
  if (property in value) {
    // properties is accessible on value here (a subset of the union type is available here)
  }
  ```

- `instanceof` narrowing

  checks prototype chain of the type for the checked type

  ```ts
  if (value instanceof Type) {
    // distinct type available here
  }
  ```

- assignments

  type of a variable is narrowed according to the assignment on declaration (any, if not initialized); each assignment can update the type to a subset of the original type but NOT to a completely different type

- type predicates

  check if a variable is of a specific type using the access to a property on this type

  ```ts
  function isType(variable: unionType): variable is type {
    return (variable as Type).property !== undefined;
  }
  ```

- discriminated unions

  use an additional property to determine the type using a literal type value

  ```ts
  interface A {
    kind: "A";
    prop1: number;
  }
  interface B {
    kind: "B";
    prop2: string;
  }
  type General = A | B; // type can be identified using the "kind" property in a switch statement
  ```

- exhaustiveness checking

  using a switch statements default to return a never-type the switch statement is forced to be extended if a new subtype is added to a union type

  the never-type can be returned (like null) as content of every data type, but does not support any properties

  ```ts
  switch(variable.kind) {
    case "A": return ...;
    case "B": return ...;
    default: return variable; // returns never
  }
  ```

### Properties

```ts
name?: type // optional property => actual type: type|undefined
readonly name: type // readonly property (internal contents of the property can still be changed; readonly can be removed via alias or mapping modifiers in parameter lists)

[index: type]: type // index signatures => only string and number are possible for the index itself
```

- named parameters: `{ <names [with defaults]> }: <type>` => assigns properties of the type to new names
- object destruction: `{ oldName: newName [= default], ... }` => assigns new names in the parameter list

### Functions

```ts
// named function
function name(parameters): return_type { ... }
type name = (parameters) => return_type
type name = {
  properties ...,
  (parameters): return_type
}

// constructors
type nameConstructor = {
  new (parameter): return_type
}

// optional parameters
function f(param = ...) { ... } // directly infers the type by the default value, default is used instead of null|undefined

// "this" in functions (NOT for arrow functions)
paramName: (this: Type) // now "this" refers to the parameter

// rest parameters
...paramName: Type
/*
- must be last in parameter list
- implicitly always array
- to pass in an array, content must be constant: [ ... ]  as const
*/

// named parameters (descructing pattern)
{ parameterNames }: { parameterTypes } // or simply use a fitting type here
```

Overloading:

- each function signature ends with “;”
- the last function signature (implementation signature) must contain the maximum possible count of parameters and has to decide accordingly based on the provided input
  - the type of the first parameter will be a combination of all possible first parameters and so on (otherwise a specific overload cannot match the implementation)
  - narrowing to declare the correct behavior
- the implementation signature cannot be called, only the overload signatures
  ```ts
  // several function signatures
  // implementation signature { body }
  ```
- rules
  - the implementation signature is not visible from outside, there should be at least two overload signatures in front of the implementation signature
  - if all overloads have the same parameter count and return type, an overload is not needed => use union type as parameter/return instead
  - do not use optional parameters in a callback method (except it is intended to be called with fewer arguments)

### Arrays

```ts
// array
const array: Array<Type> = new Array(...)
const array: Type[] = [ ... ]

// readonly array
const array: ReadonlyArray<Type> = new ReadonlyArray(...)
const array: readonly Type[] = [ ... ]

// tuple type
type name = [type0, type1, ...] // each element of an instance is accessible via the index and has to be of the specific type at this index
const [variable0, variable1] = tuple // destructs tuple into single elements
type name = [[type0, type1, ..., typeN-1?];
/*
- length property is a literal type consisting of all possible lengths according to optional parameters
- can have rest elements (...Type[]) which must be an array/tuple and can sit at any position in the tuple
=> has no set length
- can be readonly by adding the keyword in front of the brackets
*/
```

> Mostly taking readonly parameters for a function is better (in case the data does not need to be modified) because then the function can handle mutable and readonly arrays/tuples.

### Classes

```
class <name> [extends <base>] [implements <interfaces>] {
  <index signatures>
  <fields>
  constructor(<parameters>) {
    [super(...);]
    // initialization
  }
  <methods>
  <getter/setter>
}

Fields: [readonly] <name>: <type> OR <name> = <init>
- readonly fields can only be set from the constructor
Constructor:
- default constructor without parameters exists
- function with parameters (can have type annotations, defaults and overloads)
- no type parameters (generics) and return type
- super must be called before the first "this" usage
Methods:
- "this" refers to the class instance
- can override super-methods by simply redeclaring them (with additional optional parameters)
- call super methods using super.<method>(...)
- can be abstract (no implementation) => class must be abstract too
Getter: get <fieldName>() { return this.<fieldName>; }
Setter: set <fieldName>(value) { this.<fieldName> = value; }
=> getter and setter must have the same visibility

For every member: [public|protected|private] [static] <member>
```

- inheritance can cause problems in the prototype chain (https://www.typescriptlang.org/docs/handbook/2/classes.html#inheriting-built-in-types)
- classes can be subclasses of others even when there is no explicit “extends” keyword, because they may share the same properties
- Visibilities: public, protected (like in C# more restrictive), private (allows cross instance private access) => private is lost when converting to JS (except it is a JS private field with a name starting with “#” => considered hard private)
- Static:
  - function members cannot be declared again as static: name, length, call, ...
  - Classes cannot be static
  - Static blocks can be declared within classes => static { ... }

Parameter properties: constructor can directly create properties by adding those to the parameter list

```
class <name> {
  constructor(
    [public|protected|private][readonly] <name>: <type>,
    ...
  ) { }
}
```

```
const <variable> = class<generic_type> { ... }
```

Class expressions: create class and assign it to alias

This at runtime: accessing function-methods outside the class can cause a loss of the this-scope

- Solutions:
  - declare an arrow function member instead (uses more memory and loses connection to super method)
  - add this-parameter to function call expecting the instance itself => access via this (might still be used in the wrong way, but access to super is possible)
  - use parameter of type “this” => <variable>: this
    - only accepts other instances of the same type
    - can be used as return type (<method>(): this is <type>) as a typeguard

### Type Manipulation

#### Generics

> https://www.typescriptlang.org/docs/handbook/2/generics.html

Overloads can be avoided by using generics

```ts
function functionName<genericType>(...): returnType { ... }
const functionName = <genericType>(...): returnType => { ... }
```

Rules:

- when possible: use the type parameter itself instead of a constraint
- use as few type parameters as possible (maybe they are dependent on each other...)
- if a type parameter only occurs once in the declaration => is it needed? (should normally also occur as return type or in a similar way)

```ts
interface name<genericType> {
  propName: genericType,
  ...
}
type name<genericType> = {
  propName: genericType,
  ...
}
class name<genericType> { ... } // static members cannot use the generic class type (because they would belong to all different types at runtime)
```

Constraints:

```ts
genericType extends someOtherType
```

#### `keyof`, `typeof`

```ts
type variable = keyof Type; // keyof returns a union type of all properties of a type, if the type contains a string/number index signature this type is returned (string becomes string|number)
typeof someVariable;
typeof someFunction; // returns the type of a variable, only allowed on variables and properties
```

#### Indexed Access Types

```ts
variable["propertyName"];
```

- can be used to access properties of a variable or to get the type of a property by directly using the type as a variable
- https://www.typescriptlang.org/docs/handbook/2/indexed-access-types.html
- can only deal with types, not variables as an argument for the property name

#### Conditional Types

```ts
type variable = t1 extends t2 ? typeT : typeF;
```

- useful in combination with generics => https://www.typescriptlang.org/docs/handbook/2/conditional-types.html
- a function can return either of two types based on a generic type
- e.g. useful for generic infers:
  ```ts
  generic_type0 extends Array<infer generic_type1> ? generic_type1 : generic_type0
  ```
- in general it is distributive => so type0|type1 are handled one after each other => to avoid this use [t] brackets around the types in the conditional type => the union type is treated as a whole e.g. `A|B => A[]|B[]; [A|B] => (A|B)[]`

#### Mapped Types

```ts
type name<genericType> = {
  [Property in keyof genericType]: Type;
};
```

- iterates over the properties of the generic_type and creates properties with the same name but another type
- can add or remove readonly/? modifiers using +/-
  ```ts
  type name<genericType> = {
    [+/-readonly][Property in keyof genericType][+/-?]: Type
  };
  ```
- can also rename/remap properties to other names using the "as"-keyword => https://www.typescriptlang.org/docs/handbook/2/mapped-types.html
- can exclude specific properties using a conditional type

#### Template Literal Types

```ts
type name = `...${ ... }...`;
```

- string is composed based on the content between the brackets => type or union type or whatever
- can contain several of those templates => cross multiplication of the possibilities
- Intrinsic String Manipulation Types:
  - Uppercase<StringType>
  - Lowercase<StringType>
  - Capitalize<StringType>
  - Uncapitalize<StringType>

## Modules

default export:

```ts
export default ...

import someFile from "./fname.ts"
```

several exports:

```ts
export ...

import { ... } from "./fname.ts" // can also use aliases by: item as alias
import * from "./fname.ts"
// types should be imported with
import type { ... } from "./fname.ts"
import { type ... } from "./fname.ts"
```

> import without importing variables (import <file>) possible => may simply trigger some side effects that are necessary

CommonJS Syntax:

```ts
<code>
...

module.exports = {
  <properties like variables or function names>
}
```

- import via "require": `const <name> = require("<module_name>")`
- can also be accessed via destructing => directly assign several variables
