# Flutter Quickstart (de)

## Referenzen

- Setup: https://docs.flutter.dev/get-started/install/windows/mobile
  - Empfehlung:
    - Nutzung von VS Code mit https://marketplace.visualstudio.com/items?itemName=Dart-Code.flutter
    - Flutter via VS Code installieren
- Einstieg in viele Artikel je nach bisheriger Erfahrung: https://flutter.dev/learn
  - Codelab für eine erste Flutter-App: https://docs.flutter.dev/get-started/codelab

## Einstieg

Mittels Flutter gebaute UI setzt sich aus Widgets zusammen. Die Struktur von Widgets ist sehr ähnlich zu React-Code und verhält sich auch ähnlich.

Flutter verfolgt dabei folgende Ansätze (die sehr ähnlich zu React sind):

- Alles, was in der UI sichtbar ist, sind Widgets. (Ähnlich zu den Komponenten in React. Am ehesten sind die Widgets zu klassenbasierten React-Komponenten vergleichbar.)
- Widgets werden via Komposition miteinander kombiniert. D.h. sie werden ineinander geschachtelt. (Sehr ähnlich zu React bzw. HTML.)
- State und UI werden voneinander getrennt definiert, aber die UI reagiert per re-rendering auf geänderten State. (Sehr ähnlich zu React/Redux, nur dass in Flutter immer explizit die Nutzer des States benachrichtigt werden müssen.)

## Hot Reload

Flutter verfügt über ein Hot-Reload Feature, um Code-Änderungen schnell anzuzeigen. Dies ist besonders bei kleineren Änderungen praktisch, um die Auswirkungen live nachvollziehen zu können.

Werden komplexere Änderungen am Code vorgenommen ist zumeist dennoch ein kompletter Neustart (Hot Restart) der App oder sogar das vollständige erneute Kompilieren nötig.

## Unterstützung durch VS Code

Durch Nutzung von VS Code und der entsprechenden Plugins für Dart und Flutter wird viel Unterstützung bei der Entwicklung angeboten. Dies erstreckt sich von Befehlen zum Erstellen von Projekten bis zum Refactoring von Code.

- `F1` -> `Flutter: New Project` -> `Application` = Anlegen eines neuen Projekts
- Codestelle markieren -> `Strg` + `.` (oder Rechtsklick) -> `Extract ...`/`Wrap with ...` = verschiedene Optionen zum schnellen Refactoring oder zur schnellen Ergänzung von Komponenten
- `Strg` + `Shift` + `Leertaste` =  Parameterliste einer Methode anzeigen
