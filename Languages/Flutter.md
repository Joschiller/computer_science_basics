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

## Useful Components

> Hint: use `const` when instantiating components that never change when re-rendering

- `Center`
- `SizedBox` for spacing
- `Column`/`Row`
  - `mainAxisAlignment: MainAxisAlignment.center` for centered UI
    - main axis for column is vertical
    - main axis for row is horizontal
  - `crossAxisAligment` references the axis orthogonal to the main axis
- `SafeArea`/`Expanded`
  - `SafeArea` only fills the needed area
  - `Expanded` fills all available area
- `ListView` provides a scrollable view
- `Stack` + `Positioned` works similar to constraint layout in Android
- `SafeArea` enures space around the actual content to mitigate overlaps with operating system UI
