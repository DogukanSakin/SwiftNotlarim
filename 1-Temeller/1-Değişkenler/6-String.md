## String

Multiline için:

```
let quotation = """
The White Rabbit put on his spectacles.  "Where shall I begin,
please your Majesty?" he asked.
"""
```

Kodu kolay okunabilir hale getirmek için:

```
let softWrappedQuotation = """
The White Rabbit put on his spectacles.  "Where shall I begin, \
please your Majesty?" he asked.
"""
```

Swift'te String oluşturulduğunda beraberinde bir kopyası da oluşturulur ve bu string değeri bir fonksiyona vs. iletildiğinde orjinal hali değil kopyası gönderilir. Bu sayede orjinal string değeri korunmuş olur.

Swift'te bir karakter için değişken oluşturulabilir.

Örneğin:

```
let exclamationMark: Character = "!"
```

Bir string array'inden string oluşturulabilir benzer şekilde bir string'te iterasyon uygulanabilir array gibi davranır.

Örneğin:

```
let catCharacters: [Character] = ["C", "a", "t", "!", "?"]
let catString = String(catCharacters)
print(catString)
// Prints "Cat!?"
```


## Kaçış Karakterleri

```
let wiseWords = "\"Imagination is more important than knowledge\" - Einstein"
let dollarSign = "\u{24}"        // $,  Unicode scalar U+0024
let blackHeart = "\u{2665}"      // ♥,  Unicode scalar U+2665
let sparklingHeart = "\u{1F496}" // 💖, Unicode scalar U+1F496
```

- Burada ek olarak özel karakterler için # kullanılabilir. Örneğin:

```
let filePath = #"C:\Users\Username\Documents\"#
print(filePath) // "C:\Users\Username\Documents\"
```


## Stringlerde Indexler

```
let greeting = "Guten Tag!"
greeting[greeting.startIndex]
// G
greeting[greeting.index(before: greeting.endIndex)]
// !
greeting[greeting.index(after: greeting.startIndex)]
// u
let index = greeting.index(greeting.startIndex, offsetBy: 7)
greeting[index]
// a
```
Burada endIndex'e ve endIndex'in sonrasına erişmek string range'inden çıkmak olduğu için hata verir.

```
greeting[greeting.endIndex] // Error
greeting.index(after: greeting.endIndex) // Error
```

## Stringlerde insert ve remove

```
var welcome = "hello"
welcome.insert("!", at: welcome.endIndex)
// welcome now equals "hello!"
welcome.insert(contentsOf: " there", at: welcome.index(before: welcome.endIndex))
// welcome now equals "hello there!"
welcome.remove(at: welcome.index(before: welcome.endIndex))
// welcome now equals "hello there"
let range = welcome.index(welcome.endIndex, offsetBy: -6)..<welcome.endIndex
welcome.removeSubrange(range)
// welcome now equals "hello"
```

## Substringler

Substringler stringlerden farklı olarak orjinal stringin bir kısmını tutar. Bu sayede orjinal stringin kopyası oluşturulmaz. Substringler bellekte ya orjinal string'in bellekteki yerinde ya da başka bir substring için ayrılan bellek alanında tutulur. Substring'leri uzun süreki bellekte saklamak için işlem sonrası yeni bir string değişken olarak tanımlanmalıdırlar.

```
let greeting = "Hello, world!"
let index = greeting.firstIndex(of: ",") ?? greeting.endIndex
let beginning = greeting[..<index]
// beginning is "Hello"

// Convert the result to a String for long-term storage.
let newString = String(beginning)
```

<img src="https://docs.swift.org/swift-book/images/stringSubstring~dark@2x.png" width="300" height="300">

## String Eşitliği

Stringlerin içeriği eşit olduğu sürece eşittirler.

```
let quotation = "We're a lot alike, you and I."
let sameQuotation = "We're a lot alike, you and I."
if quotation == sameQuotation {
    print("These two strings are considered equal")
}
// Prints "These two strings are considered equal"
```

- hasPrefix ve hasSuffix ile stringlerin başlangıç ve bitişlerini kontrol edebiliriz.


```
let romeoAndJuliet = [
    "Act 1 Scene 1: Verona, A public place",
    "Act 1 Scene 2: Capulet's mansion",
    "Act 1 Scene 3: A room in Capulet's mansion",
    "Act 1 Scene 4: A street outside Capulet's mansion",
    "Act 1 Scene 5: The Great Hall in Capulet's mansion",
    "Act 2 Scene 1: Outside Capulet's mansion",
    "Act 2 Scene 2: Capulet's orchard",
    "Act 2 Scene 3: Outside Friar Lawrence's cell",
    "Act 2 Scene 4: A street in Verona",
    "Act 2 Scene 5: Capulet's mansion",
    "Act 2 Scene 6: Friar Lawrence's cell"
]

var act1SceneCount = 0

for scene in romeoAndJuliet {
    if scene.hasPrefix("Act 1 ") {
        act1SceneCount += 1
    }
}

print("There are \(act1SceneCount) scenes in Act 1")

// Prints "There are 5 scenes in Act 1"
```

- hasSuffix ile de bitiş kontrolü yapılabilir.

