# Flutter

- [Usage](#usage)
- [References](#references)
- [Overview](#overview)

## Usage

- mobile development
- UI framework
- based on [Dart](./Dart.md)

## References

> see [FlutterQuickstart](./FlutterQuickstart.md#referenzen)
>
> https://docs.flutter.dev/get-started/flutter-for/android-devs
>
> https://docs.flutter.dev/get-started/flutter-for/web-devs
>
> https://docs.flutter.dev/codelabs
>
> https://docs.flutter.dev/cookbook
>
> https://docs.flutter.dev/ui

> General philosophy: composition over inheritance -> wrap widgets within each other instead of adding new properties to existing widgets

## Stateless/Stateful Widgets

- stateless = state is managed outside the widget
- stateful = state is managed by the widget itself (manage state using instance variables and `setState`)

## Useful Components

> Hint: use `const` when instantiating components that never change when re-rendering

- `Center`
- `SizedBox` for spacing
- `Column`/`Row`
  - `mainAxisAlignment: MainAxisAlignment.center` for centered UI
- `SafeArea`/`Expanded`
  - `SafeArea` only fills the needed area
  - `Expanded` fills all available area
