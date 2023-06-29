## For Loop

Key ve value'a göre iterasyon örneği:

```swift
let numberOfLegs = ["spider": 8, "ant": 6, "cat": 4]
for (animalName, legCount) in numberOfLegs {
    print("\(animalName)s have \(legCount) legs")
}
```

Aralık olarak iterasyon:

```swift
for index in 1...5 {
    print("\(index) times 5 is \(index * 5)")
}
// 1 times 5 is 5
// 2 times 5 is 10
// 3 times 5 is 15
// 4 times 5 is 20
// 5 times 5 is 25
```

İndex kullanılmayacaksa tanımlanmayabilir:

```swift
let base = 3
let power = 10
var answer = 1
for _ in 1...power {
    answer *= base
}
print("\(base) to the power of \(power) is \(answer)")
// Prints "3 to the power of 10 is 59049"
```

## For Loop'ta Value Binding

```swift
let numbers = [1, 2, 3, 4, 5]

for case let number in numbers where number % 2 == 0 {
    print("\(number) çift bir sayıdır.")
}
```

