## Subscripts

Subscript'ler class, struct ve enum'ların bir özelliğidir ve temel olarak bir instance'ı array veya touple gibi bir yapıya benzetmek için kullanılırlar.

```swift
struct MyStruct {
    subscript(index: Int) -> Int {
        // Burada, index parametresiyle gelen indeksin değerini döndüren bir get bloğu bulunur
        get {
            // İndeksi kullanarak, istenen değeri döndürme
            // Örnek olarak, bir diziyi temsil ediyor olabilir
            // Bu durumda, diziye erişmek için index parametresini kullanarak ilgili elemanı döndürebilirsiniz.
        }

        // Bir set bloğu da tanımlayabilirsiniz
        set(newValue) {
            // İndeksi kullanarak, ilgili değeri yeni değerle değiştirme
            // Örnek olarak, bir diziyi temsil ediyor olabilir ve yeni değeri, index parametresi ile belirtilen indeksteki elemana atayabilirsiniz.
        }
    }
}
```

Instance method'larının aksine subscript'ler okunabilir ve yazılabilir olabilirler. Bu yüzden, get ve set bloklarını tanımlamak zorunda değilsiniz. Sadece get bloğu tanımlayarak, subscript'in sadece okunabilir olmasını sağlayabilirsiniz. Aynı şekilde, sadece set bloğu tanımlayarak, subscript'in sadece yazılabilir olmasını sağlayabilirsiniz.

Daha önce willSet'te gördüğümüz gibi burada da parametre ismi belirtilmezse default olarak newValue kullanılır.

Ayrıca getter veya setter yazılmazsa bir subscript default olarak getter olur.
Yani sadece read-only bir subscript yazmak istiyorsanız getter yazmanıza gerek yoktur.

```swift
subscript(index: Int) -> Int {
    // Return an appropriate subscript value here.
}
```

## Type Subscripts

Type Subscript'ler, bir type'ın instance'larına değil, type'ın kendisine ait olan subscript'lerdir. Type Subscript'ler, static keyword'ü ile tanımlanırlar.

```swift
enum Planet: Int {
    case mercury = 1, venus, earth, mars, jupiter, saturn, uranus, neptune
    static subscript(n: Int) -> Planet {
        return Planet(rawValue: n)!
    }
}
let mars = Planet[4]
print(mars)
```


