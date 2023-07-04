## Failable Initializers

Failable initializer'lar, başlatma işlemi sırasında bir başarısızlık durumunu temsil etmek için kullanılır. Başarısızlık durumu, nil değeri döndürerek veya nil döndürülebilen bir opsiyonel değer döndürerek ifade edilir. Failable initializer'lar, belirli bir koşulu sağlamayan durumlarda nesne oluşturma girişimlerini başarısızlığa uğratabilir. Bu durumlar, verilen parametrelere veya diğer koşullara bağlı olarak oluşabilir. Failable initializer'lar, sınıf, yapıcı veya enum türleri için tanımlanabilir.

Failable initializer'ların kullanılması için init? ifadesi kullanılır:

```swift
struct Temperature {
    var celsius: Double
    
    init?(celsius: Double) {
        if celsius < -273.15 { //  sıfırın altında sıcaklık yok
            return nil
        }
        self.celsius = celsius
    }
}

let temperature = Temperature(celsius: -300.0)

if temperature == nil {
    print("sıfırın altında sıcaklık yok")
}
```

Aynı parametre türlerine ve isimlere sahip bir normal bir failiable initializer oluşturamayız.

Benzer şekilde Failable initializer'lar, belirli bir raw değeri temsil eden enum'ları oluştururken başarısızlık durumunu temsil etmek için kullanılır. Eğer belirli bir raw değere sahip bir enum oluşturulamazsa, failable initializer nil döndürür.

```swift
enum Direction: String {
    case north = "N"
    case south = "S"
    case east = "E"
    case west = "W"

    init?(rawValue: String) {
        switch rawValue {
        case "N":
            self = .north
        case "S":
            self = .south
        case "E":
            self = .east
        case "W":
            self = .west
        default:
            return nil
        }
    }
}
```

## Failable Initializer'ların Yayılması / Paylaşımı

Bir başlatıcı başarısız olduğunda, bu başarısızlık durumunun üst sınıflara, alt sınıflara veya aynı sınıfın diğer başlatıcılarına yayılabilir.

```swift
class Vehicle {
    var numberOfWheels: Int
    
    init?(numberOfWheels: Int) {
        if numberOfWheels < 0 {
            return nil
        }
        self.numberOfWheels = numberOfWheels
    }
}

class Car: Vehicle {
    var brand: String
    
    init?(brand: String, numberOfWheels: Int) {
        self.brand = brand
        super.init(numberOfWheels: numberOfWheels)
        
        if brand.isEmpty {
            return nil
        }
    }
}
```

Car sınıfı, üst sınıf olan Vehicle'ın failable initializer'ını çağırır ve kendi başarısızlık durumunu kontrol eder. Eğer brand parametresi boş bir dize ise, başlatma işlemi başarısız olur ve nil döndürülür.

Bu durumda, başarısızlık durumu (nil) alt sınıftan üst sınıfa otomatik olarak yayılır. Yani, Car sınıfından oluşturulan bir nesne, brand parametresi boş bir dize veya negatif bir numberOfWheels değeri içeriyorsa, başlatma işlemi başarısız olur ve nil döndürülür.

## Override 

Failable initializer'larda override edilebilir.

```swift
class Document {
    var name: String?
    // this initializer creates a document with a nil name value
    init() {}
    // this initializer creates a document with a nonempty name value
    init?(name: String) {
        if name.isEmpty { return nil }
        self.name = name
    }
}

class AutomaticallyNamedDocument: Document {
    override init() {
        super.init()
        self.name = "[Untitled]"
    }
    override init(name: String) {
        super.init()
        if name.isEmpty {
            self.name = "[Untitled]"
        } else {
            self.name = name
        }
    }
}
```

init? 'e alternatif olarak init! kullanılabilir. init! kullanıldığında, başlatma işlemi başarısız olursa, program çöker.

```swift
class Document {
    var name: String?
    // this initializer creates a document with a nil name value
    init() {}
    // this initializer creates a document with a nonempty name value
    init!(name: String) {
        if name.isEmpty { return nil }
        self.name = name
    }
}

let document = Document(name: "")
```
