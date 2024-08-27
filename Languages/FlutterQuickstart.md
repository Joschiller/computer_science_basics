# Flutter Quickstart (de)

> Die grundsätzliche Denkweise bei der Entwicklung mit Flutter ist sehr ähnlich zu React.

## Referenzen

Wichtige Übersichten sind fett hervorgehoben.

- Setup: https://docs.flutter.dev/get-started/install/windows/mobile
  - Empfehlung:
    - Nutzung von VS Code mit https://marketplace.visualstudio.com/items?itemName=Dart-Code.flutter
    - Flutter via VS Code installieren
- Einstieg in viele Artikel je nach bisheriger Erfahrung: https://flutter.dev/learn
  - Codelab für eine erste Flutter-App: https://docs.flutter.dev/get-started/codelab
  - Einstieg zum Layout im Vergleich zur Webentwicklung: https://docs.flutter.dev/get-started/flutter-for/web-devs
- Codelabs/Tutorials: https://docs.flutter.dev/codelabs
- **Anleitungen für konkrete Problemlösungen: https://docs.flutter.dev/cookbook**
- **Einführung in UI-Komponenten: https://docs.flutter.dev/ui**
- **Widget Überblick: https://docs.flutter.dev/ui/widgets**

## Einstieg

Mittels Flutter gebaute UI setzt sich aus Widgets zusammen. Die Struktur von Widgets ist sehr ähnlich zu React-Code und verhält sich auch ähnlich.

Flutter verfolgt dabei folgende Ansätze (die sehr ähnlich zu React sind):

- Alles, was in der UI sichtbar ist, sind Widgets. (Ähnlich zu den Komponenten in React. Am ehesten sind die Widgets zu klassenbasierten React-Komponenten vergleichbar.)
- Widgets werden via Komposition miteinander kombiniert, indem sie ineinander geschachtelt werden. (Sehr ähnlich zu React bzw. HTML.) D.h. hier wird **nicht** auf Vererbung gesetzt.
- State und UI werden voneinander getrennt definiert, aber die UI reagiert per re-rendering auf geänderten State. (Sehr ähnlich zu React/Redux, nur dass in Flutter immer explizit die Nutzer des States benachrichtigt werden müssen.)

Flutter unterscheided zwischen "stateless" und "stateful" Widgets:

- "stateless" Widgets (`extends StatelessWidget`) werden verwendet, wenn sie von nichts weiter abhängen als der Konfiguration, die dem Widget übergeben wird. Der State des Widgets wird dann außerhalb durch andere Komponenten verwaltet. (Vergleichbar zu Props in React.)
- "stateful" Widgets (`extends StatefulWidget`) werden verwendet, wenn sie selbst einen Zustand verwalten müssen. Der State wird mittels Instanzvariablen und `setState` abgebildet. (Vergleichbar zu `useState` in React.)

Jedes Widget führt beim Rerender eine `build`-Methode aus, die die Beschreibung der UI enthält (den "Widget-Tree").

> Weitere Informationen zum Widget-Lifecycle: https://docs.flutter.dev/ui#responding-to-widget-lifecycle-events

Das Layout der Widgets wird in Flutter auch über Widgets realisiert. So gibt es beispielsweise Widgets wie `Center`, `Padding`, `SizedBox`, ..., mit denen UI-Elemente angeordnet werden können.

## Hot Reload

Flutter verfügt über ein Hot-Reload Feature, um Code-Änderungen schnell anzuzeigen. Dies ist besonders bei kleineren Änderungen praktisch, um die Auswirkungen live nachvollziehen zu können.

Werden komplexere Änderungen am Code vorgenommen ist zumeist dennoch ein kompletter Neustart (Hot Restart) der App oder sogar das vollständige erneute Kompilieren nötig.

## Unterstützung durch VS Code

Durch Nutzung von VS Code und der entsprechenden Plugins für Dart und Flutter wird viel Unterstützung bei der Entwicklung angeboten. Dies erstreckt sich von Befehlen zum Erstellen von Projekten bis zum Refactoring von Code.

- `F1` -> `Flutter: New Project` -> `Application` = Anlegen eines neuen Projekts
- Codestelle markieren -> `Strg` + `.` (oder Rechtsklick) -> `Extract ...`/`Wrap with ...` = verschiedene Optionen zum schnellen Refactoring oder zur schnellen Ergänzung von Komponenten
- `Strg` + `Shift` + `Leertaste` =  Parameterliste einer Methode anzeigen

## Genereller Aufbau einer Flutter App

Kern einer Flutter-App ist die `main`-Methode:

```dart
void main() {
  runApp(MyApp());
}
```

Alles innerhalb von `runApp` sind Widgets.

Beim Anlegen eines neuen Widgets ist die Grundstruktur folgende:

```dart
class ExampleWidget extends StatelessWidget {
  const ExampleWidget({
    super.key,
    required this.someAttribute, // overhand attributes of the widget
  });

  // declare attributes of the widget
  final String someAttribute;

  @override
  Widget build(BuildContext context) {
    return ...; // return widget tree
  }
}
```

Bei stateful Widgets wird die State-Definition vom Widget selbst getrennt.

```dart
class ExampleWidget extends StatefulWidget {
  const ExampleWidget({
    super.key,
    required this.someAttribute, // overhand attributes of the widget
  });

  // declare attributes of the widget
  final String someAttribute;

  @override
  State<ExampleWidget> createState() => _ExampleWidgetState();
}

class _ExampleWidgetState extends State<ExampleWidget> {
  var someState = 0; // use setState to update

  @override
  Widget build(BuildContext context) {
    return ...; // return widget tree
  }
}
```

## Material Design

Um Material Design nutzen zu können (siehe https://docs.flutter.dev/ui#basic-widgets):

- `uses-material-design: true` im `flutter`-Abschnitt der `pubspec.yaml` aufnehmen.
- `runApp` mit einer `MaterialApp` befüllen

## Erkennung verschiedener Gesten

Mittels des `GestureDetector`s können verschiedene Gesten auf Widgets erkannt werden: https://docs.flutter.dev/ui/interactivity/gestures
