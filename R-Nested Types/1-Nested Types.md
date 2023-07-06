## Nested Types

Nested Types, bir türün içinde başka bir türün tanımlanmasını ifade eder. Bir türün içinde başka bir yapı olan türleri tanımlamak, kod organizasyonunu geliştirir ve ilgili türleri daha düzenli bir şekilde gruplandırır.

İç içe geçmiş tipler sınıflar, struct'lar ve enum'lar için kullanılabilir. İç içe geçmiş tipler, dışarıdaki türe bağlıdır ve onun içinde kullanılır. Bu şekilde, dış türün içindeki özellikler veya işlevler iç içe geçmiş türe erişebilir ve onları kullanabilir.

Örnekler:

```swift
class OuterClass {
    // Dışarıdaki sınıfın özellikleri ve işlevleri

    class InnerClass {
        // İç içe geçmiş sınıfın özellikleri ve işlevleri
    }
}
```
```swift
struct OuterStruct {
    // Dışarıdaki yapıya ait özellikler

    struct InnerStruct {
        // İç içe geçmiş yapının özellikleri
    }
}
```
```swift
enum OuterEnum {
    // Dışarıdaki numaralandırmanın durumları

    enum InnerEnum {
        // İç içe geçmiş numaralandırmanın durumları
    }
}
```

Kapsamlı örnek:

```swift
struct BlackjackCard {


    // nested Suit enumeration
    enum Suit: Character {
        case spades = "♠", hearts = "♡", diamonds = "♢", clubs = "♣"
    }


    // nested Rank enumeration
    enum Rank: Int {
        case two = 2, three, four, five, six, seven, eight, nine, ten
        case jack, queen, king, ace
        struct Values {
            let first: Int, second: Int?
        }
        var values: Values {
            switch self {
            case .ace:
                return Values(first: 1, second: 11)
            case .jack, .queen, .king:
                return Values(first: 10, second: nil)
            default:
                return Values(first: self.rawValue, second: nil)
            }
        }
    }


    // BlackjackCard properties and methods
    let rank: Rank, suit: Suit
    var description: String {
        var output = "suit is \(suit.rawValue),"
        output += " value is \(rank.values.first)"
        if let second = rank.values.second {
            output += " or \(second)"
        }
        return output
    }
}
```

```swift