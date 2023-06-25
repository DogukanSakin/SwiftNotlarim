## Flatmap

Birden fazla array varsa ve bu arraylerin içindeki elemanları tek bir array içinde toplamak istiyorsak flatmap kullanırız.

```swift
let numbers = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
let flatMapped = numbers.flatMap { $0 }
print(flatMapped) // [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

## Reduce

Reduce fonksiyonu bir arrayi tek bir değere indirgemek için kullanılır. Örneğin bir arraydeki sayıların toplamını bulmak için reduce kullanabiliriz.

```swift
let numbers = [1, 2, 3, 4, 5]
let sum = numbers.reduce(0) { $0 + $1 }
print(sum) // 15
```

