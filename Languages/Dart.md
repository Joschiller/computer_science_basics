# Dart

- [Usage](#usage)
- [References](#references)
- [Overview](#overview)
- [Libraries](#libraries)
- [Collections/Iterables](#collectionsiterables)
- [Functions](#functions)
- [Classes/Objects](#classesobjects)
  - [Constructors](#constructors)
  - [Cascades](#cascades)
  - [Getters/Setters](#getterssetters)
- [Exceptions](#exceptions)
- [Futures, async, await](#futures-async-await)

## Usage

- mobile development with [Flutter](./Flutter.md)

## References

> see [DartQuickstart](./DartQuickstart.md#referenzen)
>
> https://dart.dev/tools/dart-format
>
> Deep-Dive and Examples:
>
> - https://dart.dev/language/concurrency
> - https://dart.dev/null-safety/understanding-null-safety
> - https://codelabs.developers.google.com/codelabs/dart-patterns-records#0
> - https://dart.dev/tutorials/server/cmdline
> - https://www.youtube.com/playlist?list=PLjxrf2q8roU0Net_g1NT5_vOO3s_FR02J

## Overview

- types can be inferred automatically
- operators:
  - assignment, if a value is null: `??=`
  - `x ?? y` is `y`, if `x` is `null`; `x` otherwise
- null safety via `?` to mark a type as nullable
  - access on nullable values via `?.`
  - nullable variables will be initialized with `null` if no other value is assigned on declaration
  - non-null can be asserted with `!`
  - after a null-check that leaves a function, the system can smart-cast to nun-nullable type
  - `late` keyword before uninitialized variable declaration allows access without null-check
- supports string interpolation in every kind of string (see https://dart.dev/language/built-in-types#strings)
- expects `;` after every line
- ternary operator exists

## Libraries

- certain core libraries provide important functionality (see https://dart.dev/overview#libraries)

## Collections/Iterables

```dart
final aListOfStrings = ['one', 'two', 'three'];
final aSetOfStrings = {'one', 'two', 'three'};
final aMapOfStringsToInts = {
  'one': 1,
  'two': 2,
  'three': 3,
};

// declarations for empty collections
final aListOfInts = <int>[];
final aSetOfInts = <int>{};
final aMapOfIntToDouble = <int, double>{};
```

- parent type for `List`/`Set`/`Map`: `Iterable<>` -> can be iterated using `for-in`-loop
  - `.elementAt(int index)`: access to elements
  - `.first`, `.last`
  - `.firstWhere(predicate, [orElse])`
  - `.singleWhere(predicate, [orElse])`
  - `.every(predicate)`, `.any(predicate)`
  - `.where(predicate)`, `.map(someFunction)`
  - `.takeWhile(predicate)`, `.skipWhile(predicate)`

## Functions

- functions can be passed in as arguments -> arrow function `(...) => ...`
- optional parameters -> must always be last in the argument list and can get a default value
  ```dart
  void function(int a, [int? b, int? c]) {
    // ...
    // b and c are `null` by default
  }
  void function(int a, [int b = 0, int c = 0]) {
    // ...
    // b and c are `0` by default
  }
  ```
- named parameters -> are optional by default unless they are marked as `required`
  ```dart
  void function(int a, {int? b}) {
    // ...
  }
  void function(int a, {int b = 0}) {
    // ...
  }
  // called with:
  // function(1)
  // function(1)
  // function(b: 2, 1) -> named parameters can be in any order
  ```

## Classes/Objects

### Constructors

- easy property initialization can be done by using a contructor of the following structure
  ```dart
  class SomeClass {
    int someProp;
    SomeClass(this.someProp); // called with SomeClass(1)
    // or SomeClass({required this.someProp}); called with SomeClass(someProp: 1)
    // required can then be omitted if the props are optional
    // can also use optional parameters with [this.someProp = 0] etc.
  }
  ```
- initializer lists -> are executed before the actual constructor body
  ```dart
  class SomeClass {
    SomeClass()
      : x = something, // initialize any values
        assert(...) // test any values
    {
      // ...
    }
  }
  ```
- to support several constructors in one class, use named constructors
  ```dart
  class SomeClass {
    SomeClass();
    SomeClass().alternateConstructor();
  }
  ```
- factory constructors
  ```dart
  class SomeClass {
    SomeClass();
    factory SomeClass.createFromSomethingElse(String someValue) {
      // ... return some new instance of SomeClass
    }
  }
  ```

- constructors can also redirect to other constructors using `the called constructor : the constructor to redirect to`
- `const` constructors can be used to create objects that never change -> all instance variables must be `final`

### Cascades

- perform several operations on the same object with: `someObject..someMethod()`
- this will return a reference to the same object so that the next cascade can be chained afterwards
- can also be used for non-null access with `?..`

### Getters/Setters

```
<type> get someProperty => _someProperty;
<type> get someProperty {
  return _someProperty;
  // ...
};

set someProperty(<type> value) => _someProperty = value;
set someProperty(<type> value) {
  // ...
}
```

## Exceptions

- any non-null object can be thrown using `throw`
- methods do not declare their thrown exceptions and it is not required to catch any exceptions

```dart
try {
  // ...
} catch (e) {
  // ...
} finally {
  // ...
}
```

## Futures, async, await

- to delay a command: `Future.delayed(const Duration(seconds: someInteger), someFunction)`
- futures must be called with `await` before the call
- functions calling a future must have the `async` keyword
- errors are caught using `try-catch` around the awaited future-call or using `.then(onSuccess, onError)` or `.catchError(onError, [(e) => e is TypeOfException])` (see also: https://dart.dev/guides/libraries/futures-error-handling#handling-specific-errors)
- optional ending statement: `.whenComplete(onComplete)` (works like finally)
- Stream = series of async events -> `await for ...` loop
  - errors can be catched with try-catch around the await-for-loop
  - helper methods for streams: e.g. `.lastWhere(predicate)`
  - further methods:
    - https://dart.dev/tutorials/language/streams#process-stream-methods
    - https://dart.dev/tutorials/language/streams#modify-stream-methods
    - most basic method: `listen()`
  - types of streams: single subscription OR broadcast
  - creating streams: https://dart.dev/articles/libraries/creating-streams
