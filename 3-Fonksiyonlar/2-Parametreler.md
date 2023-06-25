## Parametre Label'ları

Swift'te kod okunabilirliğini artırmak amacıyla argümanlara label olarak etiket eklenebilir:

```swift
func greet(person: String, from hometown: String) -> String {
    return "Hello \(person)!  Glad you could visit from \(hometown)."
}
print(greet(person: "Bill", from: "Cupertino"))
// Prints "Hello Bill!  Glad you could visit from Cupertino."
```

## Parametreler için _

Fonksiyonu çağırırken parametre isimlerini yazmak istemiyorsak parametre isimlerinin önüne _ koyabiliriz:

```swift
func someFunction(_ firstParameterName: Int, secondParameterName: Int) {
    // In the function body, firstParameterName and secondParameterName
    // refer to the argument values for the first and second parameters.
}
someFunction(1, secondParameterName: 2)
```

## Değişken Parametreler

Bir fonksiyonun parametrelerinin sayısı belli değilse değişken parametreler kullanılabilir. Bunun için parametre tipinin önüne `...` konur:

```swift
func arithmeticMean(_ numbers: Double...) -> Double {
    var total: Double = 0
    for number in numbers {
        total += number
    }
    return total / Double(numbers.count)
}
arithmeticMean(1, 2, 3, 4, 5)
// returns 3.0, which is the arithmetic mean of these five numbers
arithmeticMean(3, 8.25, 18.75)
// returns 10.0, which is the arithmetic mean of these three numbers
```

## inout parametreler

Bir fonksiyonun parametreleri varsayılan olarak sabit değerlerdir. Yani fonksiyon içinde bu parametrelerin değerleri değiştirilemez. Eğer bir fonksiyonun parametresinin değerini değiştirmek istiyorsak bu parametreyi `inout` olarak tanımlamalıyız. 

```swift
func swapTwoInts(_ a: inout Int, _ b: inout Int) {
    let temporaryA = a
    a = b
    b = temporaryA
}
```

```swift
func doubleInPlace(number: inout Int) {
    number *= 2
}

var myNumber = 5
doubleInPlace(number: &myNumber)
print(myNumber) // Çıktı: 10
```

Bu örnekte, doubleInPlace(number:) adlı bir fonksiyon tanımlanmıştır. Bu fonksiyon, bir inout parametre olan number'ı alır ve değerini iki katına çıkarır. Fonksiyonu çağırmadan önce myNumber değişkenini & operatörü ile geçerek, referansını fonksiyona iletmeliyiz. Sonuç olarak, myNumber'ın değeri fonksiyon içinde değiştirilir ve print işlemiyle 10 çıktısı alınır. 

- inout parametreleri, değiştirilebilir (var) değişkenlere ve bellekte geçici bir alana ihtiyaç duyabilir.
- inout parametreleri, fonksiyon çağrıldığında değiştirilmelidir. Bu nedenle, let ile tanımlanan sabitler inout parametre olarak kullanılamaz.
- inout parametrelerinin varsayılan değeri olamaz.
