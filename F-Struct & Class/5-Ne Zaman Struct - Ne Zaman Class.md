## Ne Zaman Struct - Ne Zaman Class

Swift programlama dilinde, class ve struct yapıları benzer işlevlere sahip olsalar da bazı farklılıklara sahiptir. Genel olarak, aşağıdaki durumlarda class veya struct kullanımını tercih edebilirsiniz:

Referans Semantiği: Eğer nesnenin referans semantiği taşıması gerekiyorsa, yani bir örneğin farklı yerlerde kullanılan aynı verilere ihtiyaç duyuluyorsa, class kullanılması uygun olabilir. Örneğin, bir kullanıcı nesnesini temsil etmek için bir sınıf kullanabiliriz:

```swift
class User {
    var name: String
    var age: Int

    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }
    
}
```

alıtım: Eğer kalıtım yapısı kullanmanız gerekiyorsa, class kullanılması gerekebilir. Sınıflar, başka bir sınıftan özellikleri ve davranışları devralabilir. Örneğin:

```swift
class Vehicle {
    var brand: String

    init(brand: String) {
        self.brand = brand
    }

    func startEngine() {
        print("Engine started.")
    }
}

class Car: Vehicle {
    var numberOfWheels: Int

    init(brand: String, numberOfWheels: Int) {
        self.numberOfWheels = numberOfWheels
        super.init(brand: brand)
    }

    override func startEngine() {
        print("Car engine started.")
    }
}
```

Değer Semantiği: Eğer nesnenin değer semantiği taşıması yeterliyse, yani bir örneğin kopyalanması yerine yeni bir örnek oluşturulmasını tercih ediyorsanız, struct kullanabilirsiniz. Örneğin, bir dikdörtgenin boyutunu temsil etmek için bir yapı kullanabiliriz:

```swift
struct Rectangle {
    var width: Double
    var height: Double

    func calculateArea() -> Double {
        return width * height
    }
}
```

Değişmezlik (Immutability): Eğer bir nesnenin değişmez olması gerekiyorsa, yani içindeki verilerin değişmemesi gerekiyorsa, struct kullanabiliriz. Bu, değeri değiştirememe garantisi sağlayarak yan etkileri azaltabilir. Örneğin:

```swift
struct Point {
    let x: Int
    let y: Int
}
```


