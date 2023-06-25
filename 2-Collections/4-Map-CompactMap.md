## Map Kullanımı

Map bir arrayden yeni bir array oluşturmak için kullanılıyor.

```swift
let numbers = [1, 2, 3, 4, 5]
let doubledNumbers = numbers.map { $0 * 2 }
print(doubledNumbers) // [2, 4, 6, 8, 10]
```

```swift
let names = ["John", "Paul", "George", "Ringo"]
let uppercasedNames = names.map { (names) -> String in
    return names.uppercased()
 }
print(uppercasedNames) // ["JOHN", "PAUL", "GEORGE", "RINGO"]
```

```swift
let numbers = [1, 2, 3, 4, 5]
let strings = numbers.map { number in return String(number) }
print(strings) // ["1", "2", "3", "4", "5"]
```
 
```swift
let numbers = [1, 2, 3, 4, 5]
let strings = numbers.map {( String($0)) }
print(strings) // ["1", "2", "3", "4", "5"]
```

compactMap ise Map ile aynı işi yapar fakat nil değerleri atlar.

```swift
let numbers = ["1", "2", "3", "4", "5", "A", "B", "C", "D", "E"]
let mapped: [Int?] = numbers.map { str in Int(str) }
print(mapped) // [1, 2, 3, 4, 5, nil, nil, nil, nil, nil]
let compactMapped: [Int] = numbers.compactMap { str in Int(str) }
print(compactMapped) // [1, 2, 3, 4, 5]
```



