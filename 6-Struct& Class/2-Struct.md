## Struct

Swift'te Sturct'lar Class ile aynı amaç doğrultusunda kullanılırlar. Ancak Struct bazı özellikleriyle Class'lardan ayrılmıştır.

Oluşturma syntax'ı aşağıdaki gibidir.

```swift
struct SomeStruct {
    // struct definition goes here
}
```

Swift'te struct gibi değer tipli yapıların bütünü kopyalandığında bellek yönetimi için aynı alanlar kullanılır. Bu olay enumlarda da vardır:

```swift
enum CompassPoint {
    case north, south, east, west
    mutating func turnNorth() {
        self = .north
    }
}
var currentDirection = CompassPoint.west
let rememberedDirection = currentDirection
currentDirection.turnNorth()


print("The current direction is \(currentDirection)")
print("The remembered direction is \(rememberedDirection)")
// Prints "The current direction is north"
// Prints "The remembered direction is west"
```

## Mutable & Immutable

Struct içerisinde fonksiyonlar aracılığıyla tanımlı ifadeleri değiştirmek için mutating anahtar kelimesiyle tanımlamaya ihtiyaç duyarız.

```swift
struct SomeStruct {
    var name: String
    mutating func changeName(name: String) {
        self.name = name
    }
}
```

