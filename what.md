# What to do and What not to do while working with the FLutter


- Always try to use ```var``` if not possible try explicite type always try to avoid ```dynamic```

## Some good practice for var


```dart
// BAD: hard to read due to nested generic types
List<List<Toppings>> pizza = List<List<Toppings>>();
for(List<Toppings> topping in pizza) {
    doSomething(topping);
}
// GOOD: the reader doesn't have to "parse" the code
// It's clearer what's going on
var pizza = List<List<Toppings>>();
for(var topping in pizza) {
    doSomething(topping);
}
```

When you don’t want to initialize a variable immediately, use the ```late``` keyword
```dart 
late List<String> names;
```

A final variable can be set only once there is no need for data type during declaring the final variable
SO we can say final is a restrictive var

## Data types
**Number**
- int
- double

Following methods are supported for them

- parse(string)
- abs()
- ceil()
- toString()

var a = 1.35e2 which is the equivalent of 1.35 * 102

var a = 0xF1A where 0xF1A equals to F1A in base 16 (3866 in base 10)

## Parsing
```dart
String value = "17";
var a = int.parse(value); // String-to-int conversion
var b = double.parse("0.98"); // String-to-double conversion
var c = int.parse("13", radix: 6); // Converts from 13 base 6
```
To convert anything to string just add ```.toString()``` at the end.
```dart
String v1 = 100.toString(); // v1 = "100";
String v2 = 100.123.toString(); // v2 = "100.123";
String v3 = 100.123.toStringAsFixed(2); // v3 = "100.12";
```

If the value is malformed then the plain parse method fails so here is the better way to do so
```dart
// 1. If the string is not a number, val is null
double? val = double.tryParse("12@.3x_"); // null
double? val = double.tryParse("120.343"); // 120.343
// 2. The onError callback is called when parsing fails
var a = int.parse("1_6", onError: (value) => 0); // 0
var a = int.parse("16", onError: (value) => 0); // 16
```

**Strings**
Ordered sequence of UTF-16 values (characters) surrounded by either single or double quotation 
There is a handy way to combine any value into String in dart called as shorthand to toString()
```dart
// No differences between s and t
var s = "Double quoted";
var t = 'Single quoted';
// Interpolate an integer into a string
var age = 25;
var myAge = "I am $age years old";
// Expressions need '{' and '}' preceeded by $
var test = "${25.abs()}"
// This is redundant, don't do it because ${} already calls toString()
var redundant = "${25.toString()}";
```
Multiline String
```dart
// Very useful for SQL queries, for example
var query = """
SELECT name, surname, age
FROM people
WHERE age >= 18
ORDER BY name DESC
""";
```

---

During concatenation
```dart
var s = 'I am ' + name + ' and I am ' + (23).toString() + ' y.o.'; // Avoid this
var s = 'I am $name. I am ${25} years old'; // Instead try this
```
If there is to much concatenation used use StringBuffer instead of String
```dart
var value = "";
for(var i = 0; i < 900000; ++i) {
value += "$i ";
}// This is not the best practice


var buffer = StringBuffer();
for(var i = 0; i < 900000; ++i)
buffer.write("$i ");
var value = buffer.toString();// Instead try this
