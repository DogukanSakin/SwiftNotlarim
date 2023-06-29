## Switch

Swift'te switch kullanırken break gerektirmeden ilk işleşme sağlandığı an kontrolden çıkarak performans artışı sağlanır.


Birden fazla kontrol için virgül kullanılabilir.

```swift
let anotherCharacter: Character = "a"
switch anotherCharacter {
case "a", "A":
    print("The letter A")
default:
    print("Not the letter A")
}
// Prints "The letter A"
```

Swift'te switch içerisinde aralık eşleştirme mevcuttur.

```swift
et approximateCount = 62
let countedThings = "moons orbiting Saturn"
let naturalCount: String
switch approximateCount {
case 0:
    naturalCount = "no"
case 1..<5:
    naturalCount = "a few"
case 5..<12:
    naturalCount = "several"
case 12..<100:
    naturalCount = "dozens of"
case 100..<1000:
    naturalCount = "hundreds of"
default:
    naturalCount = "many"
}
print("There are \(naturalCount) \(countedThings).")
// Prints "There are dozens of moons orbiting Saturn."
```

Switch'ler touples ile beraberde kullanılabilir ve aşama aşama eşleştirme yapılabilir. Ayrıca _ ile eşleşmeyen değerler için default değer belirlenebilir.

```swift
let somePoint = (1, 1)
switch somePoint {
case (0, 0):
    print("\(somePoint) is at the origin")
case (_, 0):
    print("\(somePoint) is on the x-axis")
case (0, _):
    print("\(somePoint) is on the y-axis")
case (-2...2, -2...2):
    print("\(somePoint) is inside the box")
default:
    print("\(somePoint) is outside of the box")
}
// Prints "(1, 1) is inside the box"

```

Switch case'de where sorgusu da kullanılabilir.

```swift
let yetAnotherPoint = (1, -1)
switch yetAnotherPoint {
case let (x, y) where x == y:
    print("(\(x), \(y)) is on the line x == y")
case let (x, y) where x == -y:
    print("(\(x), \(y)) is on the line x == -y")
case let (x, y):
    print("(\(x), \(y)) is just some arbitrary point")
}
// Prints "(1, -1) is on the line x == -y"
```

## Value Bindings

Switch case içerisinde değerlerin atanması için value bindings kullanılabilir.

```swift
let yetAnotherPoint = (2, 0)
switch yetAnotherPoint {
case (let distance, 0), (0, let distance):
    print("On an axis, \(distance) from the origin")
default:
    print("Not on an axis")
}
// Prints "On an axis, 2 from the origin"
```

## Fallthrough

Normalde swift switch case'de bir case'in sonunda break kullanılmazsa otomatik olarak break eklenir. Ancak bazen birden fazla case'in aynı kodu çalıştırması gerekebilir. Bu durumda fallthrough kullanılabilir.

```swift
let character: Character = "a"

switch character {
    case "a", "A":
        print("Vowel")
        fallthrough
    default:
        print("Character")
}
```