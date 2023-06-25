## Closure

Swift'te closure'lar, bir kod bloğunu veya işlevi başka bir yerde kullanılabilen bir nesne olarak temsil eden özel bir yapıdır. Closure'lar, işlevsel programlama ve asenkron programlama gibi durumlarda oldukça kullanışlıdır. 

Türleri:

- Temel Closure:

```swift
let greet = {
    print("Merhaba, dünya!")
}
greet() // "Merhaba, dünya!" çıktısını verir
```

- Parametreli Closure:

```swift
let greet = { (name: String) in
    print("Merhaba, \(name)!")
}
greet("Swift") // "Merhaba, Swift!" çıktısını verir
```

- Dönüş Değeri Olan Closure:

```swift
let multiply = { (a: Int, b: Int) -> Int in
    return a * b
}
let result = multiply(5, 3) // 15
```

- Closure'ları Parametre Olarak Alan Fonksiyonlar:

```swift
func calculate(a: Int, b: Int, operation: (Int, Int) -> Int) {
    let result = operation(a, b)
    print("Sonuç: \(result)")
}

calculate(a: 10, b: 5, operation: { (a, b) in
    return a + b
}) // "Sonuç: 15" çıktısını verir

calculate(a: 8, b: 4, operation: { (a, b) in
    return a * b
}) // "Sonuç: 32" çıktısını verir
```

- Sıralama için örnek:

```swift
let numbers = [5, 2, 10, 1, 8]
let sortedNumbers = numbers.sorted { (a, b) in
    return a < b
}
print(sortedNumbers) // [1, 2, 5, 8, 10] çıktısını verir
```