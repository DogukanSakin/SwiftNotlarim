## Integer

Swift 8, 16, 32 ve 64 bitlik int tanımlamalarına izin verir.

Burada bitlik tanımlamalar işaretli ve işaretsiz olarak ikiye ayrılır.

İşaretliler için doğrudan Int8, Int32 gibi tanımlamalar kullanılır.

Örneğin Int8 için:

```swift
let myInt : Int8 = 120 --> bu değişkenin değer aralığı -128 ile 127 arasındadır yani negatif değer alabilir
```

```swift
let myInt : UInt8 = 120 -> bu değişken ise negatif değer alamaz. Aralığı 0 ile 255'tir
```

Yazılacak kod bu tarzda minik bit ayarlamaları ve işaretli/işaretsiz ayarlamalarına ihtiyaç duymuyorsa sayının negatif olunacağı bilinse bile Int kullanılmalı.

## Sınırlar (Max-Min)

Integer'da değişken tanımlamasından sonra değer aralığının max ve minini her zaman alabiliriz.

Örneğin:

```swift
let myInt = Int8.max -> Int8'nin max değeri atanır.
```
