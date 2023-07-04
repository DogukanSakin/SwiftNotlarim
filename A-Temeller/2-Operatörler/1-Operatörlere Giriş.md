## Operatörlere Giriş

Operatörler üç grupta incelenir:

- Unary
- Binary
- Ternary

## Unary

Unary operatör, yalnızca bir operand üzerinde işlem yapar. Bu tür operatörler, operandın önünde veya arkasında yer alabilir.

Örneğin:

- Bir sayının işaretini değiştiren - operatörü: -5
- Bir bool değerini tersine çeviren ! operatörü: !true

## Binary

Binary operatör, iki operand üzerinde işlem yapar. Bu operatörlerin her biri, iki operandı arasında yer alır. 

Örneğin:

- İki sayıyı toplayan + operatörü: 2 + 3
- İki sayıyı çarpan * operatörü: 4 * 5
- İki stringi birleştiren + operatörü: "Hello, " + "World"

## Ternary

Ternary operatör, üç operand üzerinde işlem yapar ve bir koşula dayanarak sonuç üretir. 

```swift
let sayı = 10
let sonuç = sayı > 5 ? "Büyük" : "Küçük"
```


## Atama Operatörü (=)

Birden fazla değer aynı anda atanabilir.

Örneğin:

```swift
let (x, y) = (1, 2)
```

## ?? Opearatörü (Nil-Coalescing)

Nil-Coalescing operatörü, nil olmayan bir değer döndürür. Eğer değer nil ise, varsayılan değeri döndürür.

```swift
let defaultColorName = "red"
var userDefinedColorName: String? // default değeri nil
var colorNameToUse = userDefinedColorName ?? defaultColorName
```

## Range Operatörü: Closed Range (a...b)

Closed Range operatörü, a'dan b'ye kadar olan tüm değerleri içerir.

```swift
for index in 1...5 {
    print("\(index) times 5 is \(index * 5)")
}
```

## Range Operatörü: Half-Open Range (a..<b)

Half-Open Range operatörü, a'dan b'ye kadar olan tüm değerleri içerir. Ancak b değerini içermez.

```swift
let names = ["Anna", "Alex", "Brian", "Jack"]
let count = names.count
for i in 0..<count {
    print("Person \(i + 1) is called \(names[i])")
}
```

## Range Operatörü: One-Sided (a...) ve (...a)

One-Sided Range operatörü, a'dan sonraki tüm değerleri içerir. 

```swift
let names = ["Anna", "Alex", "Brian", "Jack"]
for name in names[2...] {
    print(name)
}
```

One-Sided Range operatörü, a'ya kadar olan tüm değerleri içerir.

```swift
let names = ["Anna", "Alex", "Brian", "Jack"]
for name in names[...2] {
    print(name)
}
```



