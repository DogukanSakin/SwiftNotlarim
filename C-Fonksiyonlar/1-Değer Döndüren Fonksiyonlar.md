## Geri Değer Döndüren Fonksiyonlar

Fonksiyonlar geri değer döndürebilir. Bir fonksiyonun geri döndürdüğü değer fonksiyonun sonundaki `->` işaretinden sonra yazılır. 

```swift
func topla(a: Int, b: Int) -> Int {
    return a + b
}
```

Bir fonksiyonun geri dönüş değeri tanımlanmasa bile bir değer döndürür. Bu değer `Void` olarak adlandırılır. `Void` aslında bir `Tuple`'dır. 

```swift
func topla(a: Int, b: Int) {
    print(a + b)
}
```

Eğer fonksiyon tek satırdan oluşuyorsa fonksiyonun sonundaki `->` işaretinden sonra yazılan değer tanımlanmasa bile otomatik olarak fonksiyonun tek satırı geri dönüş değeri olarak kabul edilir. 

```swift
func topla(a: Int, b: Int) -> Int {
    a + b
}
```

Bu fonksiyon return ile yazılırsa da iki fonksiyon aynı işi yapar:

```swift
func topla(a: Int, b: Int) -> Int {
    return a + b
}
```



## Birden Fazla Değer Döndürme (Touples)

Bir fonksiyon birden fazla değer döndürebilir. Bunun için fonksiyonun geri dönüş değeri `Tuple` olarak tanımlanır. 

```swift
func minMax(array: [Int]) -> (min: Int, max: Int) {
    var currentMin = array[0]
    var currentMax = array[0]
    for value in array[1..<array.count] {
        if value < currentMin {
            currentMin = value
        } else if value > currentMax {
            currentMax = value
        }
    }
    return (currentMin, currentMax)
}
```

Buradan değerleri almak için ise fonksiyonun çağırıldığı yerde `Tuple`'ın elemanlarına erişilir. 

```swift
let bounds = minMax(array: [8, -6, 2, 109, 3, 71])
print("min is \(bounds.min) and max is \(bounds.max)")
// Prints "min is -6 and max is 109"
```

## Opsiyonel Değer Döndürme

Bir fonksiyonun geri dönüş değeri opsiyonel olabilir. Bu durumda fonksiyonun geri dönüş değeri `?` ile tanımlanır. 

```swift
func sayiBul(array: [Int], sayi: Int) -> Int? {
    for (index, value) in array.enumerated() {
        if value == sayi {
            return index
        }
    }
    return nil
}
```

## implicit return

```swift
func divide(_ a: Int, by b: Int) -> Int {
    if b == 0 {
        fatalError("Division by zero is not allowed.")
    }
    
    return a / b
}
```

Bu örnekte, divide(_:_:) adlı bir fonksiyon tanımlanmıştır. Eğer b değeri sıfıra eşitse, fatalError fonksiyonu çağrılarak bir hata durumu oluşturulur ve program sonlandırılır. Bu hata durumu, bir değer döndürmeyen bir fonksiyon olduğu için implicit return olarak kullanılabilir. Bunun sebebi, Swift'in bu noktada bir değer döndürülmeyeceğini bilmesidir.

Ancak, print(13) gibi bir ifadeyi implicit return olarak kullanamazsınız çünkü print fonksiyonu bir değer döndürmez. implicit return ile kullanılabilecek bir ifade, bir değer döndüren bir fonksiyon olmalıdır.




