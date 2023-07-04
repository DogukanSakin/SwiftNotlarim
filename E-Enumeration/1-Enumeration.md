## Enumeration

Swift'te enum'lar, birbirine bağlı değerlerin bir arada tutulduğu bir yapıdır. Enum'lar, Objective-C'deki enum'lardan farklı olarak, birbirine bağlı değerlerin yanı sıra, fonksiyonlar ve hesaplanmış özellikler de içerebilir.

```swift
enum CompassPoint {
    case north
    case south
    case east
    case west
}

var directionToHead = CompassPoint.west

directionToHead = .east //farklı atama için
```
Buradaki case'lerin bir integer indexleri yoktur.

Case'ler tek satırda da yazılabilir:

```swift
enum Planet {
    case mercury, venus, earth, mars, jupiter, saturn, uranus, neptune
}
```

Enum'lar, bir türdür. Bu yüzden büyük harfle başlarlar.


## Enum'lar ve Switch

Enum'lar, switch ifadeleriyle kullanıldıklarında çok güçlüdürler. Enum'ların tüm case'lerini kapsayan bir switch ifadesi yazmak zorunda değilsiniz. Enum'ın tüm case'lerini kapsamayan bir switch ifadesi yazarsanız, default case'i yazmak zorunda değilsiniz.

```swift
directionToHead = .south

switch directionToHead {
case .north:
    print("Lots of planets have a north")
case .south:
    print("Watch out for penguins")
case .east:
    print("Where the sun rises")
case .west:
    print("Where the skies are blue")
}

// Prints "Watch out for penguins"
```

Enumları Switch ile kullanırken her case'i switch içerisinde yazmalıyız. Eğer tüm case'leri yazamazsak default case'i kullanmalıyız.

## allCases

Enum'ların tüm case'lerini almak için allCases kullanabiliriz.

```swift
enum Beverage: CaseIterable {
    case coffee, tea, juice
}

let numberOfChoices = Beverage.allCases.count
print("\(numberOfChoices) beverages available")

// Prints "3 beverages available"
```

allCase iterasyon için kullanılabilir:

```swift
for beverage in Beverage.allCases {
    print(beverage)
}

// coffee
// tea
// juice
```

## Değer Ayrıştırma

```swift
enum Barcode {
    case upc(Int, Int, Int, Int)
    case qrCode(String)
}

var productBarcode = Barcode.upc(8, 85909, 51226, 3)
productBarcode = .qrCode("ABCDEFGHIJKLMNOP")

switch productBarcode {
case let .upc(numberSystem, manufacturer, product, check):
    print("UPC : \(numberSystem), \(manufacturer), \(product), \(check).")
case let .qrCode(productCode):
    print("QR code: \(productCode).")
}
```

## Raw Değerler

Enum'lar, raw değerlerle de oluşturulabilir. Raw değerler, aynı türden olmalıdır. Raw değerler, String, Character, Integer veya Floating Point değerleri olabilir.

```swift
enum ASCIIControlCharacter: Character {
    case tab = "\t"
    case lineFeed = "\n"
    case carriageReturn = "\r"
}
```
Eğer raw değeri yoksa otomatik olarak verilen isim kullanılır:

```swift
enum MyEnum  {
    case A
    case B
    case C
}

print(MyEnum.A)
// Prints "A"
```

Raw değerlerinde integer için başlangıç değerinin belirlenmesiyle otomatik olarak arttırılır:

```swift
enum Planet: Int {
    case mercury = 1, venus, earth, mars, jupiter, saturn, uranus, neptune
}

print(Planet.earth.rawValue)
// Prints "3"
```

## Recursive Enumerations

Bir enum durumunun kendisiyle veya başka bir durumuyla ilişkilendirilmiş olduğu durumlarda kullanılır. Bu, enumların daha karmaşık ve yapısı iç içe geçmiş durumları temsil etmesine olanak tanır. Recursive Enumerations, enum'ların kendi içlerindeki değerleri kullanarak kendilerini çağırmasına izin verir. Recursive Enumerations, indirect anahtar kelimesiyle belirtilir.

```swift
enum Tree {
    case leaf
    indirect case node(left: Tree, right: Tree)
}

let tree = Tree.node(left: .leaf, right: .leaf)
```

Burada, Tree adında bir enum tanımlanmıştır. leaf durumu, ağacın yaprak düğümünü temsil ederken, node durumu ise ağacın iç düğümlerini temsil eder. node durumu, left ve right adında iki alt ağaçla ilişkilendirilmiştir.

Dikkat edilmesi gereken nokta, node durumunun indirect anahtar kelimesi ile işaretlenmiş olmasıdır. Bu, node durumunun özyinelemeli olduğunu belirtir ve alt ağaçlarının kendi enum durumlarını içerebileceği anlamına gelir.