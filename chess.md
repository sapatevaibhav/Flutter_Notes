## Okay, so I am learning Flutter and at the point I am build Chess game in flutter during this Newly learned things will be addressed in this file

# Chess

---

First thing first creating ```8 x 8``` chess board.
to do so

## 1. GridView.builder

```dart
GridView.builder(
  itemCount: 8 * 8, // This is the size of GridView we need 8 by 8 for chess
  physics: const NeverScrollableScrollPhysics(), // Set to non scrollable widget
  gridDelegate: const SliverGridDelegateWithFixedCrossAxisCount(
    crossAxisCount: 8, // column count set to default 8
  ),
  itemBuilder: (context, index) {
    return Square(isWhite: isWhite(index)); // Background color to each box / grid is specified here
  },
),
```

## 2. isWhite

The main game is here as we need some advanced math required here

```dart
bool isWhite(int index) {
  int x = index ~/ 8; // int divison operator 
  int y = index % 8; // mod
  bool isWhite = (x + y) % 2 == 0; // addition of them is even or odd
  return isWhite; // if 0 then grey else white
}
```