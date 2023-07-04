## Methods

Swift'te methodlar, bir sınıf, yapıcı (initializer) veya bir tipin içindeki işlevleri ifade eden kod bloklarıdır. Methodlar, belirli bir nesne türünün davranışını tanımlar ve bu nesneler üzerinde çalışabilen işlemleri gerçekleştirir. 

Methodlar ile fonksiyonlar arasındaki temel farklar:

- İlişkili Nesne: Methodlar, bir sınıf, yapı veya enum gibi bir türün bir parçasıdır ve bu türe ait özelliklere ve diğer methodlara erişebilir. Fonksiyonlar ise bağımsız olarak tanımlanır ve herhangi bir türe ait olmadan çalışabilir.


- Self Referansı: Methodlar, ilgili türe ait özelliklere ve methodlara erişmek için self kelimesini kullanabilir. Bu şekilde, method içindeki diğer özelliklere ve methodlara erişebilir ve onları değiştirebilir. Fonksiyonlar ise bağımsız olduğundan, bir self referansına sahip değillerdir.

- Çağırma Sözdizimi: Methodlar, ilgili türün bir örneği üzerinden çağrılır. Örneğin, myObject.myMethod() şeklinde bir çağırma sözdizimi kullanılır. Fonksiyonlar ise doğrudan adlarıyla çağrılabilir, örneğin myFunction() şeklinde bir çağırma sözdizimi kullanılır.

- Genişletilebilirlik: Methodlar, ilgili türlerin genişletilmelerine izin veren bir yapıya sahiptir. Yani, bir türe ait olan methodları daha sonra uzatabilir veya yenilerini ekleyebilirsiniz. Fonksiyonlar ise doğrudan genişletilemezler.

Methodlar temelde iki kategoriye ayrılır:

## Instance Methods

Instance Methodlar: Bir sınıf, yapıcı veya bir yapı (struct) içinde tanımlanan methodlardır. Bunlar, belirli bir nesneye ait davranışları ifade eder. Instance methodları kullanabilmek için ilgili yapıdan bir instance oluşturmamız gerekir.

```swift
class Counter {
    var count = 0
    
    func increment() {
        count += 1
    }
    
    func reset() {
        count = 0
    }
}

let counter = Counter()
counter.increment()
print(counter.count) // Çıktı: 1
counter.reset()
print(counter.count) // Çıktı: 0
```
## Value Type'larının Instance Metodlarıyla Modifiye Edilmesi

Value type'larının instance metodlarıyla modifiye edilmesi için metodun mutating olarak tanımlanması gerekir. Bu sayede value type'ın instance metodları içerisindeki özellikler değiştirilebilir.

```swift
struct Point {
    var x = 0.0, y = 0.0
    
    mutating func moveBy(x deltaX: Double, y deltaY: Double) {
        x += deltaX
        y += deltaY
    }
}

var somePoint = Point(x: 1.0, y: 1.0)
somePoint.moveBy(x: 2.0, y: 3.0)
print("The point is now at (\(somePoint.x), \(somePoint.y))")
// Prints "The point is now at (3.0, 4.0)"
```

Bu örnekte değişkenlerimiz value type olduğu için, metodumuzun mutating olarak tanımlanması gerekiyor. Aksi takdirde metodumuz içerisindeki değişiklikler, değişkenin değerini değiştirmeyecektir.

## Mutating'in Self ile Kullanımı

Mutating metodlar, self ile kullanıldığında, self'in yeni bir instance'ı ile değiştirilmesini sağlar. Örneğin, Point struct'ımızı kullanarak bir metod tanımlayalım:

```swift
struct Point {
    var x = 0.0, y = 0.0
    
    mutating func moveBy(x deltaX: Double, y deltaY: Double) {
        self = Point(x: x + deltaX, y: y + deltaY)
    }
}
```
Burada self, yeni bir Point instance'ı ile değiştirilir. Point struct'ının bir instance'ı üzerinde çağrıldığında, bu instance'ın yeni bir kopyası oluşturulur ve bu kopya üzerinde değişiklikler yapılır. 

Enumaration'lar için de aynı durum geçerlidir. 

```swift
enum TriStateSwitch {
    case off, low, high
    mutating func next() {
        switch self {
        case .off:
            self = .low
        case .low:
            self = .high
        case .high:
            self = .off
        }
    }
}
var ovenLight = TriStateSwitch.low
ovenLight.next()
// ovenLight is now equal to .high
ovenLight.next()
// ovenLight is now equal to .off
```

## Type Methods

Type Methods, bir sınıf, yapıcı (initializer) veya bir enum tipine ait olan ve doğrudan tipe ait olan metodlardır. Bunlar, bir türün genel davranışını ifade eder ve örneklendirilmiş bir nesne üzerinden değil, tipe doğrudan erişilerek çağrılırlar.

Type Methods, aşağıdaki özelliklere sahiptir:

"static" veya "class" Anahtar Kelimeleri: Bir Type Method'u tanımlamak için "static" veya "class" anahtar kelimelerinden birini kullanırız. Hangi anahtar kelimenin kullanılacağı, türe bağlı olarak farklılık gösterebilir.

static: final olarak işaretlenmiş sınıflar, yapılar ve enumlar için kullanılır. Bu tip türlerdeki metodlar alt sınıflar tarafından yeniden uygulanamaz. Örneğin:

```swift
class MyClass {
    static func myStaticMethod() {
        // Type Method kodu
    }
}
```

class: "class" Anahtar Kelimesi: "class" anahtar kelimesi ise alt sınıflar tarafından yeniden uygulanabilen sınıflar için kullanılır. 

```swift
class MyClass {
    class func myClassMethod() {
            // Type Method kodu
    }
}
```

Tipe Özgü Erişim: Type Methods, tipe ait olduğu için doğrudan tipe erişilerek çağrılırlar.

```swift
MyClass.myStaticMethod()
MyClass.myClassMethod()
```

Tipe Ait Özelliklere Erişim: Type Methods, tipe ait özelliklere doğrudan erişebilir ve onları değiştirebilir. 

```swift
class MyClass {
    static var count = 0
    
    static func incrementCount() {
        count += 1
    }
}

MyClass.incrementCount()
print(MyClass.count) // Çıktı: 1
```

Override Edilebilirlik: Type Methods, override edilebilen türlere (subclass) aitse, alt sınıflar tarafından yeniden uygulanabilir.





