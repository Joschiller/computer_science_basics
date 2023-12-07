# Java

- [Usage](#usage)
- [References](#references)
- [Overview](#overview)
- [Classes](#classes)
  - [Visibility](#visibility)
  - [Methods](#methods)
  - [Encapsulation](#encapsulation)
  - [Inheritance (`extends` keyword)](#inheritance-extends-keyword)
  - [this() and super()](#this-and-super)
  - [`abstract` Keyword](#abstract-keyword)
- [Collections](#collections)
  - [Arrays](#arrays)
  - [Lists](#lists)
  - [(Hash)Map](#hashmap)
  - [Set](#set)
- [Libraries](#libraries)

## Usage

- desktop development
- backend

## References

## Overview

Main function:

```java
public class classname {
  public static void main (String args[]) {
    //entry function for the program
  }
}
```

- each statement must end with ";"
- operators:
  - arithmetic: `+`, `-`, `*`, `/`, `%`, `++`, `--`, `+=`, `-=`, `/=`, `*=`, `%=`
  - pre and post increment differ!
  - comparision: <, >, >=, <=, ==, !=
  - boolean: ||, &&, !
- comments: `// ...`, `/* ... */`
- control structures:
  - if, else
  - ternary operator
  - switch, case, default break
  - for(init, condition, step)
  - while(condition)
  - do, white(condition)
  - break, continue

Console output:

```java
System.out.print("what to print"); // output without line break
System.out.println("what to print"); // output with line break
```

Conventions:

- **T**hisIsAClassName (= CamelCase)
- **t**hisIsAVariableName (= camelCase)
- interface**able**
- the names must represent their content!
- indexes start with 0!
- no keywords can be used as names (extend, implement, new, int, ...)

Variables:

- Definition of a variable: `[final] <data type> <variable name> = <value>;`
  - the value can be of any data type
  - an object can be instantiated there by using: `new <classname>([param])`
  - the final-keyword makes the variable a constant that cannot be changed
- data types

  | Data type | Usage                                                                                                                 | Size             | Default Value |
  | :-------- | :-------------------------------------------------------------------------------------------------------------------- | :--------------- | :------------ |
  | String    | Stores a text, surrounded by quotation marks (")<br/>`.toLowerCase(str)`<br/>`.toUpperCase(str)`<br/>`.charAt(index)` | 16 bit \* length | null          |
  | char      | single character, surrounded by single quotation marks (')                                                            | 16 bit           | `'\u0000'`    |
  | int       | integer number                                                                                                        | 32 bit           | 0             |
  | double    | point number represented by division (e.g. 4/2 = 2.0)                                                                 | 64 bit           | 0.0           |
  | float     | floating point number in scientific notation, marked with an "f"                                                      | 32 bit           | 0.0F          |
  | long      | larger integer number                                                                                                 | 64 bit           | 0             |
  | boolean   | true and false                                                                                                        |                  |               |
  | object    | any instance of a specific class                                                                                      |                  | null          |

Casting:

- change the datatype of a value implicitly → var2 needs to be a superclass to var1
  - `var1 = (datatype)var2;`
- otherwise the parse-methods can be used
  - `Double.parseDouble(value)`
  - `Integer.parseInt(value)`
  - `Boolean.parseBoolean(value)`

## Classes

- Attributes: `objectname.attributename` → represent the state of an object
- Methods: `objectname.methodname` → represent the behaviour of an object

Syntax:

```
<visibility> [static|abstract|final] class <classname> [extends <superclass>] implements <interface1>,...,<interfacen> {
  <attributes> //here the attributes are defined
  <classname>(parameter, ...) { <code> } //this is the constructor
  <methods> //here the methods get defined
}
```

### Visibility

- describes what can access a specific object/attribute/method/...

| Visible in... | only same class | package | class and subclasses | everywhere |
| :------------ | :-------------- | :------ | :------------------- | :--------- |
| private       | x               |         |                      |            |
| (default)     | x               | x       |                      |            |
| protected     | x               | x       | x                    |            |
| public        | x               | x       | x                    | x          |

### Methods

Syntax:

```
<visibility> [static|abstract|final] <return data type> <methodname> (parameter, ...) { <code> }
```

- each parameter: `[final] data type` + variable name e.g. int num
- return a value with the return keyword: e.g. `return value;`
- return type "void" = nothing will be returned
- The Constructor is a special method! -> gets called when a new instance of the class is created

Overload:

- define a specific method several times
- has to have different attributes to differ (return types and visibilities can also differ)

@Override:

- gets used for inheritance (methods or attributes)
- needs to call the super-method first: `super.methodname(... attributes ...);`
- new method cannot have a more limited visibility
- name, parameters and return type have to be the same as in the super-method

### Encapsulation

- controlling the access and manipulation of attributes
  - make attributes private
  - define public methods for reading/writing to the attributes → make it possible to control the output and input
  - this-keyword is used to mark the specific class attribute in a method, to make it differ from the parameters

### Inheritance (`extends` keyword)

- a specific class (subclass) can inherit properties from other classes (superclass) or interfaces
- polymorph: objects of subclasses can be handled with the data type of superclass

### this() and super()

- `this.variable` = calls specific attribute of the class
- `this(...)` = calls own constructor
- `super.variable` = calls specific attribute of the superclass
- `super(...)` = calls constructor of the superclass (needs to be done in inheriting classes!)

### `abstract` Keyword

- abstract classes
  - uses keyword "abstract" before class-name in definition
  - cannot be instantiated → subclasses need to implement the concrete class
- Abstract Methods
  - uses keyword "abstract" in front of the return value
- Interfaces (`interface Name { ... }`)
  - consist of only abstract methods
  - names normally: `...able { ... }`
  - classes can implement multiple interfaces → must implement all their methods
  - interfaces can extend each other (extend-keyword)

## Collections

### Arrays

- collection of data of the same type
- Instantiation:
  - `dataType[] name = new dataType[size];`
  - `dataType[] name = {value, value, ...};`
- `array.length` = attribute of the array representing the length
- access: `array[num]`, num must be a value from 0 to length-1
- methods: `.add(value), .get(num), .remove(value)`

### Lists

- does not support random access → every element needs to be processed to find one
- simple addition of new elements possible
- methods: `.add(value), .size(), .getFirst(), .removeFirst()`

### (Hash)Map

- Key-Value-pairs, does not need to have numeric key
- not sorted
- methods: `.put(key, value), .remove(key), .size(), .containsKey(key), .get(key)`

### Set

- contains unique elements

## Libraries

- include code by importing it e.g. `import java.lang.Math;`

```java
import java.lang.Math;
public class MyClass {
  public static void main (String args[]) {
	   System.out.println(Math.floor(2.5)); //round downwards 2
	   System.out.println(Math.ceil(2.5)); //round upwards 3
	   System.out.println(Math.pow(2,3)); //2 to the power of 3 = 8
	   System.out.println(Math.random()); //0.anything
  }
}
```
