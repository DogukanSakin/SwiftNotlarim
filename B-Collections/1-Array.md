## Listler - Arraylar

Arrayler, birden fazla veriyi tek bir değişkende tutmamızı sağlayan veri tipleridir. Array oluşturmak için köşeli parantezler kullanılır.

Array'leri let yerine var ile tanımlamak mantıklıdır. Çünkü append gibi fonksiyonlar ile array'e yeni elemanlar eklenebilir.


```swift
var someInts = [Int]()
print("someInts is of type [Int] with \(someInts.count) items.")
// Prints "someInts is of type [Int] with 0 items."
```

Bu tanımlama initilaze edilmiş listedir. Initilaze edilmemiş liste için:

```swift
var someInts = [Int]
```
Eğer başta değer verirsek listemiz initilaze edilmiş olur.

```swift
var someInts = [1, 2, 3]
```

Ayrıca default değer ile Array oluşturabiliriz:

```swift
var threeDoubles = Array(repeating: 0.0, count: 3)
// threeDoubles is of type [Double], and equals [0.0, 0.0, 0.0]
```

+ operatorü ile aynı türden arrayleri birleştirebiliriz:

```swift
var anotherThreeDoubles = Array(repeating: 2.5, count: 3)
// anotherThreeDoubles is of type [Double], and equals [2.5, 2.5, 2.5]
var sixDoubles = threeDoubles + anotherThreeDoubles
// sixDoubles is inferred as [Double], and equals [0.0, 0.0, 0.0, 2.5, 2.5, 2.5]
```
## Array Eleman Ekleme

append fonksiyonu kullanılabilir ya da += operatörü ile eklenebilir.

```swift
var shoppingList = ["Eggs", "Milk"]
shoppingList.append("Flour")
// shoppingList now contains 3 items, and someone is making pancakes
shoppingList += ["Baking Powder"]
// shoppingList now contains 4 items
shoppingList += ["Chocolate Spread", "Cheese", "Butter"]
// shoppingList now contains 7 items
```

Belirli bir index'e eklemek için insert fonksiyonu kullanılır.

```swift
shoppingList.insert("Maple Syrup", at: 0)
// shoppingList now contains 7 items
// "Maple Syrup" is now the first item in the list
```

## Array Eleman Çıkarma

remove fonksiyonu kullanılır.

```swift
let mapleSyrup = shoppingList.remove(at: 0)
```

sondan çıkartmak için:

```swift
let apples = shoppingList.removeLast()
```

## Array Filtreleme

```swift
var numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9]

var filteredNumbers = numbers.filter { $0 % 2 == 0 } // [2, 4, 6, 8]
```
Burada $0 listenin elemanlarını temsil eder ve tüm elemanları gezmemizi sağlar. $0 yerine başka bir isim de verebiliriz.

## Array İterasyonu

Normalde for/in ile yapılabilir ama hem index hem de value'ya ihtiyacımız varsa enumerated() fonksiyonu kullanılabilir.

```swift
for (index, value) in array.enumerated() {
    print("index: \(index), value: \(value)")
}
```
