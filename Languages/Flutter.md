# Flutter

- [Usage](#usage)
- [References](#references)
- [Overview](#overview)

## Usage

- mobile development with [Dart](./Dart.md)

## References

> Setup: https://docs.flutter.dev/get-started/install/windows/mobile
>
> - recommended:
>   - use VS Code with https://marketplace.visualstudio.com/items?itemName=Dart-Code.flutter
>   - install Flutter via VSCode
>
> https://flutter.dev/learn
>
> https://docs.flutter.dev/codelabs

> General philosophy: composition over inheritance -> wrap widgets within each other instead of adding new properties to existing widgets

## Overview

Useful hotkeys:
- F5: build and install
- right click (or Strg+.) on selected code -> "refactor" -> e.g. "Extract Widget"
- Strg+Shift+Space -> shows parameters of a currently called method

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
