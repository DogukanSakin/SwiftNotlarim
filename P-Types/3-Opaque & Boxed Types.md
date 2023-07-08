## Opaque & Boxed Types

Swift implemente detaylarını gizlemek için iki yol sunar. Opauqe ve boxed types. 

## Opaque Types

Opaque types, bir değeri veya dönüş değerini belirli bir tür yerine soyut bir tür olarak kullanmanızı sağlar. Bu, bir fonksiyonun iç mantığını gizleyerek kodunun daha basit ve anlaşılır olmasını sağlar. Gizli türler, aşağıdaki durumlarda kullanışlı olabilir:

- İç mantığı gizlenen bir veri yapısı döndürmek istediğinizde.
- Bir API'nin dış dünyaya sadece belirli bir türle etkileşimde bulunmasını sağlamak istediğinizde.
- Protokollerin karmaşık ilişkilerini gizlemek ve yalnızca sonucunu kullanıcılara sunmak istediğinizde.

```swift
struct Square: Shape {
    var size: Int
    func draw() -> String {
        let line = String(repeating: "*", count: size)
        let result = Array<String>(repeating: line, count: size)
        return result.joined(separator: "\n")
    }
}


func makeTrapezoid() -> some Shape {
    let top = Triangle(size: 2)
    let middle = Square(size: 2)
    let bottom = FlippedShape(shape: top)
    let trapezoid = JoinedShape(
        top: top,
        bottom: JoinedShape(top: middle, bottom: bottom)
    )
    return trapezoid
}
let trapezoid = makeTrapezoid()
print(trapezoid.draw())
```

Yukarıdaki örnekte makeTrapezoid() fonksiyonu, Shape protokolünü uygulayan bir tür döndürür. Ancak, fonksiyonun içindeki karmaşık mantığı gizlemek için, fonksiyonun dönüş değerini some Shape olarak belirtiriz. Bu, fonksiyonun dış dünyaya sadece Shape protokolünü uygulayan bir tür döndürdüğünü söyler. Bu, fonksiyonun iç mantığını gizler ve kodun daha basit ve anlaşılır olmasını sağlar.


## Boxed Types

Boxed Types,  karmaşık veya değerlerini saklamak istediğiniz bir türü daha basit bir kap içine koyarak kullanmanızı sağlar. Bu, daha basit bir arayüz veya soyutlama kullanmanızı ve karmaşık detayları gizlemenizi sağlar. Boxed Types, aşağıdaki durumlarda kullanışlı olabilir:

- Bellek yönetimini gizlemek ve sızıntıları önlemek istediğinizde.
- Dış dünya için basit bir arayüz sağlamak istediğinizde.
- İçerideki karmaşık yapının değişebilirliğini sağlamak istediğinizde.

```swift
struct VerticalShapes: Shape {
    var shapes: [any Shape]
    func draw() -> String {
        return shapes.map { $0.draw() }.joined(separator: "\n\n")
    }
}


let largeTriangle = Triangle(size: 5)
let largeSquare = Square(size: 5)
let vertical = VerticalShapes(shapes: [largeTriangle, largeSquare])
print(vertical.draw())
```

Yukaridaki örnekte VerticalShapes struct'ı [any Shape] yani Shape'i uygulayan herhangi bir türü tutan bir array içerir. Bu, VerticalShapes struct'ının dış dünyaya sadece Shape protokolünü uygulayan bir türü tuttuğunu söyler. Bu, VerticalShapes struct'ının iç mantığını gizler ve kodun daha basit ve anlaşılır olmasını sağlar.

## Opaque Types vs. Boxed Types

- Saklama Mekanizması: Boxed Types, değeri içinde saklayarak karmaşık veya farklı türlerin basit bir arayüz sağlar. Değerin kendisi box'ın içinde saklanır. Opaque Types ise değeri gizler ve soyut bir tür olarak kullanır. Değerin kendisi belirsizdir ve iç detayları gizlenmiştir.

- Tür İlişkisi: Boxed Types, değerlerini sakladıkları türlerin hiyerarşisini veya ilişkisini korur. Örneğin, bir BoxedAnimal türü, Animal sınıfının alt sınıflarını saklayabilir. Opaque Types ise tür ilişkisini gizler ve kullanıcıya sadece belirli bir arayüzü sunar. Bu sayede, arka planda farklı türlerin kullanılmasına izin verilir ve kullanıcıya sadece sonuç sunulur.

- Genel Kullanım Amaçları: Boxed Types, karmaşık yapılara veya farklı türlerin bir arada saklanması gereken durumlarda kullanılır. Değerleri box'a yerleştirerek, basit bir arayüz sağlar ve değerlerin kontrolünü kolaylaştırır. Opaque Types ise soyutlama sağlamak veya gizli bir yapıyı basitleştirmek için kullanılır. Değerleri gizleyerek, karmaşık yapıların detaylarını saklar ve kullanıcıya sadece sonucu sunar.

- Çalışma Zamanı Davranışı: Boxed Types, değerleri box'a yerleştirerek bellekte ayrı bir alan oluşturur ve referans semantiğiyle çalışır. Opaque Types ise değerleri gizler ve bazen daha fazla bellek kullanmadan optimize edilmiş çalışma zamanı davranışı sağlar. Bu, değerlerin kullanıldığı yerde doğrudan erişim sağlanmasına olanak tanır.

Özetle, Boxed Types, farklı türleri bir arada saklamak ve kontrol etmek için kullanılırken, Opaque Types, soyutlama sağlamak ve değerlerin gizlenmesini sağlamak için kullanılır. Boxed Types, değerlerin saklandığı bir box olarak düşünülebilirken, Opaque Types, değerlerin soyut bir arayüz olarak kullanılmasını temsil eder.