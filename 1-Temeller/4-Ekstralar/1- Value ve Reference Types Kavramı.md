## Value Types

- Değer tipli veriler, değerleri doğrudan depolarlar ve bellekte ayrı alanlarda saklanırlar.
- Bir değer tipi değişkeni bir başka değişkene veya sabite atanırken, değerler kopyalanır. Yani, orijinal değişkenin değeri bağımsız olarak kopyalanır ve iki değişkenin bellekte ayrı kopyaları bulunur.
- Değer tipli veriler, sabitlendikten sonra değiştirilemez. Bir değer tipi değişkeni kopyalayarak elde edilen yeni değişken, orijinal veriden bağımsız olarak hareket eder.
- Swift dilindeki temel değer tipleri arasında sayılar (Int, Float, Double), karakterler (Character), bool (Bool) ve yapılar (struct) yer alır.

Örnek:

```swift
var a = 5
var b = a // b, a'nın değerini kopyalar

b = 10 // b'yi değiştirir, a etkilenmez
print(a) // Çıktı: 5
print(b) // Çıktı: 10
```

## Reference Types

- Referans tipli veriler, bellekte bir referans (adres) tutarlar ve verinin değeri bu referans aracılığıyla erişilir.
- Bir referans tipli veri atandığında, asıl veri bellekte paylaşılır ve kopyalanmaz. Yani, iki referans aynı veriyi işaret eder ve verinin değişiklikleri tüm referanslara yansır.
- Referans tipli veriler, değerleri değiştirilebilir. Bir referansın üzerinde yapılan değişiklikler, tüm referansları etkiler.
- Swift dilindeki temel referans tipleri arasında sınıflar (class), fonksiyonlar (function) ve kimi özel durumlar (örneğin, array ve touple) yer alır.

Örnek:
```swift
class Person {
    var name: String
    
    init(name: String) {
        self.name = name
    }
}

var person1 = Person(name: "Ahmet")
var person2 = person1 // person2, person1'in referansını kopyalar

person2.name = "Mehmet" // person2'yi değiştirir, person1 etkilenir
print(person1.name) // Çıktı: "Mehmet"
print(person2.name) // Çıktı: "Mehmet"
```

Değer tipli ve referans tipli veriler arasındaki farklar, verilerin bellekte nasıl temsil edildiği, atama işlemlerinin nasıl gerçekleştiği ve değişikliklerin nasıl yayıldığı gibi konuları içerir. Bu farklılıklar, programlamada bellek kullanımı, performans ve veri yönetimi açısından önemlidir.