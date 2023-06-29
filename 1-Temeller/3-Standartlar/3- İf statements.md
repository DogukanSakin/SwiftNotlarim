## If

Bir if bloğundan direkt olarak bir değer yakalayabiliriz. Burada değerlerin türleri aynı olmalıdır.

Örneğin:

```swift
let weatherAdvice = if temperatureInCelsius <= 0 {
    "It's very cold. Consider wearing a scarf."
} else if temperatureInCelsius >= 30 {
    "It's really warm. Don't forget to wear sunscreen."
} else {
    "It's not that cold. Wear a T-shirt."
}


print(weatherAdvice)
// Prints "It's not that cold. Wear a T-shirt."
```

## If Let Kullanımı

if let ifadesi, bir değerin nil olup olmadığını kontrol etmek ve değeri nil olmayan bir geçici sabite atamak için kullanılır. Bu, güvenli bir şekilde nil değerlerini ele almanın bir yoludur.

```swift
let optionalNumber: Int? = 42

if let number = optionalNumber {
    print("Optional number is not nil. Value is \(number)")
} else {
    print("Optional number is nil.")
}
```
