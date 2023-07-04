## Touples Karşılaştırmaları

Soldan sağa doğru karşılaştırma yapılır. İlk true yakalanana kadar devam eder. 

```swift
(1, "zebra") < (2, "apple")   // true because 1 is less than 2; "zebra" and "apple" aren't compared
(3, "apple") < (3, "bird")    // true because 3 is equal to 3, and "apple" is less than "bird"
(4, "dog") == (4, "dog")      // true because 4 is equal to 4, and "dog" is equal to "dog"
```

Bool değer karşılaştırılamadğı için her Touples'da her zaman false döner.

```swift
("blue", -1) < ("purple", 1)        // OK, evaluates to true
("blue", false) < ("purple", true)  // Error because < can't compare Boolean values
```