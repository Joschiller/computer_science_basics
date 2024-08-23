# Dart Quickstart (de)

## Referenzen

- https://dart.dev/overview
  - Online Sandbox: **https://dartpad.dev**
  - Basics: **https://dart.dev/language**
  - CLI Apps: https://dart.dev/tutorials/server/cmdline
  - Udemy Kurs: https://www.udemy.com/course/complete-dart-guide/?couponCode=SKILLS4SALEB
  - API: https://api.dart.dev/stable/3.5.1/index.html
  - Core Libraries: https://dart.dev/libraries
  - https://dart.dev/resources/books
- **https://dart.dev/codelabs/dart-cheatsheet**

## Einstieg

Dart verwendet ein statisches null-sicheres Typsystem. Nullable Typen werden mit `?` markiert. Die Angabe von Typen ist jedoch optional, da zumeist durch Typinferenz automatisch die Erkennung von Typen möglich ist.

> Vergleich zu TypeScript: Es bleibt fast alles beim Alten.
> - `undefined` gibt es nicht. Stattdessen nur `null`.
> - Pluspunkt: Dart ist zur Runtime null-safe.

Dart setzt sich aus verschiedenen Libraries zusammen (Details siehe https://dart.dev/overview#libraries). Über gewisse Standard-Libraries hinaus können aber auch weitere hinzugefügt werden.

> Für einen schnellen Syntax-Überblick siehe: [Dart](./Dart.md)

## Installation

> siehe auch: https://dart.dev/get-dart

Kann im Zuge der Installation von Flutter mit erledigt werden.

## Asynchrone Ausführung

`Futures` werden für die Ausführung von asynchronem Code verwendet. Diese müssen mit `await` abgewartet werden. Funktionen, die asynchrone Aufrufe enthalten, müssen das `async`-Keyword aufweisen.

> Vergleich zu TypeScript: Es bleibt alles beim Alten.

## Threads

Thread-ähnliche Strukturen werden via `isolates` abgebildet. Die App selbst läuft auf einem `main isolate`, von dem ausgehend weitere erzeugt werden können.
