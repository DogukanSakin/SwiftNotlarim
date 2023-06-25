## Function Types

Swift'te "function types" (fonksiyon tipleri), fonksiyonları ve metotları bir veri türü olarak temsil eden bir özelliktir. Fonksiyon tipleri, bir fonksiyonu veya metodu bir değişkene veya sabite atayabilmenizi, başka bir fonksiyonun parametre olarak alabilmenizi veya bir fonksiyonun sonucu olarak döndürebilmenizi sağlar.

Bir fonksiyon tipini tanımlamak için, fonksiyonun giriş parametrelerinin tipleri ve dönüş değerinin tipi kullanılır. 

```swift
func addNumbers(_ a: Int, _ b: Int) -> Int {
    return a + b
}

var mathOperation: (Int, Int) -> Int = addNumbers
```

## Kullanım Alanları

Bir fonksiyonu başka bir fonksiyona parametre olarak gönderirken:

```swift
func calculate(_ operation: (Int, Int) -> Int, _ a: Int, _ b: Int) -> Int {
    return operation(a, b)
}

func multiply(_ a: Int, _ b: Int) -> Int {
    return a * b
}

let result = calculate(multiply, 5, 3)
print(result) // Çıktı: 15
```


Fonksiyon tiplerini bir fonksiyon içinde geri dönüş değeri olarak kullanabiliriz:

```swift
func calculator(_ operation: String) -> (Double, Double) -> Double {
    switch operation {
    case "+":
        return { a, b in a + b }
    case "-":
        return { a, b in a - b }
    case "*":
        return { a, b in a * b }
    case "/":
        return { a, b in a / b }
    default:
        fatalError("Invalid operation")
    }
}

let addition = calculator("+")
let result = addition(3.5, 2.5)
print(result) // Çıktı: 6.0

let multiplication = calculator("*")
let result2 = multiplication(4.0, 2.0)
print(result2) // Çıktı: 8.0
```