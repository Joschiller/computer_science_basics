# C#

- [Usage](#usage)
- [References](#references)
- [Overview](#overview)
- [Classes and Objects](#classes-and-objects)
  - [Visibility](#visibility)
  - [Methods](#methods)
  - [Encapsulation](#encapsulation)
  - [Static Keyword](#static-keyword)
  - [Const and Readonly](#const-and-readonly)
  - [Indexers](#indexers)
  - [Operator Overloading](#operator-overloading)
  - [Inheritance](#inheritance)
- [Arrays](#arrays)
- [Collections](#collections)
  - [`List<T>`](#listt)
  - [`Dictionary<K, V>`](#dictionaryk-v)
  - [`SortedList<K, V>`](#sortedlistk-v)
  - [`BitArray`](#bitarray)
  - [`Stack<T>`](#stackt)
  - [`Queue<T>`](#queuet)
  - [`HashSet<T>`](#hashsett)
  - [Strings](#strings)
  - [Structs](#structs)
  - [Enums](#enums)
  - [Exceptions](#exceptions)
  - [Files `using System.io`](#files-using-systemio)
- [Events and Delegates](#events-and-delegates)
- [Threads `using System.Threading;`](#threads-using-systemthreading)

## Usage

- desktop development

## References

## Overview

Main function:

```cs
using namespacename; ...

namespace namespacename {
  class classname {
    static void Main(string[] args) { <code> }
  }
}
```

- each statement must end with ";"
- operators:
  - arithmetic: `+`, `-`, `*`, `/`, `%`, `++`, `--`, `+=`, `-=`, `/=`, `*=`, `%=`
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
  - foreach (datatype name in array)
  - break, continue
  ```cs
  //if
  if (<condition>) { <code> } else { <code> }
  //ternary operator
  <variable> = (<condition>) ? <value if true> : <value if false>;
  //switch
  switch(<variable>) {
      case <value>: <code> break;
      ...
      [default: <code> break;]
  }
  //while
  while (<condition>) { <code> }
  do { <code> } while (<condition>);
  //for
  for (<init>; <condition>; <step>) { <code> }
  foreach (<datatype> <name> in <array>) { <code> }
  ```
- processor directives: `#region regionname`, `#endregion`, ...
- output to console: `Console.WriteLine(string);`
- input from console: `Console.ReadLine();`

Variables:

- syntax: `<visibility> [static|const] <datatype|var> <name> = <value>;`
  ```cs
  // ways of declaration
  datatype name; name = value;
  datatype name = value;
  var name = value;
  datatype name1, name2, ...; // declares several variables at the same time
  ```
- casting: `var = (type)value`
- parsing: `var = SomeClass.parseMethod(value);`
  ```cs
  int c = Int16.Parse("5"); //c will have the value 5
  ```
- value can be a value-type or an object e.g. `new SomeClass(...)`
- const variables cannot be changed = constant
- data types:
  - atically analyzed if var-keyword used
  - numeric: int, float, double
  - bool
  - char, string
  - format strings with `{int}`-sequence → list of values to insert
- value types:
  - by value: stored in stack
  - by reference: pointer stored in stack, value stored in heap

## Classes and Objects

- Attributes: `objectname.attributename` → represent the state of an object
- Methods: `objectname.methodname(parameters)` → represent the behaviour of an object
- `this` = access to the class itself

```cs
class classname {
		//constructor → gets called at instantiation
		visibility classname(parameters) { <code> }
//destructor (only one per class, without parameters and specifiers!)
		~classname() { <code> }
		...
}
//e.g. generic class
class MyList<T> { <code> } //code must use the generic datatype T
```

### Visibility

| Visible in ... | only same class | package | class and subclasses | everywhere |
| :------------- | :-------------- | :------ | :------------------- | :--------- |
| private        | x               |         |                      |            |
| (default)      | x               | x       |                      |            |
| protected      | x               | x       | x                    |            |
| public         | x               | x       | x                    | x          |

- describes what can access a specific object/attribute/method/...
- further: internal, protected internal

### Methods

```cs
//definition
[static] <return type> <name>(<attributes> [= <default>]) { <code> }

//calling a method
<name>(<parameters>);
//or
<name>(<name of parameter>: <value>, ...);
```

- each parameter: data type + variable name
- return a value with the return keyword: e.g. `return <value>;`
- return type "void" = nothing will be returned
- for overloading: need to differ in list of parameters, can differ in return type
- Passing Arguments:
  - by value: pass only variable or value; don’t change the original
  - by reference: ref-keyword in method and method-call needed; changes the original
  - by output: out-keyword in method and method-call needed → method can write to this variable (so must be declared before!)
- Generic Methods:
  ```cs
  [static] <return type> <name><list of generics>(<attributes> [= <default>]) [where <generic condition>] { <code> }
  //e.g.
  static T twoTimes<T>(T x) { return x + x; }
  static void difTypes<T, U>(T a, U b) where T : class { <code> }
  ```

### Encapsulation

- controlling the access and manipulation of attributes
  - this-keyword is used to mark the specific class attribute in a method, to make it differ from the parameters

```cs
//encapsulation
private datatype variable;
public methodForAccess ...

//properties
private datatype variable;
public datatype Variable {
		get { return variable; }
		set { variable = value; }
}
//short version
public datatype Variable { get; set; }
//without extra variable declaration → only write the accessor, variable will be created automatically
```

### Static Keyword

Static Members:

- makes members belonging to a class itself, not to a object
  - const members are also static!
  - static constructors: are called automatically

Static Classes:

- are accessible without instantiating the class
  - can only contain static members
  - cannot be instantiated

e.g. Math-class

- Members: Pi, E
- Methods: Max(), Min(), Abs(), Sin(), Cos(), Pow(), Round(), Sqrt()

### Const and Readonly

|                  Const                  |                       Readonly                        |
| :-------------------------------------: | :---------------------------------------------------: |
|            cannot be changed            |                   cannot be changed                   |
| must be initialized while been declared | can be initialized after declaration (→ constructors) |
|            cannot be changed            |            can be changed by constructors             |
|     must be a compile time constant     |       can be assigned a value of a calculation        |

### Indexers

- allows objects to be indexed like an array
- `<visibility> <datatype> this[int index] { get { <code> } set { <code> } }`

### Operator Overloading

- allows to use a defined operator on this object
- `<visibility> static <datatype> operator<operator symbol>(<classname> a, <classname> b) { <code> }`

### Inheritance

```cs
//child class can access public and protected members of parent class
class Child : Parent { <code> }

//sealed classes cannot be inherited
sealed class Parent { }
class Child : Parent { } //Error
```

- parent constructor gets called before child constructor
- child destructor gets called before parent destructor
- child objects can be instantiated in variable of parents type

Polymorphism:

```cs
class Parent { public virtual datatype method() { } }
class Child : Parent { public override datatype method() { } }
```

- if parent and child have the same methods with different implementations: instantiate child object of type parent → call method → will call the appropriate overridden method of the child class but it is the type of the parent class

Abstract Classes:

```cs
abstract class Parent { public abstract datatype method(); }
class Child : Parent { public override datatype method() { } }
```

- if parent class has no meaningful task for a virtual method → abstract method (only declaration without body)
- abstract classes cannot be implemented → contain abstract methods/accessors
- derived class must override all abstract methods/accessors

Interfaces:

```cs
interface IParent { datatype method(); }
class Child : IParent { visibility datatype method() { } }
```

- is a completely abstract class → only contains abstract members (without abstract keyword)
- derived class must implement all interface methods (without override keyword)

## Arrays

- collection of data of the same type
- Properties: Length, Rank
- Methods: .Max(), .Min(), .Sum(), .reverse()

```cs
datatype[] name = new datatype[count];
datatype[] name = new datatype[count] { ... };
datatype[] name = new datatype[] { ... };
datatype[] name = { ... };

//multidimensional → each sub array has same number of elements
datatype[ , , ... , ] name = new datatype[size0, size1, ..., sizeN];
//e.g.
int[ , ] <name> = { { 1, 2 }, { 3, 4 }, { 5, 6 } }; //each same number of elements!

//jagged array → each sub array can have a different number of elements
datatype[][]... name = new datatype[count][];
//e.g.
int[][] name = new int[][] {
		new int[] {1,2,3},
		new int[] {4,5,6,7,8}
};
```

## Collections

- Generic Collections:, `List<T>, Dictionary<TKey, TValue>, SortedList<TKey, TValue>, Stack<T>, Queue<T>, Hashset<T>`
- Non-Generic Collections (store type object): `ArrayList, SortedList, Stack, Queue, Hashtable, BitArray`

### `List<T>`

- `List<<datatype>> <name> = new List<<datatype>>[ { <values> }|() ];`
- similar to array but elements inserted/removed dynamically
- every element must be processed to find one
- access: `Item[int index]`
- Properties: Count, Capacity
- Methods: .Add(T t), .RemoveAt(int index), .Sort(), .Clear(), .TrimExcess(), .AddRange(IEnumerable coll), .Insert(int i, T t), .InsertRange(int i, IEnumerable coll), .Remove(T t), .RemoveRange(int i, int count), .Contains(T t), .IndexOf(T t), .Reverse(), .ToArray(), .GetFirst()

### `Dictionary<K, V>`

- `Dictionary<<datatype>, <datatype>> <name> = new Dictionary<<datatype>, <datatype>>[ <key/value-pairs>|() ];`
- stores key/value-pairs, sorted by key, unique key
- access: `Item[K key]`
- Properties: Count, Keys, Values
- Methods: .Add(K key, V value), .Remove(K key), .Clear(), .ContainsKey(K key), .ContainsValue(V value)

### `SortedList<K, V>`

- stores key/value-pairs, sorted by key, unique key
- access: `Item[K key]`
- Properties: Count, Keys (→ collection), Values (→ collection)
- Methods: .Add(K key, V value), .Remove(K key), .Clear(), .ContainsKey(K key), .ContainsValue(V value), .IndexOfKey(K key), .IndexOfValue(V value)

### `BitArray`

- stores collection of bits (0/1)
- Properties: Count, IsReadOnly
- Methods: .Get(int i), .Set(int i, bool value), .SetAll(bool value), .And(BitArray ba), .Or(BitArray ba), .Xor(BitArray ba), .Not()

### `Stack<T>`

- LIFO (Last In First Out)
- Properties: Count
- Methods: .Peek() (→ topmost element), .Pop(), .Push(T t), .Clear(), .Contains(T t), .ToArray()

### `Queue<T>`

- FIFO (First In First Out) → adding = Enqueue, deleting = Dequeue
- Properties: Count
- Methods: .Dequeue(), .Enqueue(T t), .Clear(), .Contains(T t), .Peek(), .ToArray()

### `HashSet<T>`

- set of unique values
- allows fast lookup, addition and removal
- Properties: Count
- Methods: .Add(T t), .IsSubsetOf(ICollection c), .Remove(T t), .Clear(), .Contains(T t), .ToString(), .ISuperSetOf(ICollection c), .UnionWith(ICollection c), .IntersectWith(ICollection c), ExceptWith(ICollection c)

### Strings

- accessible like an array
- Properties: Length
- Methods:
  - `.IndexOf(char)` → int
  - `.Insert(index, string)` → string
  - `.Replace(string, string)` → string
  - `.Contains(string)` → bool
  - `.Remove(index)` → string (removed all chars after <index>)
  - `.Substring(index,[length])` → string (starts at <index>, if no length specifies it runs until the end)

### Structs

```cs
struct name {
		visibility datatype name;
		// ...
}
```

- simpler class → encapsulates groups of related variables (e.g. coordinates, ...)
- contain: methods, properties, indexers, …
- cannot contain default constructors → constructors must contain parameters!
- can be initialized without new-keyword

### Enums

```cs
enum name {
		name0[ = value],
		name1[ = value],
		// ...
		nameN[ = value]
}
```

- standard values: integer indexes starting with 0
- also only some values can be assigned → sets the following enumerators to following integers
- to assign enum value to an integer → cast the variable: `int x = (int)<enum>.<element>;`

### Exceptions

```cs
try { <code> } catch (Exception e) { <code> } finally { <code> }
```

- try gets executed
- catch gets executed if an exception gets raised in try
- finally gets executed after try-catch block
- Exception: e.g. use Exception.Message
- can also use more specific Exception types to catch

### Files `using System.io`

Methods:

- `File.WriteAllText(file, string)`
- .AppendAllText() → appends text to file
- .Create() → creates file in specified location
- .Delete() → deletes file
- .Exists() → determines whether file exists
- .Copy() → copes file to new location
- .Move() → moves file to new location

## Events and Delegates

Syntax:

```
[visibility] delegate [return type (mostly void)] <delegate name>([param]);
[visibility] event <delegate name> <event name>;
```

- does not need to create new delegate for each event
- can also use the given delegates

## Threads `using System.Threading;`

How to start a new Thread:

- create a class with the method that should be a thread
- create an instance of the Class, add an event and start the method in a thread
- wait until the Method finished
  Example for threads:

```cs
namespace ConsoleApplication1
{
	class Program
	{
		static void Main(string[] args)
		{
			ThreadClass th = new ThreadClass(1, 2);
			th.CalculatingDone += new ThreadClass.
				CalculatingFinished(th_CalculatingDone);
			new Thread(new ThreadStart
				(th.startCalculating)).Start();
		}
		static void th_CalculatingDone(int res)
		{
			Console.Out.WriteLine(res);
		}
	}
	class ThreadClass
	{
		public delegate void CalculatingFinished(int res);
		public event CalculatingFinished CalculatingDone;
		int a = 0;
		int b = 0;
		public ThreadClass(int a, int b) { this.a = a; this.b = b; }
		public void startCalculating() { CalculatingDone(a + b); }
	}
}
```

if the returned value needs to be assigned to any control of the main thread → some more code needed

```cs
//in the starting class
private delegate void th_CalculatingDoneCallback(int res);

// [...]

//in the event method
if (this.InvokeRequired)
{
	th_CalculatingDoneCallback callback = new
		th_CalculatingDoneCallback(th_CalculatingDone);
	this.Invoke(callback, new object[] { id });
}
else { <code> }
```

<!-- TODO: https://docs.google.com/document/d/1DbDSiF1HqlRk2CNvpGT1Haz7HHmUshS7nGdHZAkU05k/edit#heading=h.ssr2nwlzm2y0 -->
