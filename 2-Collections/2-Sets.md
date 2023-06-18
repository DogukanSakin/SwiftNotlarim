## Setler

İndex değeri olmadan aynı türdeki dataları saklar.

Örnek:

```swift
var letters = Set<Character>()
print("letters is of type Set<Character> with \(letters.count) items.")
// Prints "letters is of type Set<Character> with 0 items."
```

Bir seti Array olarak da tanımlayabiliriz:

```swift
var favoriteGenres: Set<String> = ["Rock", "Classical", "Hip hop"]
```

Swift inferences sayesinde şöyle de tanımlayabiliriz:

```swift
var favoriteGenres: Set = ["Rock", "Classical", "Hip hop"]
```

Arrayde kullandığımız insert, remove gibi fonksiyonlar burada da kullanılabilir.

Setlerde sıralama olmadığı için for ile iterasyon yaparken sıralı bir şekilde dönmeyebilir. Bunun için sorted fonksiyonu kullanılabilir.

```swift
for genre in favoriteGenres.sorted() {
    print("\(genre)")
}
// Classical
// Hip hop
// Jazz
// Rock
```

## Setlerde kesişim

<img src="https://docs.swift.org/swift-book/images/setVennDiagram~dark@2x.png" height="400" width="400">