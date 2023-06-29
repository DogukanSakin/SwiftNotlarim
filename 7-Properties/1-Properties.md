## Properties

Swift programlama dilinde "properties" (özellikler), bir sınıf, yapı veya numaralandırma türünde değerlerin depolanması, erişilmesi ve ayarlanması için kullanılan öğelerdir. Properties, bir nesnenin durumunu veya özelliklerini temsil eder ve nesne tarafından taşınan verileri saklar.

Swift'te iki tür properties bulunur: "stored properties" (saklanan özellikler) ve "computed properties" (hesaplanan özellikler).

### Stored Properties

Stored properties, bir class'ın, struct veya enum türünün bir parçası olarak doğrudan bir değeri saklar. Bunlar bellekte ayrı bir alan işgal ederler ve özellikle değişken (var/let) olarak tanımlanır. Stored properties, class ve struct türleri için kullanılabilirken, enum türleri için yalnızca hesaplanan (computed) özellikler kullanılabilir.

```swift
struct Person {
    var name: String
    var age: Int
}

var person1 = Person(name: "John", age: 25)
print(person1.name) // John
print(person1.age) // 25

person1.name = "Jane"
print(person1.name) // Jane
```

Yukarıdaki örnekte, "Person" struct'ında "name" ve "age" adında iki stored property bulunmaktadır. Bu özellikler, struct'ın bir parçası olarak doğrudan bir değer saklar ve erişilebilir/ayarlanabilir.

### Lazy Stored Properties

"Lazy Stored Properties" (Geç Otomatikleştirilmiş Saklanan Özellikler), değerleri kullanıldığı anda hesaplanan ve sadece ilk erişim anında değer atanmış olan özelliklerdir. Bu özellikler, bellek kullanımını azaltmak ve performansı iyileştirmek için kullanışlıdır.

Bir lazy stored property, değerine ilk erişim yapıldığında hesaplanır ve sonraki erişimlerde aynı değeri döndürür. Bu özelliği kullanarak, değeri gerektiğinde hesaplanacak olan özelliklerin başlangıç değerlerini atamaktan kaçınabiliriz.

Lazy stored property'ler yalnızca değişken (var) özelliklerde kullanılabilir ve 'lazy' anahtar kelimesiyle tanımlanır. Ayrıca, sadece değer tipi olan (class değil) ve başlangıç değerine ihtiyaç duyan saklanan özelliklerde kullanılabilirler.

```swift
class ImageLoader {
    lazy var image: UIImage = self.loadImage()

    func loadImage() -> UIImage {
        // Burada görüntünün yüklenme işlemi gerçekleştirilir
        // Örnek olarak, bir dosyadan veya bir ağ isteğinden görüntü yüklenir
        return UIImage(named: "exampleImage")!
    }
}

let loader = ImageLoader()
// 'image' özelliğine ilk erişimde görüntü yüklenir
let loadedImage = loader.image
```

Yukarıdaki örnekte, "ImageLoader" adında bir sınıfımız var. Bu sınıfın "image" adında bir lazy stored property'si bulunmaktadır. İlk erişim anında, "image" özelliği "loadImage()" metodunu çağırarak görüntüyü yükler. Sonraki erişimlerde ise hesaplanan değer doğrudan döndürülür. Bu sayede, görüntüye ihtiyaç duyulmadığı durumlarda gereksiz yüklemelerden kaçınılabilir ve bellek kullanımı azaltılır.

Lazy stored property'lerin kullanımı, performansı artırmak ve kaynakları etkin kullanmak için faydalı olabilir, özellikle hesaplama maliyeti yüksek olan değerlere sahip özelliklerde veya başlangıç değerlerine zamanla ihtiyaç duyan durumlarda kullanılabilir.

## Computed Properties

Computed properties, gerçek değeri saklamak yerine her erişildiğinde hesaplanan bir değeri temsil eder. Computed properties, "get" ve opsiyonel olarak "set" bloklarını içeren bir yapıya sahiptir. Get bloğunda, hesaplanan değeri döndürürken set bloğunda ise yeni bir değer alır ve uygun eylemleri gerçekleştirir. Computed properties, herhangi bir tür için kullanılabilir.

```swift
struct Circle {
    var radius: Double

    var area: Double {
        get {
            return Double.pi * radius * radius
        }
        set(newArea) {
            radius = sqrt(newArea / Double.pi)
        }
    }
}

var circle = Circle(radius: 5.0)
print(circle.area) // 78.53981633974483

circle.area = 100.0
print(circle.radius) // 5.641895835477563
```


Properties, Swift programlama dilinde nesnelerin durumunu temsil etmek için önemli bir araçtır. Stored properties, verileri doğrudan saklar ve computed properties, değerleri dinamik olarak hesaplayabilir. Bu sayede nesnelerin davranışlarını ve özelliklerini daha esnek bir şekilde yönetebiliriz.

## Read-Only Computed Properties

Computed properties, sadece okunabilir (read-only) olarak da tanımlanabilir. Bu durumda, sadece get bloğu bulunur ve set bloğu bulunmaz. Read-only computed properties, sadece get bloğu bulunan computed properties'lerdir.

```swift
struct Circle {
    var radius: Double

    var area: Double {
        return Double.pi * radius * radius
    }
}

var circle = Circle(radius: 5.0)

print(circle.area) // 78.53981633974483
```





