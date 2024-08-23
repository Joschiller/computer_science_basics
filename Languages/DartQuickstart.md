# Dart Quickstart (de)

> Wer sich mit TypeScript und Kotlin etwas auskennt, wird mit Dart sehr schnell gut vorankommen, da man viele Features hier wiederfindet und oben drauf noch einiges mehr, was einem das Leben erleichtert. Die Typisierung aus TypeScript kann man mit Dart gut nachbilden, ist aber sogar echt null-safe unterwegs. Zugleich hat man aber auch ein Klassensystem mit viel Erleichterungen in Bezug auf Vererbung, das viele Features aus Kotlin aufgreift und nochmal reichlich zusätzliche Vereinfachungen und Kurzschreibweisen mitbringt.
>
> Dieses Dokument beschreibt hauptsächlich die Sicht auf Dart im Vergleich zu TypeScript, um einen leichten Umstieg auf Dart zu ermöglichen, wenn man bereits gute Vorkenntnisse in TypeScript hat.

## Referenzen

Unbedingt lesenswerte Artikel sind fett hervorgehoben.

- https://dart.dev/overview
  - **Online Sandbox: https://dartpad.dev**
  - **Basics: https://dart.dev/language**
    - die weiteren untergeordneten Seiten des "Language"-Kapitels können auch hilfreich sein, wenn man sie mal kurz überfliegt
  - CLI Apps: https://dart.dev/tutorials/server/cmdline
  - Udemy Kurs: https://www.udemy.com/course/complete-dart-guide/?couponCode=SKILLS4SALEB
  - API: https://api.dart.dev/stable/3.5.1/index.html
  - Core Libraries: https://dart.dev/libraries
  - https://dart.dev/resources/books
- **Cheat Sheet: https://dart.dev/codelabs/dart-cheatsheet**
- Codelabs/Tutorials: https://dart.dev/tutorials
- Codestyle Konventionen (per Lint erschlagbar): https://dart.dev/effective-dart/style

## Einstieg

Wie aus dem [Cheat Sheet](https://dart.dev/resources/dart-cheatsheet) und der [Introduction to Dart](https://dart.dev/language) ersichtlich, ist die Code-Syntax sehr ähnlich zu TypeScript. Dies betrifft:

- Kontrollstrukturen (if, while, for, break, continue)
- Destructuring-Patterns (siehe auch https://dart.dev/language/patterns)
- Funktions- und Variablendefinitionen (diese können auch ohne umgebende Klasse global definiert werden, sodass nicht jede Methode/Variable krampfhaft in eine Klasse verpackt werden muss)
- Funktionen können selbst als Werte übergeben werden (sog. "tear-offs"), um bspw. Lambdas zu vereinfachen
- Zugriff auf nullable Werte
- Collections
- Arrow-Functions
- [Exception Handling](#exception-handling)

Zusätzlich gibt es aber viel syntaktischen Zucker, um Code kürzer und lesbarer schreiben zu können:

- https://dart.dev/resources/dart-cheatsheet#null-aware-operators
- https://dart.dev/resources/dart-cheatsheet#cascades
- https://dart.dev/resources/dart-cheatsheet#optional-positional-parameters
- https://dart.dev/resources/dart-cheatsheet#named-parameters
- mehr Details zu Funktionen: https://dart.dev/language/functions
- https://dart.dev/language/branches (ähnlich zu `switch` in TypeScript, aber mächtiger)
  - sehr mächtig im Zusammenspiel mit Patterns: https://dart.dev/language/pattern-types
- https://dart.dev/language/records (inline-Definition von Typen, ohne diesen explizit zu benennen - bspw. nützlich, um aus einer Funktion mehrere Rückgabewerte zurückzugeben)

In Bezug auf den Umgang mit Klassen ist Dart recht ähnlich zu Kotlin (bzw. Java mit viel syntaktischem Zucker). Siehe auch:

- https://dart.dev/resources/dart-cheatsheet#getters-and-setters
- https://dart.dev/resources/dart-cheatsheet#using-this-in-a-constructor
- https://dart.dev/resources/dart-cheatsheet#initializer-lists
- https://dart.dev/resources/dart-cheatsheet#named-constructors
- https://dart.dev/resources/dart-cheatsheet#factory-constructors
- https://dart.dev/resources/dart-cheatsheet#redirecting-constructors
- https://dart.dev/resources/dart-cheatsheet#const-constructors
- https://www.fluttersolution.com/2023/04/understanding-access-modifiers-in-dart.html

Dart setzt sich aus verschiedenen Libraries zusammen (Details siehe https://dart.dev/overview#libraries). Über gewisse Standard-Libraries hinaus können aber auch weitere hinzugefügt werden.

> Für einen schnellen Syntax-Überblick über einige Grundkonzepte siehe: [Dart](./Dart.md)

## Installation

> siehe auch: https://dart.dev/get-dart

Kann im Zuge der Installation von Flutter mit erledigt werden.

## Typsystem

Dart verwendet ein statisches null-sicheres Typsystem. Nullable Typen werden mit `?` markiert. Die Angabe von Typen ist jedoch optional, da zumeist durch Typinferenz automatisch die Erkennung von Typen möglich ist.

> Vergleich zu TypeScript: Es bleibt fast alles beim Alten.
>
> - `undefined` gibt es nicht. Stattdessen nur `null`.
> - Pluspunkt: Dart ist zur Runtime null-safe.

Typchecks können mit Operatoren wie `is` oder `is!` erfolgen (siehe https://dart.dev/language/operators#type-test-operators).

Eigene Typen können mit `typedef` definiert werden (siehe https://dart.dev/language/typedefs).

## Variablen

Variablen werden mit `final`/`const` oder mit `var` deklariert. Bei Instanzvariablen von Klassen wird `var` weggelassen.

Sichtbarkeit von Variablen wird _nicht_ über Keywords wie `private` oder `public` geregelt, sondern implizit durch die Benennung entschieden. Ein Unterstrich `_` sorgt dafür, dass eine Variable `private` wird.

## Exception Handling

In Dart kann jedes non-null Objekt als Fehlerobjekt geworfen werden. Dies erlaubt beispielsweise die Definition eines eigenen Fehlertyps mit vielen Metadaten, der dann beliebig weiter verarbeitet werden kann.

> Mehr Details: https://dart.dev/language/error-handling

## Klassen und Objekte

Klassen funktionieren grundsätzlich ähnlich zu Kotlin (und somit ähnlich zu Java).

Hier eine Liste der Besonderheiten:

- Grundwissen:
  - Jede Klasse erzeugt implizit auch ein interface. D.h. jede Klasse kann von einer anderen Klasse mit `implements` als Interface aufgegriffen werden.
  - Jede Klasse verfügt über einen Default-Konstruktor ohne sämtliche Parameter.
  - Klassen können über mehrere benannte Konstruktoren verfügen (siehe https://dart.dev/language/constructors#named-constructors).
  - Mit `const`-Konstruktoren können Singletons erzeugt werden (siehe https://dart.dev/language/constructors#constant-constructors).
  - Mit `factory`-Konstruktoren können komplexe Operationen bei der Erzeugung von Objekten vorgenommen werden, ohne `final`-Instanzvariablen aufweichen zu müssen (https://dart.dev/language/constructors#factory-constructors).
  - Die Initialisierung von Instanzvariablen ist auf verschiedenen drei Wegen möglich (siehe https://dart.dev/language/constructors#instance-variable-initialization).
  - Für Klassen können custom-Operatoren definiert werden (siehe https://dart.dev/language/methods#operators).
  - Zusätzlich zu den Instanzvariablen einer Klasse können weitere getter/setter definiert werden, um weitere Variablen hinzuzufügen, die auf anderen Instanzvariablen basieren (siehe https://dart.dev/language/methods#getters-and-setters).
- Mächtige Features:
  - Mit `mixins` ist Mehrfachvererbung möglich (siehe https://dart.dev/language/mixins).
  - `enums` sind sehr mächtig (ähnlich wie in Kotlin), da sie über eigene Attribute verfügen und somit ganze Codesets innerhalb eines Enums definiert werden können (siehe https://dart.dev/language/enums).
  - Klassen können (ähnlich wie in Kotlin) über Extension-Methods ohne Erzeugung einer Kindklasse um Methoden erweitert werden (siehe https://dart.dev/language/extension-methods).
- Weiteres (in das ich mich noch nicht näher eingelesen habe):
  - https://dart.dev/language/extension-types
  - https://dart.dev/language/callable-objects

## Asynchrone Ausführung

`Futures` werden für die Ausführung von asynchronem Code verwendet. Diese müssen mit `await` abgewartet werden oder können mit `.then(...)` bzw. `.catchError(...)` behandelt werden. Funktionen, die asynchrone Aufrufe abwarten, müssen das `async`-Keyword aufweisen.

> Vergleich zu TypeScript: Es bleibt alles beim Alten.

Außerdem können mit Streams Ketten von Werten behandelt werden, die sequenziell zurückgegeben werden.

Siehe:

- https://dart.dev/language/concurrency#streams
- https://dart.dev/language/async#handling-streams

## Threads

Thread-ähnliche Strukturen werden via `isolates` abgebildet. Die App selbst läuft auf einem `main isolate`, von dem ausgehend weitere erzeugt werden können.

Jeder `isolate` verfügt über eine eigene Speicherverwaltung, sodass Konfliktsituationen (aka Race Conditions) möglichst verhindert werden.

> Mehr Details:
>
> - https://dart.dev/language/concurrency
> - https://dart.dev/language/isolates
