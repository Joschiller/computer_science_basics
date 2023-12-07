# Kotlin

- [Usage](#usage)
- [References](#references)
- [Overview](#overview)
  - [Basic Features](#basic-features)
  - [Arrays and Range](#arrays-and-range)
  - [Classes](#classes)

## Usage

- android development
- scripting

## References

## Overview

### Basic Features

```kt
<expr>!!.<expr> // not-null assertion

val <variable> = when {
<condition> -> <value>
...
else -> <value>
} // conditional assignment

// Functions:
fun <name>(<parameters>)[: return_type] { ... }
val f: (<parameter_types>) -> <return_type> = { ... }
```

### Arrays and Range

```kt
var <variable> = arrayOf(...) // array creation

for(<variable> in <array>) { ... } // foreach loop
// => possible values: array, string, range

// Range (of numbers or character):
for(<variable> in <start>..<end>) { ... }
if (<variable> in <start>..<end>) { ... }

// ForEach:
<array>.forEach(<lambda>)
<array>.map(<lambda>)
<array>.filter(<lambda>)
// can use "it" in lambda to refer to current item => shorter expression
```

### Classes

```kt
// Classes:
[open|abstract] class <name> {
<properties>
constructor(<constructor_parameters>) { ... }
}
[open|abstract] class <name>(<constructor_parameters>) { ... }
// variables: var <name> = <default>
// constructors: either in the class header to initialize all properties automatically or as additional method (several possible)

// default getter/setter => otherwise write custom ones for each property
get() = field
set(value) { field = value }

// inheritance
class <child>[<constructor>]: <parent>[<constructor>] { ... }
// superclass needs to be an "open" class (abstract classes are open by design (open not needed))

// visibilities: public (is default), protected, private
// overriding methods => override fun ...
```
