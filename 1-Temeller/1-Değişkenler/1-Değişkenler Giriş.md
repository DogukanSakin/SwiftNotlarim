## Swift'te Değişken Tipleri

Swift Type Safety bir dil olduğu için kullanılabilir tipler:

- Int
- Float
- Double
- String
- Bool

## Swift'te Sabit/Değişebilen Tanımlama

Değişebilenleri tanımlarken var kullanılır.

Örneğin:

```
var d1: Int = 6
```

Sabitler tanımlarken let kullanılır.

Örneğin:

```
let pi: Float = 3.14
```

## Değişkenler İçin Ek Bilgiler

- Ondalıklı sayı tanımlandığında default olarak double tanımlanır

Örneğin:

```
var d = 5.6 // Türü double -- Float olmasını istersek başta türünü belirtmeliyiz.
```

- Swift Type Safety dildir. Eğer tür belirtilmezse başta eşitlenen değeri alacaktır. Buna Type Inference denir.

- Bir türü başka bir türe dönüştürürken muhakkak yeni değişken tanımlanmalı ve işlem yapabilmek için aynı türde olmalı.

```swift
let twoThousand: UInt16 = 2_000
let one: UInt8 = 1
let twoThousandAndOne = twoThousand + UInt16(one)
```


