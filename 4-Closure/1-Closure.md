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

## Çağırımlar

İki farklı türde çağırım vardır:

```swift
// Here's how you call this function without using a trailing closure:


someFunctionThatTakesAClosure(closure: {
    // closure's body goes here
})


// Here's how you call this function with a trailing closure instead:


someFunctionThatTakesAClosure() {
    // trailing closure's body goes here
}
```

## Notlar 

Closure'ların parametresi inout alabilir ama default değer almazlar.

Parantezlere gerek kalmadan Closure tek satırda yazılabilir ve return kullanmaya da gerek yoktur:

```swift
reversedNames = names.sorted(by: { s1, s2 in s1 > s2 } )
```

Parametrelere isim verilmeden de kullanılabilir.

```swift
reversedNames = names.sorted(by: { $0 > $1 } )
```

Hiçbir parametre verilmeden sıralama yapılabilir:

```swift
reversedNames = names.sorted(by: >)
```

Closure tarafından değiştirilmeyen bir değişken varsa Swift bellek yönetimi için değişkeni elden çıkarır.

Closure'lar referans tiplidir:

```swift
var incrementByTwo: () -> Int = {
    var count = 0
    let incrementClosure: () -> Int = {
        count += 2
        return count
    }
    return incrementClosure
}

var firstClosure = incrementByTwo()
print(firstClosure()) // Çıktı: 2

var secondClosure = firstClosure
print(secondClosure()) // Çıktı: 4

print(firstClosure()) // Çıktı: 6
```

## Escaping

@escaping anahtar kelimesi, closure'ın belirli bir süre boyunca yaşaması gerektiğini ve fonksiyonun dışında çağrılabileceğini ifade eder. Bu, genellikle asenkron operasyonlarda veya bir fonksiyonun içinde başlatılan işlemlerin tamamlandığında geri çağırma yapmak için kullanılır.

```swift
func doSomething(completion: @escaping () -> Void) {
    DispatchQueue.main.asyncAfter(deadline: .now() + 1) {
        completion()
    }
}

doSomething {
    print("Tamamlandı!")
}
```


## Autoclosure

Swift'te "Autoclosures" (otomatik kapanan closure'lar) adı verilen bir özellik vardır. Autoclosures, bir işlev veya ifade içinde gecikmiş değerlendirme sağlar. Bu, bir değeri kapatmak ve o değerin sadece ihtiyaç duyulduğunda hesaplanmasını sağlamak için kullanışlıdır. Autoclosures, genellikle argüman olarak alınacak bir closure için kısa ve kullanımı kolay bir sözdizini sağlar. Autoclosures, genellikle geçici olarak değerlendirilmemesi gereken ifadeleri geciktirmek veya değerlendirmek için kullanılır. Bu sayede, gerektiğinde performans ve hafıza optimizasyonu sağlanabilir.

```swift
var names = ["Ahmet", "Mehmet", "Ayşe", "Fatma"]

let closureExample: () -> String = {
    return names.remove(at: 0)
}

let removedName = closureExample()
print(names) // ["Mehmet", "Ayşe", "Fatma"]
print(removedName) // "Ahmet"
```

@aoutoclosure anahtar kelimesi, closure'ın otomatik olarak kapanmasını sağlar. Bu sayede closure'ın çağrıldığı yerde değerlendirilmesi sağlanır.

```swift
var numbers = [1, 2, 3, 4, 5]

func processNextNumber(_ closure: @autoclosure () -> Int) {
    let nextNumber = closure()
    print("Sonraki sayı: \(nextNumber)")
}

processNextNumber(numbers.remove(at: 0))
print(numbers) // [2, 3, 4, 5]
```

