## Dictionaries

Swift'te Dictionaryler key-value çiftleri şeklinde tanımlanır. Dictionarylerin keyleri ve valueleri aynı türden olmak zorunda değildir. Dictionarylerin içerisindeki keyler unique olmak zorundadır. Dictionarylerin içerisindeki valueler unique olmak zorunda değildir.

Boş bir dictionary oluşturma:

```swift
var namesOfIntegers = [Int: String]()
// namesOfIntegers is an empty [Int: String] dictionary
```

Yeni item eklerken doğrudan şöyle yazılabilir:

```swift
airports["LHR"] = "London"
```

Değer eklemek veya güncellemek için updateValue kullanılabilir. Bu fonksiyon eğer verilen parametre mevcutsa günceller, yoksa ekler.

```swift
if let oldValue = airports.updateValue("Dublin Airport", forKey: "DUB"){
    print("The old value for DUB was \(oldValue).")
}
// Prints "The old value for DUB was Dublin."
```

Eleman silmek için benzer şekilde:

```swift
if let removedValue = airports.removeValue(forKey: "DUB") {
    print("The removed airport's name is \(removedValue).")
} else {
    print("The airports dictionary doesn't contain a value for DUB.")
}
```

ya da

```swift
airports["APL"] = nil
```

## İterasyon

Key-Value ayrı ayrı alınabilir:

```swift
for airportCode in airports.keys {
    print("Airport code: \(airportCode)")
}
// Airport code: LHR
// Airport code: YYZ


for airportName in airports.values {
    print("Airport name: \(airportName)")
}
// Airport name: London Heathrow
// Airport name: Toronto Pearson
```

For/in iterasyonu:

```swift
for (airportCode, airportName) in airports {
    print("\(airportCode): \(airportName)")
}
// LHR: London Heathrow
// YYZ: Toronto Pearson
```
